# Valine及Valine-Admin评论系统配置


## 1 简介{#abstract}

Valine - 一款快速、简洁且高效的无后端评论系统。

Valine 诞生于2017年8月7日，是一款基于[LeanCloud](https://leancloud.cn/)的快速、简洁且高效的无后端评论系统。

理论上支持但不限于静态博客，目前已有[Hexo](https://github.com/xCss/Valine-docs/blob/master/hexo.html)、[Jekyll](https://github.com/xCss/Valine-docs/blob/master/jekyll.html)、[Typecho](http://typecho.org/)、[Hugo](https://gohugo.io/)、[Ghost](https://ghost.org/)、[Docsify](https://github.com/daidi/docsify-valine/) 等博客和文档程序在使用Valine。

<!--more-->

**特性**：

- 快速
- 安全
- Emoji 😉
- 无后端实现
- MarkDown 全语法支持
- 轻量易用
- [文章阅读量统计](https://github.com/xCss/Valine-docs/blob/master/visitor.html) `v1.2.0+`





## 2 快速开始{#prepare}

1. 你需要[注册](https://console.leancloud.cn/register)并登录Leancloud。

{{< admonition >}}
建议注册LeanCloud国际版[LeanCloud - Build better apps, faster](https://us.leancloud.cn/login.html#/signup)，这样就可以使用官方赠送的二级域名啦。
{{< /admonition >}}

2. 创建Valine应用，名称任意，例如`Valine`

![image-20211103201542321](https://gitee.com/lizilong1993/image/raw/master/202111032015802.png)

2. 进入对应的应用，点击`设置` -> `应用 Keys`，获取`AppID`和`AppKey`

![image-20211103201705991](https://gitee.com/lizilong1993/image/raw/master/202111032017056.png)

2. 以Hugo主题配置文件为例，填入对应的地方

<img src="https://gitee.com/lizilong1993/image/raw/master/202111032018813.png" alt="image-20211103201826747" style="zoom:50%;" />



{{< admonition tip"Valine参数设置" false>}}

可选参数有[配置项 | Valine 一款快速、简洁且高效的无后端评论系统。](https://valine.js.org/configuration.html)，部分参数配置如下：

|      参数      | 值                                                                                                                                                                                                |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|     appId      | AppID                                                                                                                                                                                             |
|     appKey     | AppKey                                                                                                                                                                                            |
|  placeholder   | 评论框提示文字                                                                                                                                                                                    |
|     avatar     | **可选值：**<br/>- ' '(空字符串)<br/>-  mp<br/>- identicon<br/>- monsterid<br/>- wavatar<br/>- retro<br/>- robohash<br/>- hide<br>具体参数含义请看[头像配置](https://valine.js.org/avatar.html)。 |
|      meta      | 默认值:`['nick','mail','link']`                                                                                                                                                                   |
|    pageSize    | 评论列表分页，每页条数。                                                                                                                                                                          |
|      lang      | 默认值:`zh-CN`，可选值：`zh-CN`，`zh-TW`，`en`，`ja`。                                                                                                                                            |
|    visitor     | [文章访问量统计](https://valine.js.org/visitor.html)                                                                                                                                              |
|   highlight    | `代码高亮`，默认开启，若不需要，请手动关闭                                                                                                                                                        |
|  avatarForce   | 每次访问`强制`拉取最新的`评论列表头像`，不推荐设置为`true`，目前的`评论列表头像`会自动带上`Valine`的版本号                                                                                        |
|    recordIP    | 是否记录评论者IP                                                                                                                                                                                  |
|   serverURLs   | 默认值: `http[s]://[tab/us].avoscloud.com`，该配置适用于国内`自定义域名`用户, `海外版本`会自动检测(无需手动填写)                                                                                  |
|    emojiCDN    | 设置`表情包CDN`，参考[自定义表情](https://valine.js.org/emoji.html)                                                                                                                               |
|   emojiMaps    | 设置`表情包映射`，参考[自定义表情](https://valine.js.org/emoji.html)                                                                                                                              |
|    enableQQ    | 是否启用`昵称框`自动获取`QQ昵称`和`QQ头像`, 默认关闭，需`博/网站主`主动启用                                                                                                                       |
| requiredFields | 设置`必填项`，默认值: []，默认`匿名`，可选值：['nick']，['nick','mail']                                                                                                                           |

{{< /admonition >}}





## 3 Valine应用配置 {#installation}

1. 查看评论
   点击 `存储 `-> `结构化数据`，选择创建`Class`，名称`Comment`，其他保持默认，以后就可在此`Class`内查看

![image-20211103204537280](https://gitee.com/lizilong1993/image/raw/master/202111032045367.png)

2. 文章阅读量统计
   点击 `存储 `-> `结构化数据`，选择创建`Class`，名称`CounterCounter`，其他保持默认，以后就可在此`Class`内查看

![image-20211103204345812](https://gitee.com/lizilong1993/image/raw/master/202111032043906.png)

## 4 Valine-Admin{#add}

### 4.1 简介
[Valine-Admin](https://github.com/hongweifuture/Valine-Admin) 项目是一个对 Valine 评论系统的拓展应用，可增强 Valine 的邮件通知功能。基于 Leancloud 的云引擎与云函数，主要实现`评论邮件通知`、`评论管理`、`自定义邮件通知模板`等功能，而且还可以提供`邮件通知站长 `和 `@ 通知 `的功能。

[Valine-Admin邮件通知展示](https://github.com/hongweifuture/Valine-Admin/blob/master/高级配置.md#邮件通知展示)



### 4.2 Valine-Admin部署

1. 需要确保 Valine 的基础功能是正常的，参考 Valine Docs。
2. 进入 Leancloud 对应的 Valine 应用中。
3. 点击 云引擎 -> 设置 填写代码库：https://github.com/hongweifuture/Valine-Admin，保存

![代码库](https://gitee.com/lizilong1993/image/raw/master/202111032052022.png)

4. 设置自定义环境变量，需要设置云引擎的环境变量以提供必要的信息，变量参数参考下面的配置项

| 变量          | 示例                              | 说明                                                                                                                                                                                                                                                                           |
| ------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SITE_NAME     | Lizilong’s Blog                   | [必填] 网站名称                                                                                                                                                                                                                                                                |
| SITE_URL      | https://lizilong1993.gitee.io     | [必填] 网站地址，**最后不要加 `/`**                                                                                                                                                                                                                                            |
| SMTP_SERVICE  | QQ                                | [必填] 邮件服务提供商，支持 QQ、163、126、Gmail 以及 [更多](https://nodemailer.com/smtp/well-known/#supported-services)。 --- *如这里没有你使用的邮件提供商，请查看[自定义邮件服务器](https://github.com/hongweifuture/Valine-Admin/blob/master/高级配置.md#自定义邮件服务器)* |
| SMTP_USER     | [xxxx@qq.com](mailto:xxxx@qq.com) | [必填] SMTP登录用户，一般为邮箱地址                                                                                                                                                                                                                                            |
| SMTP_PASS     | xxxx                              | [必填] SMTP登录密码，一般为授权码，而不是邮箱的登陆密码，请自行查询对应邮件服务商的获取方式                                                                                                                                                                                    |
| SENDER_NAME   | Blog-评论提醒                     | [可选] 发件人                                                                                                                                                                                                                                                                  |
| ADMIN_URL     | https://xxxx.avosapps.us/         | [建议] 云引擎域名，用于自动唤醒                                                                                                                                                                                                                                                |
| TO_EMAIL      | xxxxx@qq.com                      | [可选] 指定站长收信邮箱，默认值为`SITE_USER`。用于 SMTP 发件人与站长收件人不一致的情况下使用。                                                                                                                                                                                 |
| TEMPLATE_NAME | rainbow                           | [可选] 通知邮件的模板（default和rainbow），参考高级功能                                                                                                                                                                                                                        |

5. 点击 `云引擎` -> `部署`，选择`Git源码部署`，分支或版本号输入master，下载最新依赖（可选），部署

![Git](https://gitee.com/lizilong1993/image/raw/master/202111032104883.png)

![master](https://gitee.com/lizilong1993/image/raw/master/202111032104228.png)



### 4.3 后台管理功能

1. 点击 `云引擎 `-> `设置`，在Web主机域名位置点击申请，获取二级域名，现在的二级域名不支持自定义，如果想好记请参考高级功能

![image-20211103210628507](https://gitee.com/lizilong1993/image/raw/master/202111032106583.png)

2. 设置后台管理登录信息，点击 `存储 `-> `结构化数据`，选择`_User` ->` 添加行`，只需要填写`password`、`username`、`email`这三个字段即可, 使用 `email` 作为账号登陆、`password `作为账号密码、`username `任意即可。

{{< admonition warning"注意" true>}}

为了安全考虑，此 email **必须**为配置中的 SMTP_USER 或 TO_EMAIL， 否则不允许登录。

{{< /admonition >}}

3. 此后，可以通过https://二级域名.leanapp.cn/管理评论。

### 4.4 定时任务

免费版的 LeanCloud 容器，是有强制性休眠策略的，不能 24 小时运行：

- 每天必须休眠 6 个小时

- 30 分钟内没有外部请求，则休眠

- 休眠后如果有新的外部请求实例则马上启动（但激活时此次发送邮件会失败）。

分析了一下上方的策略，如果不想付费的话，最佳使用方案就**设置定时器**，目前基于 LeanCloud 自带定时器实现了**两种云函数定时任务**：

- 自动唤醒，定时访问Web APP二级域名防止云引擎休眠（推荐）
- 定时检查，每天定时检查24小时内漏发的邮件通知

1. 首先需要添加环境变量，点击 云引擎 -> 设置，配置自定义环境变量，变量名ADMIN_URL，变量值Web 主机域名，即二级域名地址，添加后重启容器环境变量才会生效

![image-20211103211141819](https://gitee.com/lizilong1993/image/raw/master/202111032111907.png)2. 配置定时任务，击 云引擎 -> 定时任务

- 配置**自动唤醒**（推荐），`创建定时任务`，名称任意，生产环境选择`self-wake`云函数，Cron表达式填入`0 */20 7-23 * * ?`，表示每天 7 - 23 点每 20 分钟访问一次，这样可以保持每天的绝大多数时间邮件服务是正常的。
- 配置**定时检查**，`创建定时任务`，名称任意，生产环境选择`resend-mails`云函数，Cron表达式填入`0 0 8 * * ?`，表示每天早8点检查过去24小时内漏发的通知邮件并补发



{{< admonition warning"注意" true>}}

Valine-admin由于Leancloud`标准版流控原因`，自动唤醒任务可能会**失败**，（升级版不会控流）详情：https://forum.leancloud.cn/t/topic/22595

这里介绍一个使用第三方计划任务网站[cron-job](https://cron-job.org/en/signup/)进行定时唤醒Valine-admin的方法。具体操作参考如下文章：

[使用cron-job解决Valine-admin因流控原因自动唤醒失败的问题_HCL_Lonely的博客-CSDN博客](https://blog.csdn.net/HCL_Lonely/article/details/106446183)

{{< /admonition >}}

<br>


## 5 完成{#done}

至此基于Valine和Valine-Admin的个人博客评论功能已经完成搭建完成啦！:(far fa-laugh-beam):



觉得有帮助，麻烦顺手给我[点个Star](https://gitee.com/lizilong1993/lizilong1993)吧 or [Buy me a coffee](https://lizilong1993.gitee.io/about/)



## 参考资料{#ref}

- [配合 Valine 评论系统使用的 Valine-Admin 及显示个性头像_Johnny's Lab-CSDN博客](https://blog.csdn.net/z_johnny/article/details/104211572)
- [ZhaoqiangCn/Valine-Admin: 一个 Valine 的拓展应用，用来增强 Valine 的邮件通知。 (github.com)](https://github.com/ZhaoqiangCn/Valine-Admin)
- [Valine评论之Valine-admin配置攻略 - antmoe - 博客园 (cnblogs.com)](https://www.cnblogs.com/antmoe/p/12904118.html)
- [使用cron-job解决Valine-admin因流控原因自动唤醒失败的问题_HCL_Lonely的博客-CSDN博客](https://blog.csdn.net/HCL_Lonely/article/details/106446183)。


