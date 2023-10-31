# 基于Hugo+LoveIt+Gitee搭建个人博客[详细版]




## 1.  简介{#abstract}



Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。
​       <!--more-->
该篇文章是在Linux/UOS系统下安装搭建 Hugo 博客,在Windows环境下基本一致。

## 2. 环境{#prepare}

- [hugo v.0.88.1](https://github.com/gohugoio/hugo/releases) 
- [Hugo Themes (gohugo.io)](https://themes.gohugo.io/)
- git v2.20.1

```bash
hugo version #查看是否正确安装
git --version #git安装最新的就好，版本没啥影响
```



## 3. 搭建过程{#installation}

###    3.1 选一个主题

我这里选中了LoveIt[LoveIt | Hugo Themes (gohugo.io)](https://themes.gohugo.io/themes/loveit/)，个人非常喜欢这种简单颜色分明的主题，并且可定制化。

这是官网效果：

![image-20211101210655241](https://gitee.com/lizilong1993/image/raw/master/202111012107402.png)

### 3.2 安装

#### 3.2.1 创建一个项目

```bash
hugo new site myblog  # myblog是你的项目名，叫啥都行
cd myblog
```

#### 3.2.2 安装主题

> 全文参考[LoveIt主题官方文档](https://hugoloveit.com/zh-cn/theme-documentation-basics/)。

**LoveIt** 主题的仓库是: https://github.com/dillonzq/LoveIt.

你可以下载主题的 [最新版本 .zip 文件](https://github.com/dillonzq/LoveIt/releases) 并且解压放到 `themes` 目录.另外, 也可以直接把这个主题克隆到 `themes` 目录:

```bash
git clone https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

或者, 初始化你的项目目录为 git 仓库, 并且把主题仓库作为你的网站目录的子模块:

```bash
git init
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

#### 3.2.3 主题配置

以下是 LoveIt 主题的基本配置:

```toml
baseURL = "http://example.org/"
# [en, zh-cn, fr, ...] 设置默认的语言
defaultContentLanguage = "zh-cn"
# 网站语言, 仅在这里 CN 大写
languageCode = "zh-CN"
# 是否包括中日韩文字
hasCJKLanguage = true
# 网站标题
title = "我的全新 Hugo 网站"

# 更改使用 Hugo 构建网站时使用的默认主题
theme = "LoveIt"

[params]
  # LoveIt 主题版本
  version = "0.2.X"

[menu]
  [[menu.main]]
    identifier = "posts"
    # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
    pre = ""
    # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
    post = ""
    name = "文章"
    url = "/posts/"
    # 当你将鼠标悬停在此菜单链接上时, 将显示的标题
    title = ""
    weight = 1
  [[menu.main]]
    identifier = "tags"
    pre = ""
    post = ""
    name = "标签"
    url = "/tags/"
    title = ""
    weight = 2
  [[menu.main]]
    identifier = "categories"
    pre = ""
    post = ""
    name = "分类"
    url = "/categories/"
    title = ""
    weight = 3

# Hugo 解析文档的配置
[markup]
  # 语法高亮设置 (https://gohugo.io/content-management/syntax-highlighting)
  [markup.highlight]
    # false 是必要的设置 (https://github.com/dillonzq/LoveIt/issues/158)
    noClasses = false

```

> **注意**：在构建网站时, 你可以使用 `--theme` 选项设置主题. 但是, 我建议你修改配置文件 (**config.toml**) 将本主题设置为默认主题.



#### 3.2.4 创建一篇文章

以下是创建第一篇文章的方法:

```bash
hugo new posts/test.md
```

这将会在/myblog/content/posts/ 路径下创建一个test.md。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111012145017.png" alt="image-20211101214507966" style="zoom: 80%;" />

让我们来看看这个test.md文件里的内容。

![image-20211101214751066](https://gitee.com/lizilong1993/image/raw/master/202111012147108.png)

> 默认情况下, 所有文章和页面均作为草稿创建. 如果想要渲染这些页面, 请从元数据中删除属性 `draft: true`, 设置属性 `draft: false` 或者为 `hugo` 命令添加 `-D`/`--buildDrafts` 参数.

#### 3.2.5 本地启动网站

​       使用以下命令启动网站:

```bash
hugo serve
```

去查看 `http://localhost:1313`.

![image-20211102102908470](https://gitee.com/lizilong1993/image/raw/master/202111021029602.png)



> 在hugo serve 状态下，当文件内容更改时, 页面会随着更改自动刷新.

> 由于本主题使用了 Hugo 中的 .Scratch 来实现一些特性, 非常建议你为 `hugo server `命令添加 ``--disableFastRender `参数来实时预览你正在编辑的文章页面.
>
> ```bash
> hugo serve --disableFastRender
> ```
>
> 

#### 3.2.6 构建网站

当你准备好部署你的网站时, 运行以下命令:

```bash
hugo
```

会生成一个 `public` 目录, 其中包含你网站的所有静态内容和资源. 现在可以将其部署在任何 Web 服务器上.

![image-20211102103352671](https://gitee.com/lizilong1993/image/raw/master/202111021033713.png)

> **技巧**
>
> 网站内容可以通过`Netlify `自动发布和托管 (了解有关[通过 Netlify 进行 HUGO 自动化部署 ](https://www.netlify.com/blog/2015/07/30/hosting-hugo-on-netlifyinsanely-fast-deploys/)的更多信息). 或者, 您可以使用 AWS Amplify, Github pages, Render 以及更多…

### 3.4. 配置

#### 3.4.1 网站配置

除了 [Hugo 全局配置](https://gohugo.io/overview/configuration/) 和 [菜单配置](https://hugoloveit.com/zh-cn/theme-documentation-basics/#basic-configuration) 之外, **LoveIt** 主题还允许您在网站配置中定义以下参数 (这是一个示例 `config.toml`, 其内容为默认值).

请打开下面的代码块查看完整的示例配置 :

```toml
[params]
  #  LoveIt 主题版本
  version = "0.2.X"
  # 网站描述
  description = "这是我的全新 Hugo 网站"
  # 网站关键词
  keywords = ["Theme", "Hugo"]
  # 网站默认主题样式 ("light", "dark", "auto")
  defaultTheme = "auto"
  # 公共 git 仓库路径，仅在 enableGitInfo 设为 true 时有效
  gitRepo = ""
  #  哪种哈希函数用来 SRI, 为空时表示不使用 SRI
  # ("sha256", "sha384", "sha512", "md5")
  fingerprint = ""
  #  日期格式
  dateFormat = "2006-01-02"
  # 网站图片, 用于 Open Graph 和 Twitter Cards
  images = ["/logo.png"]

  #  应用图标配置
  [params.app]
    # 当添加到 iOS 主屏幕或者 Android 启动器时的标题, 覆盖默认标题
    title = "LoveIt"
    # 是否隐藏网站图标资源链接
    noFavicon = false
    # 更现代的 SVG 网站图标, 可替代旧的 .png 和 .ico 文件
    svgFavicon = ""
    # Android 浏览器主题色
    themeColor = "#ffffff"
    # Safari 图标颜色
    iconColor = "#5bbad5"
    # Windows v8-10磁贴颜色
    tileColor = "#da532c"

  #  搜索配置
  [params.search]
    enable = true
    # 搜索引擎的类型 ("lunr", "algolia")
    type = "lunr"
    # 文章内容最长索引长度
    contentLength = 4000
    # 搜索框的占位提示语
    placeholder = ""
    #  最大结果数目
    maxResultLength = 10
    #  结果内容片段长度
    snippetLength = 50
    #  搜索结果中高亮部分的 HTML 标签
    highlightTag = "em"
    #  是否在搜索索引中使用基于 baseURL 的绝对路径
    absoluteURL = false
    [params.search.algolia]
      index = ""
      appID = ""
      searchKey = ""

  # 页面头部导航栏配置
  [params.header]
    # 桌面端导航栏模式 ("fixed", "normal", "auto")
    desktopMode = "fixed"
    # 移动端导航栏模式 ("fixed", "normal", "auto")
    mobileMode = "auto"
    #  页面头部导航栏标题配置
    [params.header.title]
      # LOGO 的 URL
      logo = ""
      # 标题名称
      name = ""
      # 你可以在名称 (允许 HTML 格式) 之前添加其他信息, 例如图标
      pre = ""
      # 你可以在名称 (允许 HTML 格式) 之后添加其他信息, 例如图标
      post = ""
      #  是否为标题显示打字机动画
      typeit = false

  # 页面底部信息配置
  [params.footer]
    enable = true
    #  自定义内容 (支持 HTML 格式)
    custom = ''
    #  是否显示 Hugo 和主题信息
    hugo = true
    #  是否显示版权信息
    copyright = true
    #  是否显示作者
    author = true
    # 网站创立年份
    since = 2019
    # ICP 备案信息，仅在中国使用 (支持 HTML 格式)
    icp = ""
    # 许可协议信息 (支持 HTML 格式)
    license = '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'

  #  Section (所有文章) 页面配置
  [params.section]
    # section 页面每页显示文章数量
    paginate = 20
    # 日期格式 (月和日)
    dateFormat = "01-02"
    # RSS 文章数目
    rss = 10

  #  List (目录或标签) 页面配置
  [params.list]
    # list 页面每页显示文章数量
    paginate = 20
    # 日期格式 (月和日)
    dateFormat = "01-02"
    # RSS 文章数目
    rss = 10

  # 主页配置
  [params.home]
    #  RSS 文章数目
    rss = 10
    # 主页个人信息
    [params.home.profile]
      enable = true
      # Gravatar 邮箱，用于优先在主页显示的头像
      gravatarEmail = ""
      # 主页显示头像的 URL
      avatarURL = "/images/avatar.png"
      #  主页显示的网站标题 (支持 HTML 格式)
      title = ""
      # 主页显示的网站副标题
      subtitle = "这是我的全新 Hugo 网站"
      # 是否为副标题显示打字机动画
      typeit = true
      # 是否显示社交账号
      social = true
      #  免责声明 (支持 HTML 格式)
      disclaimer = ""
    # 主页文章列表
    [params.home.posts]
      enable = true
      # 主页每页显示文章数量
      paginate = 6
      #  被 params.page 中的 hiddenFromHomePage 替代
      # 当你没有在文章前置参数中设置 "hiddenFromHomePage" 时的默认行为
      defaultHiddenFromHomePage = false

  # 作者的社交信息设置
  [params.social]
    GitHub = "xxxx"
    Linkedin = ""
    Twitter = "xxxx"
    Instagram = "xxxx"
    Facebook = "xxxx"
    Telegram = "xxxx"
    Medium = ""
    Gitlab = ""
    Youtubelegacy = ""
    Youtubecustom = ""
    Youtubechannel = ""
    Tumblr = ""
    Quora = ""
    Keybase = ""
    Pinterest = ""
    Reddit = ""
    Codepen = ""
    FreeCodeCamp = ""
    Bitbucket = ""
    Stackoverflow = ""
    Weibo = ""
    Odnoklassniki = ""
    VK = ""
    Flickr = ""
    Xing = ""
    Snapchat = ""
    Soundcloud = ""
    Spotify = ""
    Bandcamp = ""
    Paypal = ""
    Fivehundredpx = ""
    Mix = ""
    Goodreads = ""
    Lastfm = ""
    Foursquare = ""
    Hackernews = ""
    Kickstarter = ""
    Patreon = ""
    Steam = ""
    Twitch = ""
    Strava = ""
    Skype = ""
    Whatsapp = ""
    Zhihu = ""
    Douban = ""
    Angellist = ""
    Slidershare = ""
    Jsfiddle = ""
    Deviantart = ""
    Behance = ""
    Dribbble = ""
    Wordpress = ""
    Vine = ""
    Googlescholar = ""
    Researchgate = ""
    Mastodon = ""
    Thingiverse = ""
    Devto = ""
    Gitea = ""
    XMPP = ""
    Matrix = ""
    Bilibili = ""
    Email = "xxxx@xxxx.com"
    RSS = true # 

  #  文章页面配置
  [params.page]
    #  是否在主页隐藏一篇文章
    hiddenFromHomePage = false
    #  是否在搜索结果中隐藏一篇文章
    hiddenFromSearch = false
    #  是否使用 twemoji
    twemoji = false
    # 是否使用 lightgallery
    lightgallery = false
    #  是否使用 ruby 扩展语法
    ruby = true
    #  是否使用 fraction 扩展语法
    fraction = true
    #  是否使用 fontawesome 扩展语法
    fontawesome = true
    # 是否在文章页面显示原始 Markdown 文档链接
    linkToMarkdown = true
    #  是否在 RSS 中显示全文内容
    rssFullText = false
    #  目录配置
    [params.page.toc]
      # 是否使用目录
      enable = true
      #  是否保持使用文章前面的静态目录
      keepStatic = true
      # 是否使侧边目录自动折叠展开
      auto = true
    #  代码配置
    [params.page.code]
      # 是否显示代码块的复制按钮
      copy = true
      # 默认展开显示的代码行数
      maxShownLines = 10
    #  KaTeX 数学公式
    [params.page.math]
      enable = true
      # 默认块定界符是 $$ ... $$ 和 \\[ ... \\]
      blockLeftDelimiter = ""
      blockRightDelimiter = ""
      # 默认行内定界符是 $ ... $ 和 \\( ... \\)
      inlineLeftDelimiter = ""
      inlineRightDelimiter = ""
      # KaTeX 插件 copy_tex
      copyTex = true
      # KaTeX 插件 mhchem
      mhchem = true
    #  Mapbox GL JS 配置
    [params.page.mapbox]
      # Mapbox GL JS 的 access token
      accessToken = ""
      # 浅色主题的地图样式
      lightStyle = "mapbox://styles/mapbox/light-v9"
      # 深色主题的地图样式
      darkStyle = "mapbox://styles/mapbox/dark-v9"
      # 是否添加 NavigationControl
      navigation = true
      # 是否添加 GeolocateControl
      geolocate = true
      # 是否添加 ScaleControl
      scale = true
      # 是否添加 FullscreenControl
      fullscreen = true
    #  文章页面的分享信息设置
    [params.page.share]
      enable = true
      Twitter = true
      Facebook = true
      Linkedin = false
      Whatsapp = true
      Pinterest = false
      Tumblr = false
      HackerNews = false
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
      Myspace = true
      Blogger = true
      Baidu = false
      Odnoklassniki = false
      Evernote = true
      Skype = false
      Trello = false
      Mix = false
    #  评论系统设置
    [params.page.comment]
      enable = true
      # Disqus 评论系统设置
      [params.page.comment.disqus]
        # 
        enable = false
        # Disqus 的 shortname，用来在文章中启用 Disqus 评论系统
        shortname = ""
      # Gitalk 评论系统设置
      [params.page.comment.gitalk]
        # 
        enable = false
        owner = ""
        repo = ""
        clientId = ""
        clientSecret = ""
      # Valine 评论系统设置
      [params.page.comment.valine]
        enable = false
        appId = ""
        appKey = ""
        placeholder = ""
        avatar = "mp"
        meta= ""
        pageSize = 10
        lang = ""
        visitor = true
        recordIP = true
        highlight = true
        enableQQ = false
        serverURLs = ""
        #  emoji 数据文件名称, 默认是 "google.yml"
        # ("apple.yml", "google.yml", "facebook.yml", "twitter.yml")
        # 位于 "themes/LoveIt/assets/data/emoji/" 目录
        # 可以在你的项目下相同路径存放你自己的数据文件:
        # "assets/data/emoji/"
        emoji = ""
      # Facebook 评论系统设置
      [params.page.comment.facebook]
        enable = false
        width = "100%"
        numPosts = 10
        appId = ""
        languageCode = "zh_CN"
      #  Telegram Comments 评论系统设置
      [params.page.comment.telegram]
        enable = false
        siteID = ""
        limit = 5
        height = ""
        color = ""
        colorful = true
        dislikes = false
        outlined = false
      #  Commento 评论系统设置
      [params.page.comment.commento]
        enable = false
      #  Utterances 评论系统设置
      [params.page.comment.utterances]
        enable = false
        # owner/repo
        repo = ""
        issueTerm = "pathname"
        label = ""
        lightTheme = "github-light"
        darkTheme = "github-dark"
    #  第三方库配置
    [params.page.library]
      [params.page.library.css]
        # someCSS = "some.css"
        # 位于 "assets/"
        # 或者
        # someCSS = "https://cdn.example.com/some.css"
      [params.page.library.js]
        # someJavascript = "some.js"
        # 位于 "assets/"
        # 或者
        # someJavascript = "https://cdn.example.com/some.js"
    #  页面 SEO 配置
    [params.page.seo]
      # 图片 URL
      images = []
      # 出版者信息
      [params.page.seo.publisher]
        name = ""
        logoUrl = ""

  #  TypeIt 配置
  [params.typeit]
    # 每一步的打字速度 (单位是毫秒)
    speed = 100
    # 光标的闪烁速度 (单位是毫秒)
    cursorSpeed = 1000
    # 光标的字符 (支持 HTML 格式)
    cursorChar = "|"
    # 打字结束之后光标的持续时间 (单位是毫秒, "-1" 代表无限大)
    duration = -1

  # 网站验证代码，用于 Google/Bing/Yandex/Pinterest/Baidu
  [params.verification]
    google = ""
    bing = ""
    yandex = ""
    pinterest = ""
    baidu = ""

  #  网站 SEO 配置
  [params.seo]
    # 图片 URL
    image = ""
    # 缩略图 URL
    thumbnailUrl = ""

  #  网站分析配置
  [params.analytics]
    enable = false
    # Google Analytics
    [params.analytics.google]
      id = ""
      # 是否匿名化用户 IP
      anonymizeIP = true
    # Fathom Analytics
    [params.analytics.fathom]
      id = ""
      # 自行托管追踪器时的主机路径
      server = ""

  #  Cookie 许可配置
  [params.cookieconsent]
    enable = true
    # 用于 Cookie 许可横幅的文本字符串
    [params.cookieconsent.content]
      message = ""
      dismiss = ""
      link = ""

  #  第三方库文件的 CDN 设置
  [params.cdn]
    # CDN 数据文件名称, 默认不启用
    # ("jsdelivr.yml")
    # 位于 "themes/LoveIt/assets/data/cdn/" 目录
    # 可以在你的项目下相同路径存放你自己的数据文件:
    # "assets/data/cdn/"
    data = ""

  #  兼容性设置
  [params.compatibility]
    # 是否使用 Polyfill.io 来兼容旧式浏览器
    polyfill = false
    # 是否使用 object-fit-images 来兼容旧式浏览器
    objectFit = false

# Hugo 解析文档的配置
[markup]
  # 语法高亮设置
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNos = true
    lineNumbersInTable = true
    # false 是必要的设置
    # (https://github.com/dillonzq/LoveIt/issues/158)
    noClasses = false
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
      # 是否在文档中直接使用 HTML 标签
      unsafe = true
  # 目录设置
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 6

# 作者配置
[author]
  name = "xxxx"
  email = ""
  link = ""

# 网站地图配置
[sitemap]
  changefreq = "weekly"
  filename = "sitemap.xml"
  priority = 0.5

# Permalinks 配置
[Permalinks]
  # posts = ":year/:month/:filename"
  posts = ":filename"

# 隐私信息配置
[privacy]
  #  Google Analytics 相关隐私 (被 params.analytics.google 替代)
  [privacy.googleAnalytics]
    # ...
  [privacy.twitter]
    enableDNT = true
  [privacy.youtube]
    privacyEnhanced = true

# 用于输出 Markdown 格式文档的设置
[mediaTypes]
  [mediaTypes."text/plain"]
    suffixes = ["md"]

# 用于输出 Markdown 格式文档的设置
[outputFormats.MarkDown]
  mediaType = "text/plain"
  isPlainText = true
  isHTML = false

# 用于 Hugo 输出文档的设置
[outputs]
  # 
  home = ["HTML", "RSS", "JSON"]
  page = ["HTML", "MarkDown"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML", "RSS"]
  taxonomyTerm = ["HTML"]

```

> 请注意, 本文档其他部分将详细解释其中一些参数.

#### 3.4.2 Hugo的运行环境

`hugo serve` 的默认运行环境是 `development`, 而 `hugo` 的默认运行环境是 `production`.

由于本地 `development` 环境的限制, **评论系统**, **CDN** 和 **fingerprint** 不会在 `development` 环境下启用.

你可以使用 `hugo serve -e production` 命令来开启这些特性.

#### 3.4.3 CND配置技巧

```toml
[params.cdn]
  # CDN 数据文件名称, 默认不启用
  # ("jsdelivr.yml")
  data = ""

```

> 默认的 CDN 数据文件位于 `themes/LoveIt/assets/data/cdn/` 目录. 可以在你的项目下相同路径存放你自己的数据文件: `assets/data/cdn/`.

#### 3.4.4 关于社交链接配置的技巧

你可以直接配置你的社交 ID 来生成一个默认社交链接和图标:

```toml
[params.social]
  Mastodon = "@xxxx"

```

生成的社交链接是 `https://mastodon.technology/@xxxx`.

或者你可以通过一个字典来设置更多的选项:

```toml
[params.social]
  [params.social.Mastodon]
    # 排列图标时的权重 (权重越大, 图标的位置越靠后)
    weight = 0
    # 你的社交 ID
    id = "@xxxx"
    # 你的社交链接的前缀
    prefix = "https://mastodon.social/"
    # 当鼠标停留在图标上时的提示内容
    title = "Mastodon"

```

所有支持的社交链接的默认数据位于 `themes/LoveIt/assets/data/social.yaml`. 你可以参考它来配置你的社交链接.

![image-20211102134637992](https://gitee.com/lizilong1993/image/raw/master/202111021346090.png)

#### 3.4.5 网站图标, 浏览器配置, 网站清单

强烈建议你把:

- apple-touch-icon.png (180x180)
- favicon-32x32.png (32x32)
- favicon-16x16.png (16x16)
- mstile-150x150.png (150x150)
- android-chrome-192x192.png (192x192)
- android-chrome-512x512.png (512x512)

放在 `/static` 目录. 利用 https://realfavicongenerator.net/ 可以很容易地生成这些文件.

可以自定义 `browserconfig.xml` 和 `site.webmanifest` 文件来设置 theme-color 和 background-color.

#### 3.4.6 自定义样式

> Hugo **extended** 版本对于自定义样式是必需的.

通过定义自定义 `.scss` 样式文件, **LoveIt** 主题支持可配置的样式.

包含自定义 `.scss` 样式文件的目录相对于 **你的项目根目录** 的路径为 `assets/css`.

在 `assets/css/_override.scss` 中, 你可以覆盖 `themes/LoveIt/assets/css/_variables.scss` 中的变量以自定义样式.

这是一个例子:

```scss
@import url('https://fonts.googleapis.com/css?family=Fira+Mono:400,700&display=swap&subset=latin-ext');
$code-font-family: Fira Mono, Source Code Pro, Menlo, Consolas, Monaco, monospace;

```

在 `assets/css/_custom.scss` 中, 你可以添加一些 CSS 样式代码以自定义样式.

### 3.5. 多语言和 i18n{#multilanguage}

**LoveIt** 主题完全兼容 Hugo 的多语言模式, 并且支持在网页上切换语言.

![language-switch.gif (770×226) (hugoloveit.com)](https://gitee.com/lizilong1993/image/raw/master/202111021353959.gif)

#### 3.5.1 兼容性

![image-20211102135224621](https://gitee.com/lizilong1993/image/raw/master/202111021352693.png)

#### 3.5.2 基本配置

学习了 [Hugo如何处理多语言网站](https://gohugo.io/content-management/multilingual) 之后, 请在 [站点配置](https://hugoloveit.com/zh-cn/theme-documentation-basics/#site-configuration) 中定义你的网站语言.

例如, 一个支持英语, 中文和法语的网站配置:

```toml
# [en, zh-cn, fr, pl, ...] 设置默认的语言
defaultContentLanguage = "zh-cn"

[languages]
  [languages.en]
    weight = 1
    title = "My New Hugo Site"
    languageCode = "en"
    languageName = "English"
    [[languages.en.menu.main]]
      identifier = "posts"
      pre = ""
      post = ""
      name = "Posts"
      url = "/posts/"
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

  [languages.zh-cn]
    weight = 2
    title = "我的全新 Hugo 网站"
    # 网站语言, 仅在这里 CN 大写
    languageCode = "zh-CN"
    languageName = "简体中文"
    # 是否包括中日韩文字
    hasCJKLanguage = true
    [[languages.zh-cn.menu.main]]
      identifier = "posts"
      pre = ""
      post = ""
      name = "文章"
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

  [languages.fr]
    weight = 3
    title = "Mon nouveau site Hugo"
    languageCode = "fr"
    languageName = "Français"
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

```

然后, 对于每个新页面, 将语言代码附加到文件名中.

单个文件 `my-page.md` 需要分为三个文件:

- 英语: `my-page.en.md`
- 中文: `my-page.zh-cn.md`
- 法语: `my-page.fr.md`

> 请注意, 菜单中仅显示翻译的页面. 它不会替换为默认语言内容.

> Tips: 也可以使用 [文章前置参数](https://gohugo.io/content-management/multilingual#translate-your-content) 来翻译网址.
>

#### 3.5.3 修改默认的翻译字符串

翻译字符串用于在主题中使用的常见默认值. 目前提供[一些语言](https://hugoloveit.com/zh-cn/theme-documentation-basics/#language-compatibility)的翻译, 但你可能自定义其他语言或覆盖默认值.

要覆盖默认值, 请在你项目的 i18n 目录 `i18n/<languageCode>.toml` 中创建一个新文件，并从 `themes/LoveIt/i18n/en.toml` 中获得提示.

另外, 由于你的翻译可能会帮助到其他人, 请花点时间通过 [ 创建一个 PR](https://github.com/dillonzq/LoveIt/pulls) 来贡献主题翻译, 谢谢!

### 3.6. 搜索{#search}

基于 [Lunr.js](https://lunrjs.com/) 或 [algolia](https://www.algolia.com/), **LoveIt** 主题支持搜索功能.

#### 3.6.1 输出配置

为了生成搜索功能所需要的 `index.json`, 请在你的 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics/#site-configuration) 中添加 `JSON` 输出文件类型到 `outputs` 部分的 `home` 字段中.

```toml
[outputs]
  home = ["HTML", "RSS", "JSON"]

```

#### 3.6.2 搜索配置

基于 Hugo 生成的 `index.json` 文件, 你可以激活搜索功能.

这是你的 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics/#site-configuration) 中的搜索部分:

```toml
[params.search]
  enable = true
  # 搜索引擎的类型 ("lunr", "algolia")
  type = "lunr"
  # 文章内容最长索引长度
  contentLength = 4000
  # 搜索框的占位提示语
  placeholder = ""
  #  最大结果数目
  maxResultLength = 10
  #  结果内容片段长度
  snippetLength = 50
  #  搜索结果中高亮部分的 HTML 标签
  highlightTag = "em"
  #  是否在搜索索引中使用基于 baseURL 的绝对路径
  absoluteURL = false
  [params.search.algolia]
    index = ""
    appID = ""
    searchKey = ""

```

> **怎样选择搜索引擎?**   
>
>  以下是两种搜索引擎的对比:
>
> - `lunr`: 简单, 无需同步 `index.json`, 没有 `contentLength` 的限制, 但占用带宽大且性能低 (特别是中文需要一个较大的分词依赖库)
> - `algolia`: 高性能并且占用带宽低, 但需要同步 `index.json` 且有 `contentLength` 的限制
>
> 文章内容被 `h2` 和 `h3` HTML 标签切分来提高查询效果并且基本实现全文搜索. `contentLength` 用来限制 `h2` 和 `h3` HTML 标签开头的内容部分的最大长度.

> **关于 algolia 的使用技巧**
>
> 你需要上传 `index.json` 到 algolia 来激活搜索功能. 你可以使用浏览器来上传 `index.json` 文件但是一个自动化的脚本可能效果更好. [Algolia Atomic](https://github.com/chrisdmacrae/atomic-algolia) 是一个不错的选择. 为了兼容 Hugo 的多语言模式, 你需要上传不同语言的 `index.json` 文件到对应的 algolia index, 例如 `zh-cn/index.json` 或 `fr/index.json`…

## 4 页面组织{#page}

### 4.1 内容组织

以下是一些方便你清晰管理和生成文章的目录结构建议:

- 保持博客文章存放在 `content/posts` 目录, 例如: `content/posts/我的第一篇文章.md`
- 保持简单的静态页面存放在 `content` 目录, 例如: `content/about.md`
- 本地资源组织

> **本地资源引用**
>
> 有三种方法来引用**图片**和**音乐**等本地资源:
>
> 1. 使用[页面包](https://gohugo.io/content-management/page-bundles/)中的[页面资源](https://gohugo.io/content-management/page-resources/). 你可以使用适用于 `Resources.GetMatch` 的值或者直接使用相对于当前页面目录的文件路径来引用页面资源.
> 2. 将本地资源放在 **assets** 目录中, 默认路径是 `/assets`. 引用资源的文件路径是相对于 assets 目录的.
> 3. 将本地资源放在 **static** 目录中, 默认路径是 `/static`. 引用资源的文件路径是相对于 static 目录的.
>
> 引用的**优先级**符合以上的顺序.
>
> 在这个主题中的很多地方可以使用上面的本地资源引用, 例如 **链接**, **图片**, `image` shortcode, `music` shortcode 和**前置参数**中的部分参数.
>
> 页面资源或者 **assets** 目录中的[图片处理](https://gohugo.io/content-management/image-processing/)会在未来的版本中得到支持. 非常酷的功能! 😄

### 4.2 前置参数

**Hugo** 允许你在文章内容前面添加 `yaml`, `toml` 或者 `json` 格式的前置参数.

> **注意**
>
> **不是所有**的以下前置参数都必须在你的每篇文章中设置. 只有在文章的参数和你的 [网站设置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `page` 部分不一致时才有必要这么做.

这是一个前置参数例子:

```yaml
---
title: "我的第一篇文章"
subtitle: ""
date: 2020-03-04T15:58:26+08:00
lastmod: 2020-03-04T15:58:26+08:00
draft: true
author: ""
authorLink: ""
description: ""
license: ""
images: []

tags: []
categories: []
featuredImage: ""
featuredImagePreview: ""

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: true
ruby: true
fraction: true
fontawesome: true
linkToMarkdown: true
rssFullText: false

toc:
  enable: true
  auto: true
code:
  copy: true
  # ...
math:
  enable: true
  # ...
mapbox:
  accessToken: ""
  # ...
share:
  enable: true
  # ...
comment:
  enable: true
  # ...
library:
  css:
    # someCSS = "some.css"
    # 位于 "assets/"
    # 或者
    # someCSS = "https://cdn.example.com/some.css"
  js:
    # someJS = "some.js"
    # 位于 "assets/"
    # 或者
    # someJS = "https://cdn.example.com/some.js"
seo:
  images: []
  # ...
---

```



- **title**: 文章标题.
- **subtitle**:文章副标题.
- **date**: 这篇文章创建的日期时间. 它通常是从文章的前置参数中的 `date` 字段获取的, 但是也可以在 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中设置.
- **lastmod**: 上次修改内容的日期时间.
- **draft**: 如果设为 `true`, 除非 `hugo` 命令使用了 `--buildDrafts`/`-D` 参数, 这篇文章不会被渲染.
- **author**: 文章作者.
- **authorLink**: 文章作者的链接.
- **description**: 文章内容的描述.
- **license**: 这篇文章特殊的许可.
- **images**: 页面图片, 用于 Open Graph 和 Twitter Cards.
- **tags**: 文章的标签.
- **categories**: 文章所属的类别.
- **featuredImage**: 文章的特色图片.
- **featuredImagePreview**: 用在主页预览的文章特色图片.
- **hiddenFromHomePage**: 如果设为 `true`, 这篇文章将不会显示在主页上.
- **hiddenFromSearch**: 如果设为 `true`, 这篇文章将不会显示在搜索结果中.
- **twemoji**:如果设为 `true`, 这篇文章会使用 twemoji.
- **lightgallery**: 如果设为 `true`, 文章中的图片将可以按照画廊形式呈现.
- **ruby**: 如果设为 `true`, 这篇文章会使用 [上标注释扩展语法](https://hugoloveit.com/zh-cn/theme-documentation-content/#ruby).
- **fraction**:如果设为 `true`, 这篇文章会使用 [分数扩展语法](https://hugoloveit.com/zh-cn/theme-documentation-content/#fraction).
- **fontawesome**: 如果设为 `true`, 这篇文章会使用 [Font Awesome 扩展语法](https://hugoloveit.com/zh-cn/theme-documentation-content/#fontawesome).
- **linkToMarkdown**: 如果设为 `true`, 内容的页脚将显示指向原始 Markdown 文件的链接.
- **rssFullText**:如果设为 `true`, 在 RSS 中将会显示全文内容.
- **toc**: 和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.toc` 部分相同.
- **code**:[网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.code` 部分相同.
- **math**:https://github.com/dillonzq/LoveIt/releases/tag/v0.2.0) 和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.math` 部分相同.
- **mapbox**:和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.mapbox` 部分相同.
- **share**: 和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.share` 部分相同.
- **comment**: 和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.comment` 部分相同.
- **library**: 和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.library` 部分相同.
- **seo**:和 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中的 `params.page.seo` 部分相同.

> **技巧**
>
> **featuredImage** 和 **featuredImagePreview** 支持[本地资源引用](https://hugoloveit.com/zh-cn/theme-documentation-content/#contents-organization)的完整用法.
>
> 如果带有在前置参数中设置了 `name: featured-image` 或 `name: featured-image-preview` 属性的页面资源, 没有必要在设置 `featuredImage` 或 `featuredImagePreview`:
>
> ```yaml
> resources:
> - name: featured-image
>   src: featured-image.jpg
> - name: featured-image-preview
>   src: featured-image-preview.jpg
> ```

### 4.3 内容摘要

**LoveIt** 主题使用内容摘要在主页中显示大致文章信息。Hugo 支持生成文章的摘要.

![/zh-cn/theme-documentation-content/summary.zh-cn.png](https://gitee.com/lizilong1993/image/raw/master/202111021435473.png)

#### 4.3.1 自动摘要拆分

默认情况下, Hugo 自动将内容的前 70 个单词作为摘要.

你可以通过在 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中设置 `summaryLength` 来自定义摘要长度.

如果您要使用 **CJK中文/日语/韩语** 语言创建内容, 并且想使用 Hugo 的自动摘要拆分功能，请在 [网站配置](https://hugoloveit.com/zh-cn/theme-documentation-basics#site-configuration) 中将 `hasCJKLanguage` 设置为 `true`.

#### 4.3.2 手动摘要拆分

另外, 你也可以添加 `<!--more-->` 摘要分割符来拆分文章生成摘要.

摘要分隔符之前的内容将用作该文章的摘要.

> **注意**
>
> 请小心输入`<!--more-->` ; 即全部为小写且没有空格.

#### 4.3.3 前置参数摘要

你可能希望摘要不是文章开头的文字. 在这种情况下, 你可以在文章前置参数的 `summary` 变量中设置单独的摘要.

#### 4.3.4 使用文章描述作为摘要

你可能希望将文章前置参数中的 `description` 变量的内容作为摘要.

你仍然需要在文章开头添加 `<!--more-->` 摘要分割符. 将摘要分隔符之前的内容保留为空. 然后 **LoveIt** 主题会将你的文章描述作为摘要.

#### 4.3.5 摘要选择的优先级顺序

由于可以通过多种方式指定摘要, 因此了解顺序很有用. 如下:

1. 如果文章中有 `<!--more-->` 摘要分隔符, 但分隔符之前没有内容, 则使用描述作为摘要.
2. 如果文章中有 `<!--more-->` 摘要分隔符, 则将按照手动摘要拆分的方法获得摘要.
3. 如果文章前置参数中有摘要变量, 那么将以该值作为摘要.
4. 按照自动摘要拆分方法.

> **注意**
>
> 不建议在摘要内容中包含富文本块元素, 这会导致渲染错误. 例如代码块, 图片, 表格等.
>

## 5. 支持的功能{#function}

### 5.1 Markdown基本语法

这部分内容将在[Markdown基本语法]()中介绍。

### 5.2 Markdown扩展语法

这部分内容将在[Markdown扩展语法]()中介绍。

### 5.3 Emoji支持

这部分内容将在[Emoji支持]()中介绍。

### 5.4 数学公式

这部分内容将在[数学公式]()中介绍。

### 5.5 字符注音或者注释

**LoveIt** 主题支持一种 **字符注音或者注释** Markdown 扩展语法:

```markdown
[Hugo]^(一个开源的静态网站生成工具)

```

呈现的输出效果如下:

![image-20211102144803277](https://gitee.com/lizilong1993/image/raw/master/202111021448338.png)

### 5.6 分数

**LoveIt** 主题支持一种 **分数** Markdown 扩展语法:

```markdown
[浅色]/[深色]

[99]/[100]

```

呈现的输出效果如下:

![image-20211102144911965](https://gitee.com/lizilong1993/image/raw/master/202111021449024.png)

### 5.7 Font Awesome

**LoveIt** 主题使用 [Font Awesome](https://fontawesome.com/) 作为图标库. 你同样可以在文章中轻松使用这些图标.

从 [Font Awesome 网站](https://fontawesome.com/icons?d=gallery) 上获取所需的图标 `class`.

```markdown
去露营啦! :(fas fa-campground fa-fw): 很快就回来.

真开心! :(far fa-grin-tears):
```

![image-20211102145139315](https://gitee.com/lizilong1993/image/raw/master/202111021451377.png)

### 5.8 转义字符

在某些特殊情况下 (编写这个主题文档时 ), 你的文章内容会与 Markdown 的基本或者扩展语法冲突, 并且无法避免.

转义字符语法可以帮助你渲染出想要的内容:

```markdown
{?X} -> X
```

例如, 两个 `:` 会启用 emoji 语法. 但有时候这不是你想要的结果. 可以像这样使用转义字符语法:

```markdown
{?:}joy:
```

呈现的输出效果如下:

**:joy：**而不是 **😂**

> **技巧**
>
> 这个方法可以间接解决一个还未解决的 **[Hugo 的 issue](https://github.com/gohugoio/hugo/issues/4978)**.

另一个例子是:

```markdown
[link{?]}(#escape-character)
```

呈现的输出效果如下:

<img src="https://gitee.com/lizilong1993/image/raw/master/202111021456696.png" alt="image-20211102145603632" style="zoom: 67%;" />而不是 **[link](https://hugoloveit.com/zh-cn/theme-documentation-content/#escape-character)**.





## 6 自动化部署到Gitee{#auto_push}

### 6.1新建仓库

访问Gitee官网https://gitee.com/，注册并登录。



![image-20211103164357931](https://gitee.com/lizilong1993/image/raw/master/202111031728623.png)

点击`+`——>`新建仓库`，填写你的仓库名称。

![image-20211103164529099](https://gitee.com/lizilong1993/image/raw/master/202111031728537.png)

{{< admonition warning"注意" true>}}

此处`仓库名称`和`路径`要填写一致，这样最后你的个人博客网址就会是https://yourname.gitee.io，否则会变成https://gitee.com/yourname.io。

{{< /admonition >}}



### 6.2 生成个人令牌

点击个人头像，选择`设置`。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111031649314.png" alt="image-20211103164955263" style="zoom:50%;" />

点击左侧菜单栏的`私人令牌`——>`生成新令牌`。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111031650537.png" alt="image-20211103165031488" style="zoom:50%;" />

输入令牌描述，所有选项都选上。

![image-20211103165302483](https://gitee.com/lizilong1993/image/raw/master/202111031728644.png)

生成成功。

<img src="https://gitee.com/lizilong1993/image/raw/master/202111031653732.png" alt="image-20211103165344683" style="zoom: 50%;" />

{{< admonition  warning  "注意" >}}
个人令牌请单独存起来，因为Gitee将不会明文显示你的个人令牌。

{{< /admonition >}} 



### 6.3 自动化部署

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
  
  现已**修改**为同时提交public文件夹和整个工程文件到不同的两个仓库，这样更方便对源码和博客分别进行管理。
  
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

### 6.4 开启Gitee Pages服务

点击`仓库`--->`服务`--->`Gitee Pages`服务。

![image-20211103170421835](https://gitee.com/lizilong1993/image/raw/master/202111031728384.png)

{{< admonition  note "注意" >}}
每次更新后都需要来点一下更新部署按钮。

 <img src="https://gitee.com/lizilong1993/image/raw/master/202111031728283.png" alt="image-20211103170711480" style="zoom:50%;" />

{{< /admonition >}} 

## 7 完成{#done}

至此已经完成全部配置啦！:(far fa-laugh-beam):

觉得有帮助，麻烦顺手给我[点个Star](https://gitee.com/lizilong1993/lizilong1993)吧 or [Buy me a coffee](https://lizilong1993.gitee.io/about/)

## 参考资料



- [Hexo还是Hugo？Typecho还是Wordpress？读完这篇或许你就有答案了！ - 二十五画生 (laoda.de)](https://blog.laoda.de/archives/blog-choosing)
- [在Linux系统搭建Hugo博客_WuJvya的博客-CSDN博客](https://blog.csdn.net/qq_42185895/article/details/113780415)
- [LoveIt主题安装 (hugoloveit.com)](https://hugoloveit.com/zh-cn/theme-documentation-basics/)
- [Font Awsome](https://fontawesome.cc/)
- [Valine](https://valine.js.org/quickstart.html)


