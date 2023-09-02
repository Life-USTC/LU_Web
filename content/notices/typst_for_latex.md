---
title: "写给LaTeX用户的Typst入门"
date: 2023-09-02T19:14:33+08:00
draft: false
---
> 原文地址：[Guide for LaTeX users – Typst Documentation](https://link.zhihu.com/?target=https%3A//typst.app/docs/guides/guide-for-latex-users/)

这篇文章是写给那些已经使用过LaTeX，并想要尝试Typst的用户。
我们将从用户的角度出发，解释这两套系统之间主要的不同。
虽然Typst并不是基于LaTeX构建的，语法也完全不同，但通过这篇文章，你可以了解如何把LaTeX的经验转化过来。

跟LaTeX一样，Typst是一门基于标记的排版系统[1]。首先在纯文本里编写自己的文档，然后通过一些命令和语法对其进行修饰，最后使用编译器将源文件排版成PDF。在以下几个方面，Typst跟LaTeX之间也存在区别：
**日常任务上，Typst使用更为专用的语法** ：这一点类比Markdown。 **Typst的命令也更有「原则性」**
：在LaTeX中，你可能需要为不同软件包学习不同的语法和约定，但在Typst中命令都保持一致，所以你只需要理解一些基本的概念。
**Typst比LaTeX快得多** ：Typst的编译通常只需要几毫秒而不是几秒，因此编译器都可以提供更加迅速的预览。

在接下来的部分，我们将回答从LaTeX切换到Typst的一些常见问题。

## 怎样创建一个新的、空的文档？

很简单，你只需要创建一个空的文本文档（文件后缀是`.typ`），
无需额外的模板，你可以直接开始编写。

换行符和LaTeX保持一致，空白一行即可：

![_example_](https://pic3.zhimg.com/v2-99b96afdfef3d4257b4766f1727b4066_b.jpg)

## 怎样创建段落标题、强调……？

LaTeX使用命令`\section`来创建段落标题，多级标题分别使用`\subsection`，`\subsubsection`
等，根据文档种类的不同，还有`\part`和`\chapter`

在Typst中，标题显得没那么啰嗦，在含有标题的那行，前面加上等号和空格，你就得到了一个第一级标题：`= Introduction`。
如果需要二级标题，就只需要两个等号`== In this paper`。
通过在前面加上等号，你可以嵌套任意层级的标题。

> 译者注：  
>
> 这一点上更接近Markdown中`#`的作用，在接下来的阅读中你会不断看到这种「Markdown+LaTeX」杂糅的产物，结合这两者分别的痛点，可以更加深入了解Typst设计这些语法的原因。

 _斜体_ 只需要把文本包含在`_下划线_` 中  
 **粗体** 则需要包含在`*星号*` 之中。

以下是一些常用的标记命令，分别是LaTeX和对应的Typst语法：

| | LaTeX| Typst |
|---|---|--- |
| 加粗 | `\textbf{strong}` | `_strong_` |
| 斜体 | `\emph{emphasis}` | `_emphasis_` |
| 行内代码 | `\texttt{print(1)}` | `` `print(1)` `` |
| 链接 | `\url{https://typst.app}`| `https://typst.app` |
| 标签 | `\label{intro}` | `<intro>` |
| 引用 | `\ref{intro}` | `@intro` |
| 引文 | `\cite{humphrey97}` | `@humphrey97` |
| 无序列表 | itemize | `\- List` |
| 有序列表 | enumerate | `\+ List` |
| 术语表 | description | `/ Term: List` |
| 图表 | figure | `#figure` |
| 表 | table | `#table` |
| 公式 | `$x$` align/equation | `$x$, $ x = y $` |

在Typst中使用列表并不需要环境，而使用一种更为轻量的语法。
只需要在每行开头前使用连字符，就可以创建一个无序列表：

![_example_](https://pic3.zhimg.com/v2-739616c81ee96368439e0810e688ea32_b.jpg)

通过正确的缩进，列表也可嵌套。
在每项间添加空行，可以得到一个行间距更大的列表。
把连字符`-`换成加号`+`可以得到有序列表。
替换成`/ Term: Description`的形式可以得到术语表。

> 译者注：
> 这里的 **连字符** 对应原文中hyphen，但这里并不是`U+2010`而是 **`U+2212`(Minus)**更不是`U+2013`(EN DASH)
>
> **如果不清楚上面在说什么就直接敲键盘上的减号就ok～**

## 如何使用命令？

LaTeX十分依赖以反斜杠(`\`)开头的命令，它需要通过这些宏来排版、插入或改变内容。
有些命令可以传入参数，这些参数通常使用大括号括起来。`\cite{rasmus}`

Typst区分两种模式： **标记模式** 和 **代码模式** [2]。
默认是 **标记模式** 。此模式下，你可以直接编排文本、使用不同的语法结构，如`*使用星号标记粗体文本*` 。
而 **代码模式** 下，则更类似像Python一样的编程语言，提供了输入、执行代码的选项。

在Typst的标记中，你可以使用井号(`#`)来使用单个命令（或者表达式）。
例如，你可以通过这种方式来分割不同的文件，或者基于某些条件渲染文字。在 **代码模式** 下，也可以通过方括号来包含正常的（ **标记模式** 下的）内容。
在 **代码模式** 下，内容（标记模式的整体）会被跟其他变量一样，当作一个值本身进行处理。

![_example_](https://pic1.zhimg.com/v2-4dcd9c4bd949f431e4e154590d20618c_b.jpg)

> 译者注：这段英文原文就表述的很不清晰，这里提供一点解释。
>
> **标记模式** ，如同Markdown，不需要额外的内容，默认就处在这个 **标记模式**
> 下：可以直接使用`_text_`或者`*text*`来创造斜体/粗体（参考上文）
>
> **代码模式** ，以`#`开头（类比LaTeX中以`\`开头来书写命令），仅仅存在于一个命令（表达式）中，当这个表达式结束之后，一切又回到
> **标记模式** 中。
> 在 **代码模式** 中，无需额外使用`#`（命令/关键字会直接识别，不同于LaTeX），同时在命令中也可以使用 **标记模式**（使用`[]`，比如例子给出的`[Hi #x]`
>
> 另外：
>
> * 在 **标记模式** 中，可以引用 **代码模式** 的函数、值，都通过`#`进行标记
> * 在 **代码模式** 中，函数返回值为`Content`的会在当前位置渲染出来
> * 在 **代码模式** 中，使用 **标记模式** 的内容(`Content`)，也可以作为变量的值
>
> 有一点点Vue那种混写的感觉

不同于LaTeX，Typst中函数定义总是要求函数名+括号的形式。（而LaTeX中，没有参数的情况下，`[]`和`{}` 都是可以忽略的。）
向函数内传入的参数与函数相关，并且可以在文档中找到。

### 参数

一个函数可以有多个传入参数，有些参数是 **位置参数** [3]，只需提供变量的值即可（不需要提供参数名）：
`#lower("SCREAM")`会以全小写的形式返回传入值。
很多函数使用 **命名参数** 来提高可读性，例如创建一个指定大小和描边的正方形，可以使用如下 **命名参数** ：

![_example_](https://pic2.zhimg.com/v2-a5aa173a486e4c3370e60a0a6c93e3dd_b.jpg)

指定 **命名参数** 时，你需要首先输入参数的名字，例如`width` `height`等，接下来输入冒号和对应的值`(2cm 1cm red)`
（你可以在文档或者自动补全中找到可以传入的参数）。
命名参数有些类似LaTeX中配置环境的办法，比如`\begin{enumerate}[label={\alph*)}]`。

大多数情况下，你会希望向函数传递一些`Content`。
例如，在LaTeX中的命令`\underline{Alternative A}`
在Typst中写成`#underline([Alternative A])`，方括号表示其中的内容就是`Content` 。
在这些括号中，你可以使用正常的标记语法。然而，这样写的括号数量还是太多了，因此你可以把位于尾部的`Content`放到括号后面（如果没有其他参数，甚至可以忽略`()`）：

> 译者注：
>
> 类似一些declarative UI中 omit trailing closure的方法

![_example](https://pic2.zhimg.com/v2-e90b7dfe5d86eeb7a8e73416df5976c9_b.jpg)

### 数据类型

你很可能已经注意到了，上文提到的这些参数有着不同的数据类型。Typst支持多种数据类型，下表是其中一些比较重要的类型和声明他们的办法。

> 注意：为了使用以下任何类型，你必须处在 **代码模式** 中。

| Data Type | Example |
| --- | --- |
| Content | [_fast_ typesetting] |
| String | "Pietro S. Author" |
| Integer | 23 |
| Floating point number | 1.459 |
| Absolute length | 12pt, 5in, 0.3cm |
| Relative length | 65% |

`String`与`Content`之间的不同之处在于`Content`中可以包含标记（包含函数调用），而`String`就是一个有序的字符串。

Typst提供了分支、循环结构，以及常用的运算符，比如`+`和`==`，你也可以定义你自己的变量，并在此基础上进行计算。

### 影响后续内容的命令

在LaTeX中，有些命令，例如`\textbf{bold text}`通过大括号传入参数，并且只影响括号内的内容。而有些命令，比如`\bfseries
bold text`「像开关一样起作用」，在这行命令后的所有内容都会受这个命令的影响。

在Typst中，同样的函数可以同时用来影响：

* 文档的剩余部分
* 一段区域（作用域）
* 它的参数

举例来说，`#text(weight: "bold")[bold text]`仅仅会加粗传入的参数，而`#set text(weight:
"bold")`会影响「直到这个区域结束」，（或者，如果不在作用域中，影响文档的剩余部分）。根据使用方式的不同（函数调用/使用`set`命令），很容易区分它的作用域。

![_example_](https://pic4.zhimg.com/v2-623836c64257966a75f7b473cd22f6eb_b.jpg)

`set`命令可能出现在文档的任何部分。后续调用中，可将`set`命令的参数视作默认参数：

![_example_](https://pic2.zhimg.com/v2-7a25ee6d377dcb787867652f70e248e9_b.jpg)

> 在这里，`+`是调用`enum`函数的语法糖（想象成某种简写），我们在上文中设置了`set rule`，因此这里的`enum`会参考`set
> rule`的参数。从这个意义上讲，多数的语法都是某个函数的一部分。如果你需要重新定义一个组件的样式（超过了修改其参数所能提供的），你可以通过`show
> rule`完全重定义其样式（与LaTeX中`\renewcommand`相似 .

### 怎样导入文档样式

在LaTeX中，你可以使用`\documentclass{article}`来定义文档的样式。在这个命令中，你也可以通过把`article`更换为`report`和`amsart`来更换文档的样式。

在使用Typst中，你可以通过函数来修改文档的样式。通常情况下，你可以使用模板中提供的函数来修改整个文档，使用方式如下：你可以通过import来导入模板函数，然后你使用这个函数来对文档使用样式。具体的做法是通过`show
rule`来将整个文档包装在这个函数中，具体如下：

![_example_](https://pic2.zhimg.com/v2-1d05466d8c3f1a5cf2b543244e085855_b.jpg)
![_example_](https://pic3.zhimg.com/v2-7149b8f69443dc7826d4c902fc4cf95e_b.jpg)

这里的`import`命令，导入了其他文档中声明的函数。在这个例子中，它从`conf.typ`中导入了`conf`函数。这个函数讲整个文档装饰成一个会议论文。我们通过`show
rule`讲这个样式应用到全局，同时设置了文档的一些元数据[4]。在应用`show rule`之后，我们可以立刻开始写整个文章。

>
> 函数算作Typst的命令，而且可以将相应的输出成所需的结果，包括`Content`。在Typst中函数都是「过程的、纯的」，意味着他们除了输出值不可以有其他额外的影响。区别于LaTeX中宏定义可能对文档有着意想不到的作用
>
> 为了将一个样式应用到整个文档，`show rule`会把后续的所有内容都作为参数，传递给冒号后面定义的函数，
> `.with`是一种方法，它通过预先设置一些参数，在传递给`show rule`之前进行一些设置。

在网页应用中，你可以选择一些预先定义好的模板，甚至可以通过`template wizard`创建自己的模板 。你也可以访问`awesome-typst
repo`来查看一些社区提供的模板。我们正在筹备一个包管理器，在那之后这一切都会更加容易分享！

你也可以创建自己、自定义的模板，他们比LaTeX同类的`.sty`文件更加简短、已读（甚至是几个量级的好用\\(^o^)/~，所以赶快来尝试吧）

### 怎样导入包

跟LaTeX相比，Typst更像是那种自带电池的玩具，所以会自带很多LaTeX包的内容。在下面我们列出一些LaTeX中常用的包，和他们对应的Typst命令：

|LaTeX Package | Typst Alternative |
|---|--- |
|graphicx, svg | image function |
|tabularx | table, grid functions |
|fontenc, inputenc, unicde-math | Just start writing! |
|babel, polyglossia | text function: #set text(lang: "zh") |
|amsmath | math mode |
|amsfonts, amssymb | sym module & syntax |
|geometry, fancyhdr | page |
|xcolor | text function: # set text(fill: rgb("#0178A4")) |
|hyperref | link function |
|bibtext, biblatex, natbib | cite, bibliography functions |
|lstlisting, minted | raw function & syntax |
|parskip | block & par functions |
|csquotes | set the text language and type " or ' |
|caption | figure function |
|enumitem | list, enum, terms function |

如果你需要从另一个文件中导入函数/变量，可以使用`import`命令。如果你仅仅需要导入文件的内容，可以使用`include`命令。它会从文档中获取相应的内容，填入文档中。

目前，Typst尚不存在包管理器，但是我们在正在积极地筹备一个，来帮助你轻松地导入一些工具或者模板类的包（通常是社区贡献的），并且你也可以贡献你自己的。在那之前，我们还是建议你查看`awesome-
typst repo`，这里面包含了很多为Typst使用的包。

### 怎样输入数学公式？

在Typst中 ，把公式包含在dollar记号(`$`)中即可，在两个`$$`中添加额外的空格（或者换行）可以进入展示模式[5]。

![_example_](https://pic4.zhimg.com/v2-06025a5657b5a267fbcb9f537eb77eab_b.jpg)

数学模式跟常规的标记模式或者代码模式不完全相同。数字和单独的字符会被展示出来，而连续的（不含数字的）字符会被解释为Typst变量。

Typst预定义了一些很有用的符号（所有的希腊字母`(alpha, beta, ...)` & 一些希伯来字母`(alef,
bet)`），一些字符可以通过他们的缩写来轻松地访问到，例如`<=, >=, ->`。

完整的符号列表可在文档中找到，如果那里缺失了某些符号，你也可以通过`Unicode escape`插入这些字符。

一些其他的或者相近的符号，一般可以通过加入`._modifier_`访问到，例如可以通过`arrow.l.squiggly`来插入一个「向左弯曲的箭头」。

如果你只想要向公式中加入一个多字符的文本，使用双引号把他们包裹起来：

![_example_](https://pic4.zhimg.com/v2-83909a07ee317deff5c7a325e984a0b3_b.jpg)

在Typst中，分隔符会自动根据表达式来缩放（就好像LaTeX中默认帮你插入了`\left`和`\right`
命令）。你也可以通过`lr`函数来手动修改分隔符的行为。为防止分隔符自动缩放，你可以通过反斜杠来进行转义。

在不破坏运算优先级的前提下，Typst自动把`/`的两端处理成分式，所有没必要的括号不会出现在编译结果中：

![_example_](https://pic3.zhimg.com/v2-dd0f9e088c2430e8ee98d5af201496d2_b.jpg)

上标和下标在Typst和LaTeX中表现相似，`$x^2$`会创建上标，`$x_2$`会创建下标。如果你需要包含更多的字符，把包含的字符包裹在括号中即可：`$x_(a
-> epsilon)`。

既然数学模式下变量不需要以`#`或者`/`开头，你也可以无需额外的字符来调用函数：

![_example_](https://pic3.zhimg.com/v2-d036726db8d94f7d2d9d2aa08b10e68a_b.jpg)

上述例子通过`cases`函数来表述`f`，有了`cases`函数之后，参数通过逗号分隔，这些参数也会被`math`模式进行解释。如果你需要传递Typst变量的话，加上`#`
前缀。

![_example_](https://pic2.zhimg.com/v2-3e3ab587cccf7dcefdb0a3d5f1189249_b.jpg)

在数学模式下，你可以使用任意的Typst函数或者任何内容，如果你希望他们正常工作，只需要使用`#`前缀，没人可以阻止你把长方体或者emoji作为参数传入：

![_example_](https://pic2.zhimg.com/v2-fe8a0648ff68ecce51d2fa2b76430509_b.jpg)

如果你更希望直接以Unicode形式输入符号，这也是可行的~

数学模式下，函数也可以通过`;`作为分隔符，传入一个二维列表，这一点最常用的使用方式是使用`mat`函数创建矩阵：

![_example_](https://pic4.zhimg.com/v2-7cd751394d45cbf9a1523f4e16934df7_b.jpg)

### 怎么得到一个类似LaTeX的样子?

使用LaTeX编写的文章总能让人一眼认出，这通常是因为字体、对齐方式、窄行距和宽页边距。

下面的例子可以作为一个参考：

![_example_](https://pic3.zhimg.com/v2-bac026a85eda520ed317694628e2d042_b.jpg)

### 相比LaTeX，Typst还有哪些不足？

今天，对于大多数人，Typst已经是一个可以替代LaTeX的产品，但是仍然有很多功能Typst（尚）不支持，以下是一些不支持的功能（少部分有替代方法）

1. 原生图表和绘图：LaTeX用户经常在文档内通过PGF/TikZ，Typst现在还不包含绘图的工具，但是社区已经提供了一些方案，例如`typst-canvas` `typst-plot`和`circuitypst`等，你可以访问他们的链接来开始绘图
2. 在不换页的情况下调整页边距：LaTeX中，你可以在不换页的前提下调整页边距。在Typst中调整页边距，你必须使用`page`函数（会强制换页）。如果你只是需要调整几个段落的边距，可以使用`pad`函数（负padding）
3. 不定位置的图表：LaTeX中的`\figure`命令会自动寻找最理想的图表位置，可能是在页面的最上面、最下面，或者是单独的一页。在Typst中，图标总是会放在标记模式中确定的位置。这个功能可能节省一些头疼的时间，但有些时候仍需手动放置图表。这个功能会很快加入Typst
4. 以图片的形式插入PDF：在LaTeX中，有时为插入矢量图，会以图片的形式插入PDF或者EPS文件。Typst不支持以图片形式读取这两个格式，但通过第三方工具，你总是可以很容易把它们转换成SVG格式（再插入），后续网页应用也会加入自动转换的支持
5. 换行符优化：LaTeX的算法会智能优化换行符 & 换页符。Typst虽然会避免「孤儿」和「寡妇」[6]的出现，它所使用的算法远远不及LaTeX使用的复杂。你可以在提交前，插入自定义的换页符：`#pagebreak(weak: true)` 。参数`weak`会保证：如果这里本来就该是很自然的换页，不会插入双页换行符，你可以使用`#v(1fr)`在页面中插入一些空白。这点和LaTeX的`\vfill`相似
6. 参考文献不能自定义样式：在LaTeX中，`bibtet` `biblatex` 和 `natbib`提供了一些自定义引用和参考文献的格式（也可以通过`.bbx`来定义样式）。相比之下，Typst目前仅支持一小部分引用格式，但是我们现阶段想通过支持一种`XML`格式的`Citation Style Language(CSL)`来支持这一功能。
