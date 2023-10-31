# 视频流服务器搭建[简单版]


## 1 视频流介绍{#abstract}

###  1.1视频流协议

几种不同视频流协议的优缺点如下[1]：

![三种协议](https://gitee.com/lizilong1993/image/raw/master/20210122084333.png)
<center>三种协议总结</center>

### 1.2 直播点播框架

![](https://cdn.ar414.com/ar414-nginx-rtmp.png)
<center>分流+水印的直播系统拓扑图</center>

## 2 视频流点播服务器搭建[2]{#VOD}

### 2.1 环境搭建

#### Docker容器

rtmp服务默认端口是1935，另外安装nginx后需要进行验证，需要开放一个http端口，为了防止和宿主机的8080端口冲突，这里我们使用**8082**端口；我们需要将视频文件拷贝到容器中，因此还需要挂载一个目录，因此docker容器运行命令如下所示:

~~~ bash
docker run --name video -v /Users/lzl/files:/root/videos -d -i -p 8082:8082  -p 1935:1935 ubuntu:18.04 && docker ps
~~~
命令很执行完成之后，docker返回结果如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123211451.png)
在上图中中可以看到已经有一个容器运行了，接着我们需要进入容器安装nginx和rtmp模块，进入容器命令如下所示
~~~bash
docker exec -it video bash
~~~
命令执行完成之后，返回信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123211406.png)

#### 国内镜像加速源

docker的Ubuntu镜像apt软件源默认使用官方域名，这个域名在国内访问非常慢，为了后续安装速度能够更快，我们将apt的软件源更换成阿里云源的地址，执行命令如下所示
~~~bash
echo 'deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
' > /etc/apt/sources.list  && cat /etc/apt/sources.list
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123211726.png)
从上图中可以看到已经执行成功，已经使用阿里云的软件源替代了默认的软件源。

#### 更新软件源列表

接下来我们更新一下本地的软件源信息，执行命令如下所示
~~~ bash
apt update
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123212108.png)
从上图中可以看到已经从阿里云中更新了软件源信息，更新速度也非常快，到此我们已经完成运行环境的基础准备。

### 2.2 Nginx安装

在我们更新apt软件源完成之后，就可以安装Nginx等一些软件的依赖环境，执行的命令如下所示
~~~ bash
apt-get install -y libpcre3 libpcre3-dev libssl-dev zlib1g-dev gcc  wget unzip vim make curl
~~~
安装的依赖软件有点多，会根据你的网速安装速度也不一样，命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123213108.png)
![](https://gitee.com/lizilong1993/image/raw/master/20210123213146.png)
从上图中可以看到依赖已经安装完成，接下来我们开始安装nginx，nginx不能使用apt安装，需要源码编译安装才可以，因为需要我们编译一个模块进去。

#### 源码下载

我们首先将需要的模块下载下来，这里我不准备使用*nginx-rtmp-module*，而是使用*nginx-http-flv-module*来替代，因为后者是基于前者开发的，前者拥有的功能后者都有，后者是国内的开发开发，有中文文档，所以就采用它了，首先将它下载下来并解压，执行的命令如下所示
~~~bash
wget https://github.com/winshining/nginx-http-flv-module/archive/master.zip ; unzip master.zip
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123213510.png)
从上图中可以看出已经下载并解压完成，接着我们还需要下载nginx本身的源码，下载Nginx源码并解压的命令如下所示
~~~bash
wget http://nginx.org/download/nginx-1.17.6.tar.gz  && tar -zxvf nginx-1.17.6.tar.gz
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123213632.png)
![](https://gitee.com/lizilong1993/image/raw/master/20210123213709.png)
下载并解压完成，到此我们两个所需要的源码都准备完成。

#### 编译安装

接着我们进入编译安装环节，首先进入刚才解压的nginx目录当中，执行的命令如下所示
~~~bash
cd  nginx-1.17.6 && ls
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123213835.png)
从上图中可以看到解压出来的目录结构，我们执行./configure便可以配置编译参数，这个地方我们需要将刚才下载的插件*nginx-http-flv-module*加入进来,执行的命令如下所示
~~~bash
./configure --add-module=../nginx-http-flv-module-master
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123214010.png)
在上图中可以看到准备编译已经完成，但在编译的过程当中有可能会出现一些意外因素，nginx默认编译非常严格，只要遇到一些意外就会中断编译，因此我们将一些非致命的意外设置为警告模式，执行命令如下所示
~~~bash
vim objs/Makefile
~~~
在当前文件夹下有一个*objs/Makefile*文件，我们将里面的-Werror删除，用vim打开文件后如下所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123214201.png)
删除之后，保存并退出，接着就可以进行编译Nginx了，编译的过程稍微有点长，执行的命令如下所示
~~~bash
make
~~~
命令执行之后，返回的信息如下图所示

