# [博客美化]添加live2D看板娘





## 1 简介{#abstract}

给你的博客添加一个live2D看板娘~~:wink:

<!--more-->

{{< version 1.0.0 >}}

## 2 下载{#download}

你可以选择把仓库clone到本地，也可以直接使用在线CDN。

`live2D` 仓库地址是：[GitHub - xiazeyu/live2d-widget-models: The model library for live2d-widget.js](https://github.com/xiazeyu/live2d-widget-models)。

本文使用在线CDN，将如下内容复制粘贴到`your_blog_dir/themes/LoveIt/layouts/partials/footer.html`中的结尾`{{- end -}}`上一行即可。

```html
<!-- Live2D，网页上的小人，可以修改live2d_config.js来修改模型，模型都在static/live2d_models里面 -->
<!-- 你也可以把js文件下载下来，放到static/js/目录下，就不依赖别人的服务了 -->
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/live2d-widget@3.1.4/lib/L2Dwidget.min.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/live2d-widget@3.1.4/lib/L2Dwidget.0.min.js"></script>

<script type="text/javascript">
    L2Dwidget.init({
        model: {
            scale: 1,
            hHeadPos: 0.5,
            vHeadPos: 0.618,
            jsonPath: 'https://cdn.jsdelivr.net/npm/live2d-widget-model-koharu/assets/koharu.model.json',       // xxx.model.json 的路径,换人物修改这个
        },
        display: {
            superSample: 1,     // 超采样等级
            width: 120,         // canvas的宽度
            height: 300,        // canvas的高度
            position: 'left',   // 显示位置：左或右
            hOffset: 0,         // canvas水平偏移
            vOffset: 0,         // canvas垂直偏移
        },
        mobile: {
            show: true,         // 是否在移动设备上显示
            scale: 1,           // 移动设备上的缩放
            motion: true,       // 移动设备是否开启重力感应
        },
        react: {
            opacityDefault: 1,  // 默认透明度
            opacityOnHover: 1,  // 鼠标移上透明度
        },
     });
</script>
   
```
结果如下:
![](https://gitee.com/lizilong1993/image/raw/master/202111080329291.png)



















## 3 安装配置{#installation}

安装过程非常简单，就是将`jsonPath`这项的`url`替换到下图中的位置即可。
![](https://gitee.com/lizilong1993/image/raw/master/202111080333031.png)
<br>
以下为各模型的名称和样貌:
|    名字    |                                              样貌                                               |                                         jsonPath                                          |
| :--------: | :---------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------: |
|  chitose   | ![image-20211108023145450](https://gitee.com/lizilong1993/image/raw/master/202111080231492.png) |    https://cdn.jsdelivr.net/npm/live2d-widget-model-chitose/assets/chitose.model.json     |
| epsilon2_1 |       ![epsilon2_1](https://gitee.com/lizilong1993/image/raw/master/202111080229206.png)        | https://cdn.jsdelivr.net/npm/live2d-widget-model-epsilon2_1/assets/Epsilon2.1.model.json  |
|     gf     | ![image-20211108023311258](https://gitee.com/lizilong1993/image/raw/master/202111080233300.png) | https://cdn.jsdelivr.net/npm/live2d-widget-model-gf/assets/Gantzert_Felixander.model.json |
|   haru01   |            ![](https://gitee.com/lizilong1993/image/raw/master/202111080236934.png)             |     https://cdn.jsdelivr.net/npm/live2d-widget-model-haru/01/assets/haru01.model.json     |
|   haru02   | ![image-20211108023726769](https://gitee.com/lizilong1993/image/raw/master/202111080237812.png) |     https://cdn.jsdelivr.net/npm/live2d-widget-model-haru/02/assets/haru02.model.json     |
|   haruto   | ![image-20211108023821771](https://gitee.com/lizilong1993/image/raw/master/202111080238813.png) |     https://cdn.jsdelivr.net/npm/live2d-widget-model-haruto/assets/haruto.model.json      |
|   hibiki   | ![image-20211108023949675](https://gitee.com/lizilong1993/image/raw/master/202111080239720.png) |     https://cdn.jsdelivr.net/npm/live2d-widget-model-hibiki/assets/hibiki.model.json      |
|   hijiki   | ![image-20211108024056171](https://gitee.com/lizilong1993/image/raw/master/202111080240212.png) |     https://cdn.jsdelivr.net/npm/live2d-widget-model-hijiki/assets/hijiki.model.json      |
|   izumi    | ![image-20211108024156229](https://gitee.com/lizilong1993/image/raw/master/202111080241277.png) |      https://cdn.jsdelivr.net/npm/live2d-widget-model-izumi/assets/izumi.model.json       |
|   koharu   | ![image-20211108024253590](https://gitee.com/lizilong1993/image/raw/master/202111080242640.png) |     https://cdn.jsdelivr.net/npm/live2d-widget-model-koharu/assets/koharu.model.json      |
|    miku    | ![image-20211108024505026](https://gitee.com/lizilong1993/image/raw/master/202111080245066.png) |                                  同上，修改模型名字就好                                   |
|    ni-j    | ![image-20211108024550235](https://gitee.com/lizilong1993/image/raw/master/202111080245274.png) |                                  同上，修改模型名字就好                                   |
|    nico    | ![image-20211108024631880](https://gitee.com/lizilong1993/image/raw/master/202111080246919.png) |                                  同上，修改模型名字就好                                   |
|  nipsilon  | ![image-20211108024850898](https://gitee.com/lizilong1993/image/raw/master/202111080248944.png) |                                  同上，修改模型名字就好                                   |
|    nito    | ![image-20211108024939862](https://gitee.com/lizilong1993/image/raw/master/202111080249903.png) |                                  同上，修改模型名字就好                                   |
|  shizuku   | ![image-20211108025042244](https://gitee.com/lizilong1993/image/raw/master/202111080250288.png) |                                  同上，修改模型名字就好                                   |
|   tororo   | ![image-20211108025115353](https://gitee.com/lizilong1993/image/raw/master/202111080251394.png) |                                  同上，修改模型名字就好                                   |
|  tsumiki   | ![image-20211108025152572](https://gitee.com/lizilong1993/image/raw/master/202111080251609.png) |                                  同上，修改模型名字就好                                   |
| unitychan  | ![image-20211108025221904](https://gitee.com/lizilong1993/image/raw/master/202111080252943.png) |                                  同上，修改模型名字就好                                   |
|   wanko    | ![image-20211108025252364](https://gitee.com/lizilong1993/image/raw/master/202111080252409.png) |                                  同上，修改模型名字就好                                   |
|    z16     | ![image-20211108025340386](https://gitee.com/lizilong1993/image/raw/master/202111080253429.png) |                                  同上，修改模型名字就好                                   |

## 4 完成{#done}

至此已经完成全部安装配置啦！:(far fa-laugh-beam):

<br>

***觉得有帮助，麻烦顺手给我[点个Star](https://gitee.com/lizilong1993/lizilong1993)吧 or [Buy me a coffee](https://lizilong1993.gitee.io/about/)***

<br><br><br><br>

## 参考资料{#ref}

- [将live2d猫咪整合到Hugo主题LoveIt - 二次元の技术宅 (maoxuner.cn)](https://www.maoxuner.cn/post/2020/02/hugo-loveit-with-live2d-cats/)
- [个人博客挂件基于Live2d的看板娘实现和源码 - DP2PX.COM](https://dp2px.com/2019/09/19/hexo-live2d/)
- [美化系列小记：Hexo博客 | Midoriya](https://www.midoriya.co/beautify-blog/#搜索功能-algolia)


