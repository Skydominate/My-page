# 多文件 Latex 项目


***多项目论文latex写作技巧***

<!--more-->

LaTeX 有两个包可以支持在多项目文件中进行单文件编译
- `subfiles`：可以单独编译每个子文件，每个子文件都会用到主文档的 preamble
- `standalone` 每一个子文件类似于一个单独的文件，它们可以在之后合并到主文档里，它们各自的 preamble 也会纳入到主文档中。当你需要在多个文档中重复使用一个文件的时候，这个包非常有用，例如，tikz 图片。

## 1 `subfiles` 包
可以解决大多数问题，下面例子使用的文件结构如下所示

```latex
|- images
|  └─ overleaf-logo.pdf
|- sections
|  |─ introduction.tex
|  └─ section2.tex
|- main.tex
```

### 1.1 主文件

需要在主文件中添加两条特殊的命令

```latex
\documentclass{article}
\usepackage{graphicx}
\graphicspath{images/}

\usepackage{blindtext}

\usepackage{subfiles} % Best loaded last in the preamble

\title{Subfiles package example}
\author{Overleaf}
\date{ }

\begin{document}

\maketitle

\section{Introduction}

\subfile{sections/introduction}

\section{Second section}

\subfile{sections/section2}

\end{document}
```

![编译pdf](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image110.jpg "pdf")

首先需要在 preamble 中使用包 `\usepackage{subfiles}`

接下来每个外部的文件由命令`\subfile{}`引入。在这个例子中，我们从`sections`文件夹中引入了`introduction.tex`和`section2.tex`两个文件。文件名的后缀可以省略

### 1.2 子文件

设置好主文件后，每个子文件必须有一个特殊的结构

```latex
\documentclass[../main.tex]{subfiles}
\graphicspath{{\subfix{../images/}}}
\begin{document}
\textbf{Hello world!}
\begin{figure}[bh]
\centering
\includegraphics[width=3cm]{overleaf-logo}

\label{fig:img1}
\caption{Overleaf logo}
\end{figure}

Hello, here is some text without a meaning...

\end{document}
```

![编译pdf](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image113.jpg "pdf")

现在这个文件可以编译为一个独立的文件，document class 和 preamble 的其余部分将与主文档中定义的相同

第一条命令是 `\documentclass[../main.tex]{subfiles}`

方括号中的参数是相对于主文件的相对路径。在这个例子中，文件`introduction.tex`在文件夹`sections`中，所以文件`main.tex`是当前文件夹的上一级目录 (这也是../的含义)

在`introduction.tex`文件中使用`\graphicspath`命令的时候，你还需要使用`\subfix`命令，该命令的参数为相对文件夹路径

```latex
\graphicspath{{\subfix{../images/}}}
```

## 2 `standalone` 包

这个包提供了与`subfiles`包相同的功能，并且更为灵活。但是它的语法也更复杂，容易出错。主要的区别在于，它允许每个子文件拥有自己的 preamble。

下面的例子使用的文件结构为：

```latex
|- images
|  └─ overleaf-logo.pdf
|- sections
|  |─ introduction.tex
|  └─ section2.tex
|- diagram.tex
|- main.tex
```

### 2.1 主文件

```latex
\documentclass{article}
\usepackage[subpreambles=true]{standalone}
\usepackage{import}

\title{Standalone package example}
\author{Overleaf}
\date{May 2021}

\begin{document}

\maketitle

\section{First section}
\import{sections/}{introduction}

\section{Second section}
\import{sections/}{section2}

\end{document}
```

![编译pdf](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image111.jpg "pdf")

首先引入包 `\usepackage[subpreambles=true]{standalone}`

这个命令应该放置在文档的靠前部分。方括号中的参数告诉 $\LaTeX$ 去引入每个子文件中的 preamble (包只会引入一次)。如果没有指定这个参数，则需要确保在主文档中引入了所有必须的包，以及不同的 preamble 之间的兼容性

在主文档的主体部分，每个子文件由命令 `\import{}{}` 引入。也可以使用标准的 `\input{}`命令。这个例子中的方法，可以避免嵌套文件所可能引入的错误

### 2.2 子文件

每个子文件都必须拥有自己的 preamble，其中包含了所有让子文件正常运行的包

```latex
\documentclass[class=article, crop=false]{standalone}
\usepackage[subpreambles=true]{standalone}
\usepackage{import}
\usepackage{blindtext}

\begin{document}
A TikZ figure will be rendered below this line

\begin{figure}[ht]
\centering
\subimport{../}{diagram.tex}
\label{fig:tikzexample}
\caption{A nice simple diagram}
\end{figure}

\blindtext
\end{document}
```
![编译pdf](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image112.jpg "pdf")

其中 `\documentclass[class=article, crop=false]{standalone}` 声明了这个文件是使用了`standalone` 包的文件，方括号中有两个参数：

- `class=article`。设置当前文档的类型，你也可以使用其他的文档类型，例如`book`、`report`等 (除了beamer)
- `crop=false`。如果这个命令被忽略了，那么文件的输出会被裁剪到一个最小的大小

第二条命令 `\usepackage[subpreambles=true]{standalone}` 并不是强制的

但是因为这个例子用到了**嵌套的**子文件，所以我们必须使用它。命令 `\subimport{../}{diagram.tex}` 插入了一个 *tikz 图片*，`diagram.tex`文件的内容如下：

```latex
\documentclass{standalone}
\usepackage{tikz}
\usetikzlibrary{positioning}
\begin{document}

\begin{tikzpicture}[
roundnode/.style={circle, draw=green!60, fill=green!5, very thick, minimum size=7mm},
squarednode/.style={rectangle, draw=red!60, fill=red!5, very thick, minimum size=5mm},
]
%Nodes
\node[squarednode]      (maintopic)                              {2};
\node[roundnode]        (uppercircle)       [above=of maintopic] {1};
\node[squarednode]      (rightsquare)       [right=of maintopic] {3};
\node[roundnode]        (lowercircle)       [below=of maintopic] {4};

%Lines
\draw[->] (uppercircle.south) -- (maintopic.north);
\draw[->] (maintopic.east) -- (rightsquare.west);
\draw[->] (rightsquare.south) .. controls +(down:7mm) and +(right:7mm) .. (lowercircle.east);

\end{tikzpicture}
\end{document}
```
![编译pdf](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image114.jpg "tikz")

这是 `standalone` 包的主要特性，可以在文档的任何地方引入这个文件，并且循环利用里面的代码。例如，这个示意图可以随后在另外一个项目中使用，而不需要做任何改动

___

> 文章参考[Multi-file LaTeX projects](https://www.overleaf.com/learn/latex/Multi-file_LaTeX_projects)