![](https://gitee.com/lizilong1993/image/raw/master/20210123214647.png)
在上图中可以看到一些Nginx的一些日志存放路径信息，当我们执行安装命令后，就会往这些文件里写入相应信息，执行安装命令如下所示
~~~bash
make install
~~~
安装命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123214756.png)
在上图中可以可以看到安装过程大致执行了哪些命令，安装完成后接下来需要进行一些简单的配置就可以使用了.

###  2.3 配置rtmp服务

在完成Nginx的安装之后，我们需要对Nginx进行一番配置，并启动Nginx服务。

#### 添加rtmp服务

我们直接使用vim命令去编辑Nginx的配置文件，执行命令如下所示
~~~bash
vim /usr/local/nginx/conf/nginx.conf
~~~
vim命令执行之后，打开的编辑窗口如下所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123215003.png)
我们将以下配置信息复制并粘贴到配置文件信息里面，放在http配置上面
~~~ xml
rtmp {                #RTMP服务
   server {
       listen 1935;  #//服务端口
        chunk_size 4096;   #//数据传输块的大小
 
 
        application vod {
                play /opt/video/vod; #//视频文件存放位置。
        }
   }
}
~~~
> tips：
> vim快捷键
> - x删除光标选中字符
> - X删除左边字符
> - Esc退出编辑模式
> - :wq保存并退出

#### 验证配置

粘贴完成并保存之后，我们在终端执行nginx -t命令，来测试一下配置文件是否有异常，执行命令如下所示
~~~bash
/usr/local/nginx/sbin/nginx -t
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123220847.png)
在上图中可以看出Nginx提示我们配置文件没有异常，说明我们配置没有语法错误，我们启动一下Nginx并使用curl命令来测试启动是否成功，执行命令如下所示
~~~bash
/usr/local/nginx/sbin/nginx && curl http://127.0.0.1
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123221043.png)
从上图中Nginx返回的信息可以看出我们Nginx服务已经启动成功.

### 2.4 视频播放

在上述环节都操作完毕之后，此时基本都处于正常，现在我们就可以开始来播放视频了，不过我们还需要在视频目录下放一个视频文件，这样才能播放到这个视频。

#### 添加视频文件

