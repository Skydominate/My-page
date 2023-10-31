# Latex 导言区


***论文写作中一些宏包的使用介绍***

<!--more-->

## 宏包简介

宏包是用来扩展/增强 $\LaTeX$ 的功能，宏包与 $\LaTeX$ 的关系和浏览器插件与浏览器的关系类似，通过安装不同的宏包可以实现一些复杂排版功能，例如插入复杂的列表表格、插入公式和特殊符号、插入代码、设置文档版式等。

| 宏包名 | 说明 |
| :-: | :-: |
| adjustbox | 实现对齐 |
| algorithm | 算法环境宏包 |
| amsfonts | AMS 扩展符号的基础字体支持 |
| amsmath | AMS数学公式扩展 |
| amssymb | 在 amsfonts 基础上将 AMS 扩展符号定义成命令 |
| amsthm | 对定理的排版 |
| arydshln | 支持排版虚线表格线 |
| comment | 提供了一个注释环境 |
| enumitem | 对枚举类型 enumerate 进行缩进 |
| epstopdf | pdflatex 命令下支持 EPS 格式的矢量图 |
| float | 为浮动体提供不浮动的 H 模式；提供自定义浮动体结构的功能 |
| framed |  |
| graphicx | 支持插图 |
| hyperref | 生成 PDF 并按照文档编码产生书签 |
| mathrsfs | 花体字母 'mathscr' 宏包 |
| mathtools | 数学公式扩展宏包，提供了公式编号定制和更多的符号、矩阵等 |
| multicol | 提供将内容自由分栏的 multicols 环境 |
| multirow | 支持合并多行单元格 |
| ragged2e | 协助 $\LaTeX$ 断词，尽可能地使排版比较整齐 |
| setspace | 行距 |
| subfig | 提供子图表和子标题的排版。类似宏包有 subfigure 和 subcaption 等 |
| textcomp | 生成特殊的符号，例如 $^{\circ}$C 可以写为 '\textcelsius' |
| threeparttable | 该宏包可以在表格之后增加表格注释，解决了为表格标题或表格参数做注释的问题 |
| tikz | 绘图宏包 |

## 格式设置：

```latex
\beamertemplateballitem                     %使itemize环境中的变成小球，这是一种视觉效果
\setbeamertemplate{theorems}[numbered]      %定理编号
\setbeamertemplate{caption}[numbered]       %图和表格的标题显示编号
\setbeamertemplate{navigation symbols}{}    %取消导航条
\setbeamerfont{frametitle}{size=\large}     %设置 Beamer 页标题字体
```

## 在 Beamer 中添加参考文献

使用脚注的形式给幻灯片某页添加参考文献:

在 `\begin{document}` 前添加如下命令
```latex
\usepackage[backend=bibtex,sorting=none]{biblatex}
\addbibresource{ref.bib}
\setbeamerfont{footnote}{size=\tiny}
```

在文中引用使用
```latex
\footfullcite{bib_item}         %文献item
```

___

> 具体的有关 $\LaTeX$ 的资源可以参考网站 [$\LaTeX$编辑部](https://www.latexstudio.net/hulatex/index.htm)
