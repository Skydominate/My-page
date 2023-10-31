# 十分钟搭建一个私人的LoveIt风格博客



***大概只需要十分钟即可搭建完成一个类似上图的私人博客.***

## 1 简介{#abstract}

Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。
{{< admonition warning "注意" true >}}
 本教程只为快速搭建一个风格跟LoveIt展示页**几乎一样**的个人博客,只在源代码上进行了简单修改.**如果**想要完全打造一个个人风格的博客,还需要后续自行改造.
{{< /admonition >}}

<!--more-->

{{< admonition info ":(far fa-kiss-wink-heart):" false >}}
觉得不错的话请给原作者[LoveIt](https://github.com/dillonzq/LoveIt)点个Star吧,当然也请顺便给我[lizilong1993](https://gitee.com/lizilong1993/lizilong1993)点个Star吧,谢谢!
{{< /admonition >}}



## 2 环境准备{#prepare}

你需要下载如下软件：

- [hugo](https://github.com/gohugoio/hugo/releases/tag/v0.89.0)
- Git
- [LoveIt](https://github.com/dillonzq/LoveIt)

{{< admonition >}}
Hugo **extended** 版本能够支持支持更多的Markdown语法,建议下载Hugo**extended**版本.
{{< /admonition >}}

![image-20211103140407490](https://gitee.com/lizilong1993/image/raw/master/202111031404590.png)



{{< admonition tip"镜像下载地址" true>}}
如果github下载网速堪忧的话，也可以去gitee自行搜索，或者直接点击如下链接下载。

- [hugo_extended_0.88.1_Windows-64bit.zip](https://gitee.com/lizilong1993/image/raw/master/202111031411672.zip)

- [LoveIt-0.2.10.zip](https://gitee.com/lizilong1993/image/raw/master/202111031409842.zip)

{{< /admonition >}}

hugo下载解压后如下：

![image-20211103141748934](https://gitee.com/lizilong1993/image/raw/master/202111031417986.png)

LoveIt主题下载解压后如下：

![image-20211103141616088](https://gitee.com/lizilong1993/image/raw/master/202111031416163.png)



Hugo下载完成解压后如下

![image-20211103140443419](https://gitee.com/lizilong1993/image/raw/master/202111031404462.png)





## 3 主题安装 {#installation}

### 3.1 创建你的项目

Hugo 提供了一个 `new` 命令来创建一个新的网站:

```bash
hugo new site myblog
cd myblog
```
运行结果如下:

![image-20211103142610000](https://gitee.com/lizilong1993/image/raw/master/202111031426054.png)



{{< admonition tip "注意" false>}}
Hugo存放的文件夹路径需要添加到系统环境变量中去。
![](https://gitee.com/lizilong1993/image/raw/master/202111031430222.png)

可以通过`CMD`执行 

```bash
hugo version
```

来判断环境变量是否配置正确。

{{< /admonition >}}

### 3.2 安装主题

请把下载主题文件[LoveIt-0.2.10.zip](https://gitee.com/lizilong1993/image/raw/master/202111031409842.zip)解压放到 `themes` 目录.

![image-20211103145445838](https://gitee.com/lizilong1993/image/raw/master/202111031454887.png)

{{< admonition tip "注意" false>}}

请将文件夹名称修改为`LoveIt`,或者你也可以修改`myblog/config.toml`文件中的`theme`字段。

![](https://gitee.com/lizilong1993/image/raw/master/202111031459634.png)

{{< /admonition >}}



## 4 配置主题

{{< admonition note"注意" true>}}

这里是关键步骤，虽然有点不求甚解，但是真的能够省很多功夫，问题就是后期修改需要经常去翻LoveIt的官方文档。

{{< /admonition >}}

### 4.1 文件替换

将`myblog/themes/LoveIt/exampleSite`路径下的所有文件直接复制到`myblog/`下**覆盖**掉。

其中：

- `assets`存放全局资源
- `content`存放md文件，即你的文章
- `static`存放静态资源
- `config.toml`为博客配置文件

完成上面这步应该就能实现跟LoveIt官网（如下图）一模一样的效果了。

![image-20211103151042819](https://gitee.com/lizilong1993/image/raw/master/202111031510953.png)

使用`hugo serve`命令启动网站来看看效果吧。

 

{{< admonition tip"注意" true>}}

由于LoveIt主题使用了 Hugo 中的 `.Scratch `来实现一些特性, 非常建议你为` hugo server `命令添加 `--disableFastRender `参数来实时预览你正在编辑的文章页面.

```bash
hugo serve --disableFastRender
```

`hugo serve` 的默认运行环境是 `development`, 而 `hugo` 的默认运行环境是 `production`。

由于本地 `development` 环境的限制, **评论系统**, **CDN** 和 **fingerprint** 不会在 `development` 环境下启用.

你可以使用 `hugo serve -e production` 命令来开启这些特性。

{{< /admonition >}}

### 4.2 参数修改

至此只需要修改一下`myblog/config.toml`中的参数即可完成主题配置。

首先复制如下内容**覆盖**原始的`myblog/config.toml`里的内容。

```toml
baseURL = "https://example.com"
# [en, zh-cn, fr, pl, ...] determines default content language
# [en, zh-cn, fr, pl, ...] 设置默认的语言
defaultContentLanguage = "zh-cn"
# theme
# 主题
theme = "LoveIt"
# themes directory



# website title
# 网站标题
title = "Lizilong's Blog"

# whether to use robots.txt
# 是否使用 robots.txt
enableRobotsTXT = true
# whether to use git commit log
# 是否使用 git 信息
enableGitInfo = false
# whether to use emoji code
# 是否使用 emoji 代码
enableEmoji = true

[languages]
  [languages.en]
    weight = 2
    # language code
    languageCode = "en"
    # language name
    languageName = "English"
    # whether to include Chinese/Japanese/Korean
    hasCJKLanguage = false
    # default amount of posts in each pages
    paginate = 12
    # [UA-XXXXXXXX-X] google analytics code
    googleAnalytics = ""
    # copyright description used only for seo schema
    copyright = "This work is licensed under a Creative Commons Attribution-NonCommercial 4.0 International License."
    # Menu config
    [languages.en.menu]
      [[languages.en.menu.main]]
        identifier = "posts"
        # you can add extra information before the name (HTML format is supported), such as icons
        pre = ""
        # you can add extra information after the name (HTML format is supported), such as icons
        post = ""
        name = "Posts"
        url = "/posts/"
        # title will be shown when you hover on this menu link.
        title = ""
        weight = 1
      [[languages.en.menu.main]]
        identifier = "tags"
        pre = ""
        post = ""
        name = "Tags"
        url = "/tags/"
        title = ""
        weight = 2
      [[languages.en.menu.main]]
        identifier = "categories"
        pre = ""
        post = ""
        name = "Categories"
        url = "/categories/"
        title = ""
        weight = 3
      [[languages.en.menu.main]]
        identifier = "documentation"
        pre = ""
        post = ""
        name = "Docs"
        url = "/categories/documentation/"
        title = ""
        weight = 4
      [[languages.en.menu.main]]
        identifier = "about"
        pre = ""
        post = ""
        name = "About"
        url = "/about/"
        title = ""
        weight = 5
      [[languages.en.menu.main]]
        identifier = "github"
        pre = "<i class='fab fa-github fa-fw'></i>"
        post = ""
        name = ""
        url = "https://github.com/xxxxx"
        title = "GitHub"
        weight = 6
    [languages.en.params]
      # site description
      description = "About Me"
      # site keywords
      keywords = ["Theme", "Hugo"]
      # App icon config
      [languages.en.params.app]
        # optional site title override for the app when added to an iOS home screen or Android launcher
        title = "xxx's Blog"
        # whether to omit favicon resource links
        noFavicon = false
        # modern SVG favicon to use in place of older style .png and .ico files
        svgFavicon = ""
        # Android browser theme color
        themeColor = "#ffffff"
        # Safari mask icon color
        iconColor = "#5bbad5"
        # Windows v8-10 tile color
        tileColor = "#da532c"
      # Search config
      [languages.en.params.search]
        enable = true
        # type of search engine ("lunr", "algolia")
        type = "algolia"
        # max index length of the chunked content
        contentLength = 4000
        # placeholder of the search bar
        placeholder = ""
        # max number of results length
        maxResultLength = 10
        # snippet length of the result
        snippetLength = 30
        # HTML tag name of the highlight part in results
        highlightTag = "em"
        # whether to use the absolute URL based on the baseURL in search index
        absoluteURL = false
        [languages.en.params.search.algolia]
          index = "index.en"
          appID = "PASDMWALPK"
          searchKey = "b42948e51daaa93df92381c8e2ac0f93"
      # Home page config
      [languages.en.params.home]
        # amount of RSS pages
        rss = 10
        # Home page profile
        [languages.en.params.home.profile]
          enable = true
          # Gravatar Email for preferred avatar in home page
          gravatarEmail = ""
          # URL of avatar shown in home page
          avatarURL = "/images/avatar.png"
          # title shown in home page (HTML format is supported)
          title = ""
          # subtitle shown in home page
          subtitle = "Record niceness and enjoy life"
          # whether to use typeit animation for subtitle
          typeit = true
          # whether to show social links
          social = true
          # disclaimer (HTML format is supported)
          disclaimer = ""
        # Home page posts
        [languages.en.params.home.posts]
          enable = true
          # special amount of posts in each home posts page
          paginate = 6
      # Social config in home page
      [languages.en.params.social]
        GitHub = "xxxx"
        Weibo = "xxxx"
        Zhihu = "xxx"
        Douban = ""
        Googlescholar = ""
        Researchgate = ""
        Bilibili = "xxx"
        Email = "xxxx"
        RSS = true


  [languages.zh-cn]
    weight = 1
    # 网站语言, 仅在这里 CN 大写
    languageCode = "zh-CN"
    # 语言名称
    languageName = "简体中文"
    # 是否包括中日韩文字
    hasCJKLanguage = true
    # 默认每页列表显示的文章数目
    paginate = 12
    # [UA-XXXXXXXX-X] 谷歌分析代号
    googleAnalytics = ""
    # 版权描述，仅仅用于 SEO
    copyright = "This work is licensed under a Creative Commons Attribution-NonCommercial 4.0 International License."
    # 菜单配置
    [languages.zh-cn.menu]
      [[languages.zh-cn.menu.main]]
        identifier = "posts"
        # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
        pre = ""
        # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
        post = ""
        name = "所有文章"
        url = "/posts/"
        title = ""
        weight = 1
      [[languages.zh-cn.menu.main]]
        identifier = "tags"
        pre = ""
        post = ""
        name = "标签"
        url = "/tags/"
        title = ""
        weight = 2
      [[languages.zh-cn.menu.main]]
        identifier = "categories"
        pre = ""
        post = ""
        name = "分类"
        url = "/categories/"
        title = ""
        weight = 3
      [[languages.zh-cn.menu.main]]
        identifier = "documentation"
        pre = ""
        name = "文档"
        url = "/categories/documentation/"
        title = ""
        weight = 4
      [[languages.zh-cn.menu.main]]
        identifier = "about"
        pre = ""
        post = ""
        name = "关于"
        url = "/about/"
        title = ""
        weight = 5
      [[languages.zh-cn.menu.main]]
        identifier = "github"
        pre = "<i class='fab fa-github fa-fw'></i>"
        post = ""
        name = ""
        url = "https://github.com/xxx"
        title = "GitHub"
        weight = 6
    [languages.zh-cn.params]
      # 网站描述
      description = "关于"
      # 网站关键词
      keywords = ["Theme", "Hugo"]
      # 应用图标配置
      [languages.zh-cn.params.app]
        # 当添加到 iOS 主屏幕或者 Android 启动器时的标题, 覆盖默认标题
        title = "xxx's Blog"
        # 是否隐藏网站图标资源链接
        noFavicon = false
        # 更现代的 SVG 网站图标, 可替代旧的 .png 和 .ico 文件
        svgFavicon = ""
        # Android 浏览器主题色
        themeColor = "#ffffff"
        # Safari 图标颜色
        iconColor = "#5bbad5"
        # Windows v8-10 磁贴颜色
        tileColor = "#da532c"
      # 搜索配置
      [languages.zh-cn.params.search]
        enable = true
        # 搜索引擎的类型 ("lunr", "algolia")
        type = "algolia"
        # 文章内容最长索引长度
        contentLength = 4000
        # 搜索框的占位提示语
        placeholder = ""
        # 最大结果数目
        maxResultLength = 10
        # 结果内容片段长度
        snippetLength = 50
        # 搜索结果中高亮部分的 HTML 标签
        highlightTag = "em"
        # 是否在搜索索引中使用基于 baseURL 的绝对路径
        absoluteURL = false
        [languages.zh-cn.params.search.algolia]
          index = "index.zh-cn"
          appID = "PASDMWALPK"
          searchKey = "b42948e51daaa93df92381c8e2ac0f93"
      # 主页信息设置
      [languages.zh-cn.params.home]
        # RSS 文章数目
        rss = 10
        # 主页个人信息
        [languages.zh-cn.params.home.profile]
          enable = true
          # Gravatar 邮箱，用于优先在主页显示的头像
          gravatarEmail = ""
          # 主页显示头像的 URL
          avatarURL = "/images/avatar.png"
          # 主页显示的网站标题 (支持 HTML 格式)
          title = ""
          # 主页显示的网站副标题
          subtitle = "记录美好,享受生活"
          # 是否为副标题显示打字机动画
          typeit = true
          # 是否显示社交账号
          social = true
          # 免责声明 (支持 HTML 格式)
          disclaimer = ""
        # 主页文章列表
        [languages.zh-cn.params.home.posts]
          enable = true
          # 主页每页显示文章数量
          paginate = 6
      # 主页的社交信息设置
      [languages.zh-cn.params.social]
        GitHub = "xxx"
        Weibo = "xxx"
        Zhihu = "xxxx"
        Douban = ""
        Googlescholar = ""
        Researchgate = ""
        Bilibili = "xxx"
        Email = "xxx"
        RSS = true

  [languages.fr]
    weight = 3
    # language code
    languageCode = "fr"
    # language name
    languageName = "Français"
    # whether to include Chinese/Japanese/Korean
    hasCJKLanguage = false
    # default amount of posts in each pages
    paginate = 12
    # [UA-XXXXXXXX-X] google analytics code
    googleAnalytics = ""
    # copyright description used only for seo schema
    copyright = "This work is licensed under a Creative Commons Attribution-NonCommercial 4.0 International License."
    # Menu config
    [languages.fr.menu]
      [[languages.fr.menu.main]]
        identifier = "posts"
        pre = ""
        post = ""
        name = "Postes"
        url = "/posts/"
        title = ""
        weight = 1
      [[languages.fr.menu.main]]
        identifier = "tags"
        pre = ""
        post = ""
        name = "Balises"
        url = "/tags/"
        title = ""
        weight = 2
      [[languages.fr.menu.main]]
        identifier = "categories"
        pre = ""
        post = ""
        name = "Catégories"
        url = "/categories/"
        title = ""
        weight = 3
      [[languages.fr.menu.main]]
        identifier = "documentation"
        pre = ""
        post = ""
        name = "Docs"
        url = "/categories/documentation/"
        title = ""
        weight = 4
      [[languages.fr.menu.main]]
        identifier = "about"
        pre = ""
        name = "À propos"
        url = "/about/"
        title = ""
        weight = 5
      [[languages.fr.menu.main]]
        identifier = "github"
        pre = "<i class='fab fa-github fa-fw'></i>"
        post = ""
        name = ""
        url = "https://github.com/xxx"
        
        title = "GitHub"
        weight = 6
    [languages.fr.params]
      # site description
      description = "À propos du thème LoveIt"
      # site keywords
      keywords = ["Thème", "Hugo"]
      # App icon config
      [languages.fr.params.app]
        # optional site title override for the app when added to an iOS home screen or Android launcher
        title = "xxx's Blog"
        # whether to omit favicon resource links
        noFavicon = false
        # modern SVG favicon to use in place of older style .png and .ico files
        svgFavicon = ""
        # Android browser theme color
        themeColor = "#ffffff"
        # Safari mask icon color
        iconColor = "#5bbad5"
        # Windows v8-10 tile color
        tileColor = "#da532c"
      # Search config
      [languages.fr.params.search]
        enable = true
        # type of search engine ("lunr", "algolia")
        type = "algolia"
        # max index length of the chunked content
        contentLength = 4000
        # placeholder of the search bar
        placeholder = ""
        # max number of results length
        maxResultLength = 10
        # snippet length of the result
        snippetLength = 30
        # HTML tag name of the highlight part in results
        highlightTag = "em"
        # whether to use the absolute URL based on the baseURL in search index
        absoluteURL = false
        [languages.fr.params.search.algolia]
          index = "index.fr"
          appID = "PASDMWALPK"
          searchKey = "b42948e51daaa93df92381c8e2ac0f93"
      # Home page config
      [languages.fr.params.home]
        # amount of RSS pages
        rss = 10
        # Home page profile
        [languages.fr.params.home.profile]
          enable = true
          # Gravatar Email for preferred avatar in home page
          gravatarEmail = ""
          # URL of avatar shown in home page
          avatarURL = "/images/avatar.png"
          # title shown in home page (HTML format is supported)
          title = ""
          # subtitle shown in home page
          subtitle = "Enregistrer les bonnes choses et profiter de la vie"
          # whether to use typeit animation for subtitle
          typeit = true
          # whether to show social links
          social = true
          # disclaimer (HTML format is supported)
          disclaimer = ""
        # Home page posts
        [languages.fr.params.home.posts]
          enable = true
          # special amount of posts in each home posts page
          paginate = 6
      # Social config in home page
      [languages.fr.params.social]
       GitHub = "xxx"
        Weibo = "xxx"
        Zhihu = "xxx"
        Douban = ""
        Googlescholar = ""
        Researchgate = ""
        Bilibili = "xxx"
        Email = "xxxx"
        RSS = true
[params]
  # LoveIt theme version
  # LoveIt 主题版本
  version = "0.2.X"
  # site default theme ("light", "dark", "auto")
  # 网站默认主题 ("light", "dark", "auto")
  defaultTheme = "auto"
  # public git repo url only then enableGitInfo is true
  # 公共 git 仓库路径，仅在 enableGitInfo 设为 true 时有效
  gitRepo = ""
  # which hash function used for SRI, when empty, no SRI is used ("sha256", "sha384", "sha512", "md5")
  # 哪种哈希函数用来 SRI, 为空时表示不使用 SRI ("sha256", "sha384", "sha512", "md5")
  fingerprint = ""
  # date format
  # 日期格式
  dateFormat = "2006-01-02"
  # website images for Open Graph and Twitter Cards
  # 网站图片, 用于 Open Graph 和 Twitter Cards
  images = ["/logo.png"]

  # Header config
  # 页面头部导航栏配置
  [params.header]
    # desktop header mode ("fixed", "normal", "auto")
    # 桌面端导航栏模式 ("fixed", "normal", "auto")
    desktopMode = "fixed"
    # mobile header mode ("fixed", "normal", "auto")
    # 移动端导航栏模式 ("fixed", "normal", "auto")
    mobileMode = "auto"
    # Header title config
    # 页面头部导航栏标题配置
    [params.header.title]
      # URL of the LOGO
      # LOGO 的 URL
      logo = ""
      # title name
      # 标题名称
      name = "xxx's Blog"
      # you can add extra information before the name (HTML format is supported), such as icons
      # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
      pre = "<i class='fas fa-heart fa-fw'></i>"
      # you can add extra information after the name (HTML format is supported), such as icons
      # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
      post = ""
      # whether to use typeit animation for title name
      # 是否为标题显示打字机动画
      typeit = false

[params.busuanzi]         # count web traffic by busuanzi                             # 是否使用不蒜子统计站点访问量
    enable = true
    siteUV = true
    sitePV = true
    pagePV = true

  [params.reward]                                         # 文章打赏
    enable = true
    wechat = "wechat,jpg"           # 微信二维码
    alipay = "alipay.jpg"    

  # Footer config
  # 页面底部信息配置
  [params.footer]
    enable = true
    # Custom content (HTML format is supported)
    # 自定义内容 (支持 HTML 格式)
    custom = ''
    # whether to show Hugo and theme info
    # 是否显示 Hugo 和主题信息
    hugo = true
    # whether to show copyright info
    # 是否显示版权信息
    copyright = true
    # whether to show the author
    # 是否显示作者
    author = true
    # site creation time
    # 网站创立年份
    since = 2019
    # ICP info only in China (HTML format is supported)
    # ICP 备案信息，仅在中国使用 (支持 HTML 格式)
    icp = ""
    # license info (HTML format is supported)
    # 许可协议信息 (支持 HTML 格式)
    license= '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'

  # Section (all posts) page config
  # Section (所有文章) 页面配置
  [params.section]
    # special amount of posts in each section page
    # section 页面每页显示文章数量
    paginate = 20
    # date format (month and day)
    # 日期格式 (月和日)
    dateFormat = "01-02"
    # amount of RSS pages
    # RSS 文章数目
    rss = 10

  # List (category or tag) page config
  # List (目录或标签) 页面配置
  [params.list]
    # special amount of posts in each list page
    # list 页面每页显示文章数量
    paginate = 20
    # date format (month and day)
    # 日期格式 (月和日)
    dateFormat = "01-02"
    # amount of RSS pages
    # RSS 文章数目
    rss = 10

  # Page config
  # 文章页面配置
  [params.page]
    # whether to hide a page from home page
    # 是否在主页隐藏一篇文章
    hiddenFromHomePage = false
    # whether to hide a page from search results
    # 是否在搜索结果中隐藏一篇文章
    hiddenFromSearch = false
    # whether to enable twemoji
    # 是否使用 twemoji
    twemoji = false
    # whether to enable lightgallery
    # 是否使用 lightgallery
    lightgallery = false
    # whether to enable the ruby extended syntax
    # 是否使用 ruby 扩展语法
    ruby = true
    # whether to enable the fraction extended syntax
    # 是否使用 fraction 扩展语法
    fraction = true
    # whether to enable the fontawesome extended syntax
    # 是否使用 fontawesome 扩展语法
    fontawesome = true
    # whether to show link to Raw Markdown content of the content
    # 是否显示原始 Markdown 文档内容的链接
    linkToMarkdown = true
    # whether to show the full text content in RSS
    # 是否在 RSS 中显示全文内容
    rssFullText = false
    # Table of the contents config
    # 目录配置
    [params.page.toc]
      # whether to enable the table of the contents
      # 是否使用目录
      enable = true
      # whether to keep the static table of the contents in front of the post
      # 是否保持使用文章前面的静态目录
      keepStatic = false
      # whether to make the table of the contents in the sidebar automatically collapsed
      # 是否使侧边目录自动折叠展开
      auto = true
    # Code config
    # 代码配置
    [params.page.code]
      # whether to show the copy button of the code block
      # 是否显示代码块的复制按钮
      copy = true
      # the maximum number of lines of displayed code by default
      # 默认展开显示的代码行数
      maxShownLines = 10
    # KaTeX mathematical formulas config (KaTeX https://katex.org/)
    # KaTeX 数学公式配置 (KaTeX https://katex.org/)
    [params.page.math]
      enable = false
      # default block delimiter is $$ ... $$ and \\[ ... \\]
      # 默认块定界符是 $$ ... $$ 和 \\[ ... \\]
      blockLeftDelimiter = ""
      blockRightDelimiter = ""
      # default inline delimiter is $ ... $ and \\( ... \\)
      # 默认行内定界符是 $ ... $ 和 \\( ... \\)
      inlineLeftDelimiter = ""
      inlineRightDelimiter = ""
      # KaTeX extension copy_tex
      # KaTeX 插件 copy_tex
      copyTex = true
      # KaTeX extension mhchem
      # KaTeX 插件 mhchem
      mhchem = true
    # Mapbox GL JS config (Mapbox GL JS https://docs.mapbox.com/mapbox-gl-js)
    # Mapbox GL JS 配置 (Mapbox GL JS https://docs.mapbox.com/mapbox-gl-js)
    [params.page.mapbox]
      # access token of Mapbox GL JS
      # Mapbox GL JS 的 access token
      accessToken = "pk.eyJ1IjoiZGlsbG9uenEiLCJhIjoiY2s2czd2M2x3MDA0NjNmcGxmcjVrZmc2cyJ9.aSjv2BNuZUfARvxRYjSVZQ"
      # style for the light theme
      # 浅色主题的地图样式
      lightStyle = "mapbox://styles/mapbox/light-v10?optimize=true"
      # style for the dark theme
      # 深色主题的地图样式
      darkStyle = "mapbox://styles/mapbox/dark-v10?optimize=true"
      # whether to add NavigationControl (https://docs.mapbox.com/mapbox-gl-js/api/#navigationcontrol)
      # 是否添加 NavigationControl (https://docs.mapbox.com/mapbox-gl-js/api/#navigationcontrol)
      navigation = true
      # whether to add GeolocateControl (https://docs.mapbox.com/mapbox-gl-js/api/#geolocatecontrol)
      # 是否添加 GeolocateControl (https://docs.mapbox.com/mapbox-gl-js/api/#geolocatecontrol)
      geolocate = true
      # whether to add ScaleControl (https://docs.mapbox.com/mapbox-gl-js/api/#scalecontrol)
      # 是否添加 ScaleControl (https://docs.mapbox.com/mapbox-gl-js/api/#scalecontrol)
      scale = true
      # whether to add FullscreenControl (https://docs.mapbox.com/mapbox-gl-js/api/#fullscreencontrol)
      # 是否添加 FullscreenControl (https://docs.mapbox.com/mapbox-gl-js/api/#fullscreencontrol)
      fullscreen = true
    # Social share links in post page
    # 文章页面的分享信息设置
    [params.page.share]
      enable = true
      Twitter = true
      Facebook = true
      Linkedin = false
      Whatsapp = false
      Pinterest = false
      Tumblr = false
      HackerNews = true
      Reddit = false
      VK = false
      Buffer = false
      Xing = false
      Line = true
      Instapaper = false
      Pocket = false
      Digg = false
      Stumbleupon = false
      Flipboard = false
      Weibo = true
      Renren = false
      Myspace = false
      Blogger = false
      Baidu = false
      Odnoklassniki = false
      Evernote = false
      Skype = false
      Trello = false
      Mix = false
    # Comment config
    # 评论系统设置
    [params.page.comment]
      enable = true
      # Disqus comment config (https://disqus.com/)
      # Disqus 评论系统设置 (https://disqus.com/)
      [params.page.comment.disqus]
        enable = false
        # Disqus shortname to use Disqus in posts
        # Disqus 的 shortname，用来在文章中启用 Disqus 评论系统
        shortname = ""
      # Gitalk comment config (https://github.com/gitalk/gitalk)
      # Gitalk 评论系统设置 (https://github.com/gitalk/gitalk)
      [params.page.comment.gitalk]
        enable = false
        owner = ""
        repo = ""
        clientId = ""
        clientSecret = ""
      # Valine comment config (https://github.com/xCss/Valine)
      # Valine 评论系统设置 (https://github.com/xCss/Valine)
      [params.page.comment.valine]
        enable = true
        appId = ""
        appKey = ""
        placeholder = "留一个友善的评论吧"
        avatar = "robohash"
        meta= ""
        pageSize = 10
        lang = ""
        visitor = true
        recordIP = true
        highlight = true
        enableQQ = false
        serverURLs = ""
        # emoji data file name, default is "google.yml"
        # ("apple.yml", "google.yml", "facebook.yml", "twitter.yml")
        # located in "themes/LoveIt/assets/data/emoji/" directory
        # you can store your own data files in the same path under your project:
        # "assets/data/emoji/"
        # emoji 数据文件名称, 默认是 "google.yml"
        # ("apple.yml", "google.yml", "facebook.yml", "twitter.yml")
        # 位于 "themes/LoveIt/assets/data/emoji/" 目录
        # 可以在你的项目下相同路径存放你自己的数据文件:
        # "assets/data/emoji/"
        emoji = ""
      # Facebook comment config (https://developers.facebook.com/docs/plugins/comments)
      # Facebook 评论系统设置 (https://developers.facebook.com/docs/plugins/comments)
      [params.page.comment.facebook]
        enable = false
        width = "100%"
        numPosts = 10
        appId = ""
        languageCode = ""
      # Telegram comments config (https://comments.app/)
      # Telegram comments 评论系统设置 (https://comments.app/)
      [params.page.comment.telegram]
        enable = false
        siteID = ""
        limit = 5
        height = ""
        color = ""
        colorful = true
        dislikes = false
        outlined = false
      # Commento comment config (https://commento.io/)
      # Commento comment 评论系统设置 (https://commento.io/)
      [params.page.comment.commento]
        enable = false
      # Utterances comment config (https://utteranc.es/)
      # Utterances comment 评论系统设置 (https://utteranc.es/)
      [params.page.comment.utterances]
        enable = false
        # owner/repo
        repo = ""
        issueTerm = "pathname"
        label = ""
        lightTheme = "github-light"
        darkTheme = "github-dark"
    # Third-party library config
    # 第三方库配置
    [params.page.library]
      [params.page.library.css]
        # someCSS = "some.css"
        # located in "assets/" 位于 "assets/"
        # Or 或者
        # someCSS = "https://cdn.example.com/some.css"
      [params.page.library.js]
        # someJavascript = "some.js"
        # located in "assets/" 位于 "assets/"
        # Or 或者
        # someJavascript = "https://cdn.example.com/some.js"
    # Page SEO config
    # 页面 SEO 配置
    [params.page.seo]
      # image URL
      # 图片 URL
      images = []
      # Publisher info
      # 出版者信息
      [params.page.seo.publisher]
        name = "xxxx"
        logoUrl = "/images/avatar.png"

  # TypeIt config
  # TypeIt 配置
  [params.typeit]
    # typing speed between each step (measured in milliseconds)
    # 每一步的打字速度 (单位是毫秒)
    speed = 100
    # blinking speed of the cursor (measured in milliseconds)
    # 光标的闪烁速度 (单位是毫秒)
    cursorSpeed = 1000
    # character used for the cursor (HTML format is supported)
    # 光标的字符 (支持 HTML 格式)
    cursorChar = "|"
    # cursor duration after typing finishing (measured in milliseconds, "-1" means unlimited)
    # 打字结束之后光标的持续时间 (单位是毫秒, "-1" 代表无限大)
    duration = -1

  # Site verification code for Google/Bing/Yandex/Pinterest/Baidu
  # 网站验证代码，用于 Google/Bing/Yandex/Pinterest/Baidu
  [params.verification]
    google = ""
    bing = ""
    yandex = ""
    pinterest = ""
    baidu = ""

  # Site SEO config
  # 网站 SEO 配置
  [params.seo]
    # image URL
    # 图片 URL
    # image = "/images/Apple-Devices-Preview.png"
    # thumbnail URL
    # 缩略图 URL
    # thumbnailUrl = "/images/screenshot.png"

  # Analytics config
  # 网站分析配置
  [params.analytics]
    enable = false
    # Google Analytics
    [params.analytics.google]
      id = ""
      # whether to anonymize IP
      # 是否匿名化用户 IP
      anonymizeIP = true
    # Fathom Analytics
    [params.analytics.fathom]
      id = ""
      # server url for your tracker if you're self hosting
      # 自行托管追踪器时的主机路径
      server = ""

  # Cookie consent config
  # Cookie 许可配置
  [params.cookieconsent]
    enable = false
    # text strings used for Cookie consent banner
    # 用于 Cookie 许可横幅的文本字符串
    [params.cookieconsent.content]
      message = ""
      dismiss = ""
      link = ""

  # CDN config for third-party library files
  # 第三方库文件的 CDN 设置
  [params.cdn]
    # CDN data file name, disabled by default
    # ("jsdelivr.yml")
    # located in "themes/LoveIt/assets/data/cdn/" directory
    # you can store your own data files in the same path under your project:
    # "assets/data/cdn/"
    # CDN 数据文件名称, 默认不启用
    # ("jsdelivr.yml")
    # 位于 "themes/LoveIt/assets/data/cdn/" 目录
    # 可以在你的项目下相同路径存放你自己的数据文件:
    # "assets/data/cdn/"
    data = "jsdelivr.yml"

  # Compatibility config
  # 兼容性设置
  [params.compatibility]
    # whether to use Polyfill.io to be compatible with older browsers
    # 是否使用 Polyfill.io 来兼容旧式浏览器
    polyfill = false
    # whether to use object-fit-images to be compatible with older browsers
    # 是否使用 object-fit-images 来兼容旧式浏览器
    objectFit = false

# Markup related configuration in Hugo
# Hugo 解析文档的配置
[markup]
  # Syntax Highlighting (https://gohugo.io/content-management/syntax-highlighting)
  # 语法高亮设置 (https://gohugo.io/content-management/syntax-highlighting)
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNos = true
    lineNumbersInTable = true
    # false is a necessary configuration (https://github.com/dillonzq/LoveIt/issues/158)
    # false 是必要的设置 (https://github.com/dillonzq/LoveIt/issues/158)
    noClasses = false
  # Goldmark is from Hugo 0.60 the default library used for Markdown
  # Goldmark 是 Hugo 0.60 以来的默认 Markdown 解析库
  [markup.goldmark]
    [markup.goldmark.extensions]
      definitionList = true
      footnote = true
      linkify = true
      strikethrough = true
      table = true
      taskList = true
      typographer = true
    [markup.goldmark.renderer]
      # whether to use HTML tags directly in the document
      # 是否在文档中直接使用 HTML 标签
      unsafe = true
  # Table Of Contents settings
  # 目录设置
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 6

# Author config
# 作者配置
[author]
  name = "xxx"
  email = "xxx"
  link = "xxx"

# Sitemap config
# 网站地图配置
[sitemap]
  changefreq = "weekly"
  filename = "sitemap.xml"
  priority = 0.5

# Permalinks config (https://gohugo.io/content-management/urls/#permalinks)
# Permalinks 配置 (https://gohugo.io/content-management/urls/#permalinks)
[Permalinks]
  # posts = ":year/:month/:filename"
  posts = ":filename"

# Privacy config (https://gohugo.io/about/hugo-and-gdpr/)
# 隐私信息配置 (https://gohugo.io/about/hugo-and-gdpr/)
[privacy]
  # privacy of the Google Analytics (replaced by params.analytics.google)
  # Google Analytics 相关隐私 (被 params.analytics.google 替代)
  [privacy.googleAnalytics]
    # ...
  [privacy.twitter]
    enableDNT = true
  [privacy.youtube]
    privacyEnhanced = true

# Options to make output .md files
# 用于输出 Markdown 格式文档的设置
[mediaTypes]
  [mediaTypes."text/plain"]
    suffixes = ["md"]

# Options to make output .md files
# 用于输出 Markdown 格式文档的设置
[outputFormats.MarkDown]
  mediaType = "text/plain"
  isPlainText = true
  isHTML = false

# Options to make hugo output files
# 用于 Hugo 输出文档的设置
[outputs]
  home = ["HTML", "RSS", "JSON"]
  page = ["HTML", "MarkDown"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML", "RSS"]
  taxonomyTerm = ["HTML"]


```

修改内容如下表：

|  ID   |     字段      |  行数   |           值           | 备注                                                                                                                                                                                                          |
| :---: | :-----------: | :-----: | :--------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|   1   |     title     |   14    |      你的博客名称      |                                                                                                                                                                                                               |
|   2   | enableGitInfo |   21    |         false          | 改成true就需要删除`myblog/content/posts/`下的某个md文件                                                                                                                                                       |
|   3   |    weight     |   28    |           2            | 表示在博客语言切换菜单子菜单位于第二位，修改为1表示位于第一位                                                                                                                                                 |
|   4   |      url      |   91    |     你的github链接     |                                                                                                                                                                                                               |
|   5   |     title     |   102   |      你的博客名称      |                                                                                                                                                                                                               |
|   6   |   avatarURL   |   144   |       avatar.png       | **注意**：`/images/avatar.png`是相对于`myblog/static/`的                                                                                                                                                      |
|   7   |    social     | 162-169 |      你的社交链接      | **注意**：<br/>1. 只用输入你的社交链接的后缀即可，例如https://github.com/lizilong1993只用填写`lizilong1993`.<br>2. 如果有其它社交链接需求，可以打开`Myblog\myblog\assets\data\social.yml`文件查找，用法简单。 |
|   8   |      url      |   235   |     你的github链接     |                                                                                                                                                                                                               |
|   9   |   avatarURL   |   288   |   你的avatar.png路径   |                                                                                                                                                                                                               |
|  10   |     title     |   290   |          名字          |                                                                                                                                                                                                               |
|  11   |   subtitle    |   292   |         副标题         |                                                                                                                                                                                                               |
|  12   |    social     | 306-313 |        个人信息        | 如果不够可以参考第7项修改                                                                                                                                                                                     |
|  13   |    weight     |   317   |           3            | 根据第1项对应修改                                                                                                                                                                                             |
|  14   |      url      |   376   |     你的github链接     |                                                                                                                                                                                                               |
|  15   |   subtitle    |   434   |         副标题         | 法语版副标题                                                                                                                                                                                                  |
|  16   |    social     | 448-455 |        个人信息        | 如果不够可以参考第7项修改                                                                                                                                                                                     |
|  17   |     name      |   494   |        博客标题        |                                                                                                                                                                                                               |
|  18   |               |   497   | 博客标题**前面**的图标 | [Font Awesome](https://fontawesome.cc/)图标                                                                                                                                                                   |
|  19   |               |   500   | 博客标题**后面**的图标 |                                                                                                                                                                                                               |
|  20   |    reward     | 513-514 |       你的收款码       |                                                                                                                                                                                                               |
|  21   |    footer     | 519-541 |     博客网站footer     | 根据注释，按需修改                                                                                                                                                                                            |
|  22   |     share     | 664-691 | 是否显示某站的分享链接 | 按需修改                                                                                                                                                                                                      |
|  23   |    comment    |         |    你的评论工具配置    | 国内建议用Valine，配置方法参考[Valine](https://valine.js.org/quickstart.html)。                                                                                                                               |
|  24   |    author     | 921-923 |        作者信息        |                                                                                                                                                                                                               |



## 5 自动化部署到Gitee{#auto_push}

### 5.1新建仓库

访问Gitee官网https://gitee.com/，注册并登录。



![image-20211103164357931](https://gitee.com/lizilong1993/image/raw/master/202111031643003.png)

点击`+`——>`新建仓库`，填写你的仓库名称。

![image-20211103164529099](https://gitee.com/lizilong1993/image/raw/master/202111031645158.png)

{{< admonition warning"注意" true>}}

此处`仓库名称`和`路径`要填写一致，这样最后你的个人博客网址就会是https://yourname.gitee.io，否则会变成https://gitee.com/yourname.io。

{{< /admonition >}}



### 5.2 生成个人令牌

点击个人头像，选择`设置`。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111031649314.png" alt="image-20211103164955263" style="zoom:50%;" />

点击左侧菜单栏的`私人令牌`——>`生成新令牌`。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111031650537.png" alt="image-20211103165031488" style="zoom:50%;" />

输入令牌描述，所有选项都选上。

![image-20211103165302483](https://gitee.com/lizilong1993/image/raw/master/202111031653557.png)

生成成功。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111031653732.png" alt="image-20211103165344683" style="zoom: 50%;" />

{{< admonition  warning  "注意" >}}
个人令牌请单独存起来，因为Gitee将不会明文显示你的个人令牌。

{{< /admonition >}} 



### 5.3 自动化部署

{{< admonition  warning "该方法已废弃"  true>}}

现已**废弃**该方法，采用**2021/11/8日修改内容**提到的方法。

{{< /admonition >}} 

新建一个文本文档，将如下内容写入。

```bash
::auto push code and posts to gitee


echo ====push code and posts to gitee====

echo start building
hugo

echo push code and posts to gitee remote branch code-hugo
git status
git add -u
git status
git commit -m "new posts"
git push  origin master:code-hugo
echo push the produced static blog website files to gitee remote branch master
cd ./public
git status
git add -u
git status
git commit -m "add posts"
git push  origin master

echo All work done!

pause
```

将文件后缀改为`*.bat`。每一行的意思可以看注释，大概流程是：

- 构建
- 将工程代码push到远程仓库code-hugo分支
- cd到 ./public文件夹
- 将生成的静态博客文件push到远程仓库master分支


{{< admonition  tip "2021/11/8修改"  true>}}
现已修改为同时提交public文件夹和整个工程文件到不同的两个仓库，这样更方便对源码和博客分别进行管理。

具体方式参考[使用Hugo在GitHub上搭建个人博客初步_kutawei的博客-CSDN博客](https://blog.csdn.net/kutawei/article/details/105421545)`第五步`。

1. 按照上述博文`第五步`进行操作
2. 新建`deploy_blog.sh`和`自动化部署.bat`两个文件
3. `deploy_blog.sh`内写入

```bash

#!/bin/sh
 
# If a command fails then the deploy stops
set -e
 
printf "\033[0;32mDeploying updates to Gitee...\033[0m\n"
 
# Build the project.
hugo -D # if using a theme, replace with `hugo -t <YOURTHEME>`
 
# Go To Public folder

 
# Add changes to git.
git add .
 
# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
    msg="$*"
fi
git commit -m "$msg"
 
# Push source and build repos.
git push origin master

```

4. `自动化部署.bat`写入内容

```bash
echo =====deploy to gitee====
"D:\Software\Git\bin\sh.exe"  --login -i -c "./deploy_public.sh"
"D:\Software\Git\bin\sh.exe"  --login -i -c "./deploy_hugo_blog.sh"
```

 `"D:\Software\Git\bin\sh.exe" `是你git bash的存放路径。

{{< /admonition >}} 

### 5.4 开启Gitee Pages服务

点击`仓库`--->`服务`--->`Gitee Pages`服务。

![image-20211103170421835](https://gitee.com/lizilong1993/image/raw/master/202111031704909.png)

{{< admonition  note "注意" >}}
每次更新后都需要来点一下更新部署按钮。

 <img src="https://gitee.com/lizilong1993/image/raw/master/202111031707525.png" alt="image-20211103170711480" style="zoom:50%;" />

{{< /admonition >}} 

## 6 完成{#done}

至此已经完成全部配置啦！:(far fa-laugh-beam):

觉得有帮助，麻烦顺手给我[点个Star](https://gitee.com/lizilong1993/lizilong1993)吧 or [Buy me a coffee](https://lizilong1993.gitee.io/about/)

## 参考资料{#ref}

- [使用Hugo在GitHub上搭建个人博客初步_kutawei的博客-CSDN博客](https://blog.csdn.net/kutawei/article/details/105421545)