接着我们创建一个存放视频的文件夹，并将权限设置设置为777，防止因为权限问题导致无法播放，执行命令如下所示
~~~bash
mkdir -p /opt/video/vod  && chmod -R 777 /opt/video/vod
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123221334.png)
在上图中可以看出，创建文件夹和设置权限命令已经执行完成，接着我们需要将我们准备好的视频文件复制到我们之前配置指定的目录下，执行命令如下所示
~~~bash
cp /home/lzl/video/LJ3-01_SVC_WHU_00100_20190701T101239_FS_OVE_0001_L2A_0001_CMOS1.mp4 /opt/video/vod &&  ls /opt/video/vod
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123230714.png)
在上图中可以看出，已经将视频文件LJ3-01_SVC_WHU_00100_20190701T101239_FS_OVE_0001_L2A_0001_CMOS1.mp4文件复制到此目录中，接着我们就可以测试播放了；不过在测试播放之前我们需要安装一个视频播放器，因为浏览器是不支持rtmp协议。
> tips
> 如果显示cp:cannot stat "xxx",no such file or directory,就需要退出容器从主机往容器内上传文件，具体参考[docker从容器里面拷文件到宿主机或从宿主机拷文件到docker容器里面](https://www.cnblogs.com/jifeng/p/10930111.html)。

### 2.5 安装VLC播放器

一般用于调试流媒体我们习惯使用vlc播放器，我们去官网下载一下他，官网地址如下

https://www.videolan.org/
安装完成后，打开软件，选择*媒体->打开网络串流*
![](https://gitee.com/lizilong1993/image/raw/master/20210123230954.png)
在上图中可以看到窗口中有一个输入框，将如下播放地址复制进去之后，点击右下方的open按钮，就可以开始播放了。

~~~bash
rtmp://125.220.153.38/vod/LJ3-01_SVC_WHU_00100_20190701T101239_FS_OVE_0001_L2A_0001_CMOS1.mp4
~~~
点击后成功播放效果下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210123231549.png)
至此Nginx+rtmp模块搭建点播服务已经成功了。

##  3 视频流直播服务器搭建[3]{#live_stream}

搭建好了点播服务，还需要继续搭建直播服务。

### 3.1 配置rtmp直播服务

我们需要在nginx配置文件中增加直播的配置，这里我们依然使用vim命令打开配置文件，执行命令如下
~~~ bash
vim  /usr/local/nginx/conf/nginx.conf
~~~
vim命令执行结果如下
![](https://gitee.com/lizilong1993/image/raw/master/20210124124252.png)
我们将直播配置添加到rtmp项配置下面，其中的含义已经在配置中注明，配置如下所示

~~~ bash
application live{
            live on;        #直播
 
            #回看功能 视频切片变成ts文件
            hls on;                                 #这个参数把直播服务器改造成实时回放服务器。
            wait_key on;                           #对视频切片进行保护，这样就不会产生马赛克了。
            hls_path /opt/video/rtmp/hls;       #切片视频文件存放位置。
            hls_fragment 10s;                       #每个视频切片的时长。
            hls_playlist_length 60s;                #总共可以回看的事件，这里设置的是1分钟。
            hls_continuous on;                      #连续模式。
            hls_cleanup on;                         #对多余的切片进行删除。
            hls_nested on;                          #嵌套模式。
 
        }        
~~~
添加后如下
![](https://gitee.com/lizilong1993/image/raw/master/20210124130607.png)

接着我们再将另外一项配置增加到HTTP服务中，这个是用来监控我们的推流状态的，如果不配置我们就不方便监控推流的状态；我们容器映射到外面的http端口为**8082**，所以这里我们也把NGINX里面的HTTP端口也改为**8082**，这样我们才可以访问到
![](https://gitee.com/lizilong1993/image/raw/master/20210124150700.png)
然后，添加配置项如下
~~~ bash
    location /stat {
        rtmp_stat all;
        rtmp_stat_stylesheet stat.xsl;
    }
 
    location /stat.xsl {
       root /nginx-http-flv-module-master/;
   }
~~~

增加配置之后，如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210124133817.png)
在上图中可以看到，上面有一个配置路径是/nginx-http-flv-module-master/这是我们开始下载源码解压的位置，如果你解压的位置不是这个，就需要将这里改成你解压的位置。

设置好nginx配置之后，我们保存并退出，然后你重启nginx服务器，让刚才的配置生效,重启的命令如下
~~~ bash
/usr/local/nginx/sbin/nginx -s reload
~~~
命令执行之后，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210124133941.png)
在上图中可以看到重启没有报错，说明我们的配置没有出现语法错误，并且重启已经成功了。

### 3.2 OBS推流

在上面nginx配置完成之后，其实直播服务已经搭建完成了，但是我们还需要验证一下，最简单的方式就是推流然后去拉流播放，推流我们一般使用obs进行推流，官网地址如下所示
https://obsproject.com/
把OBS下载并安装好之后，打开界面如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210124134135.png)

点击下图加号添加媒体源
![](https://gitee.com/lizilong1993/image/raw/master/20210124134321.png)

我这里选的是笔记本摄像头
![](https://gitee.com/lizilong1993/image/raw/master/20210124134443.png)

接着点击下图右侧的**开始推流**
![](https://gitee.com/lizilong1993/image/raw/master/20210124134516.png)

然后选择**推流**，填写服务器地址和串流密钥，我这里随便填的test。
![](https://gitee.com/lizilong1993/image/raw/master/20210124134741.png)
服务器地址+串联密钥就是你推流到服务器的地址。
设置好之后点击下方的确定，然后回到主窗口中点击开始推流按钮，就会开始推流，如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210124150955.png)
在上图中可以下方的状态栏可以看到已经在开始推流了，其中的LIVE后面的为当期推流持续时间，CPU后面的百分比代表推流占用了多少CUP资源，在客户端显示推流成功之后，我们可以通过浏览器访问推流监控页面，地址如下所示
http://125.220.153.38:8082/stat

浏览器打开监控页面，返回的信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210124151051.png)

### 3.3 VLC拉流

打开VLC，选择*媒体——>打开网络串流*，填入刚刚OBS推流的地址+串联密钥，也就是下图
![](https://gitee.com/lizilong1993/image/raw/master/20210124151204.png)

结果如下
![](https://gitee.com/lizilong1993/image/raw/master/20210124151519.png)

在上图中可以看到已经开始播放我刚才推送上去的视频了。

目测两者之前有大约3-5s的延迟。

### 3.4 直播转录播

如果我们需要将推流的视频存保留下来将来用作回放，并不需要特意配置，因为nginx-http-flv-module-master模块已经帮我们保存了，保存的位置是在nginx配置中hls_path项设置的位置，我们通过CD命令查看一下，执行命令如下所示
~~~bash
cd /opt/video/rtmp/hls/test1 && ls
~~~

命令执行之后，返回的文件列表信息如下图所示
![](https://gitee.com/lizilong1993/image/raw/master/20210124151916.png)

在上图中可以看到TS片，到此我们通过nginx+rtmp搭建直播服务已经完成了。

## 参考文献{#ref}

> 视频流协议

[1] [理解RTMP、HttpFlv和HLS的正确姿势](https://www.jianshu.com/p/32417d8ee5b6)



> 搭建视频服务器



[2] [Ubuntu中使用Nginx+rtmp模块搭建流媒体视频点播服务](https://blog.csdn.net/weixin_39822629/article/details/110488219)



[3] [Ubuntu中使用Nginx+rtmp搭建流媒体直播服务](https://blog.csdn.net/u013431141/article/details/103768139?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)


