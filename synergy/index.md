# [神器推荐]Synergy——类KVM的多电脑键盘鼠标共享工具





## 1 简介{#abstract}

synergy是一款键盘鼠标共享工具，方便大家使用一个键盘鼠标来操控多台电脑，支持windows、Linux、mac和Raspberry Pi。

<!--more-->



{{< admonition info "特性" true >}}

- 多设备连接（最高15台设备）

- 无缝切换

- Win到Command自动切换
- 自定义快捷键
- 共用剪切板

{{< /admonition >}}



## 2 下载{#prepare}

Synergy 1.5改为收费软件了，不过有大神提供了激活码生成工具。



{{< admonition warning "注意" true >}}

如果有余力，还请支持[正版激活](https://symless.com/synergy/features)。

{{< /admonition >}}



你可以按照自己的需求去数码荔枝来下载试用版[下载 Synergy ](https://dl.lizhi.io/synergy)，然后参考以下文章激活。后文会显示详细安装激活过程。

- [C++ Shell (cpp.sh)](http://cpp.sh/3mjw3)
- [MrLithium's blog: Synergy and Serial Number Activation Key for SSL security - Reverse Engineering the source code (easy)](https://mrlithium.blogspot.com/2017/06/synergy-serial-number-activation-key.html)

{{< admonition tip "注意" false >}}

请选择**本地下载**

<img src="https://gitee.com/lizilong1993/image/raw/master/202111041029026.png" alt="image-20211104102835806" style="zoom: 25%;" />

{{< /admonition >}}







## 3 安装激活{#installation}

安装过程非常简单，就不介绍了，现在主要介绍一下激活过程。

1. 打开[C++ Shell (cpp.sh)](http://cpp.sh/3mjw3)

![image-20211104103633872](https://gitee.com/lizilong1993/image/raw/master/202111041036971.png)

2. `Optimization level`选最后那个`Maximum`，然后点击`Run`

3. 接下来按照提示填写就好（内容真假无所谓），如下：

<div align=center>
<img src="https://gitee.com/lizilong1993/image/raw/master/202111041039183.png" alt="image-20211104102835806" style="zoom: 50%" />
</div>

4. 这行字符串就是生成的激活码，**一个激活码可以激活多台电脑**。
5. 打开软件，点击`文件`->`激活`，填入激活码即可。

<div align=center>
<img src="https://gitee.com/lizilong1993/image/raw/master/202111041102372.png" alt="image-20211104102835806" style="zoom: 50%" />
</div>

<br><br>

## 4 配置{#config}

Synergy分为`Server `和 `Client`，也就是两台电脑必须有一台作为Server，而键盘鼠标是连接在Server上的，Client通过`Server IP地址`或`名称`来连接Server从而共用Server的键鼠设备。



{{< admonition warning "注意" true >}}

键盘鼠标一定要连接在Server端上，并且Server电脑是用**固定IP**的，使用Server name连不上，亲测:(fas fa-grin-squint-tears):

{{< /admonition >}}
<br>
1. **服务器端配置如下：**

![](https://gitee.com/lizilong1993/image/raw/master/202111041117750.jpg)
{{< admonition tip "注意" true >}}

这里电脑的排列与物理世界的摆放方位一定要一致！

{{< /admonition >}}
2. **客户端配置如下：**

![](https://gitee.com/lizilong1993/image/raw/master/202111041121620.png)

这里填入Server端的IP就好。

最后，在两边都点击应用就可以连接起来啦！

![](https://gitee.com/lizilong1993/image/raw/master/202111041122896.png)

## 5 完成{#done}

至此已经完成全部安装配置啦！:(far fa-laugh-beam):

<br>

***觉得有帮助，麻烦顺手给我[点个Star](https://gitee.com/lizilong1993/lizilong1993)吧 or [Buy me a coffee](https://lizilong1993.gitee.io/about/)***

<br><br><br><br>

## 参考资料{#ref}

- [synergy 一套键鼠多台设备共享 | 家的博客 (anjia0532.github.io)](https://anjia0532.github.io/2017/02/08/share-mouse-and-keyboard-with-your-windows-linux-machines-md/)


