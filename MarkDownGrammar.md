---
title: MarkDown语法笔记
date: 2016-06-29 21:47:17
tags: ["MarkDown"]
categories: ["其他"]
page_pv: true
page_pv_header: 本文总阅读量
page_pv_footer: 次
---
## 区块元素

### 段落和换行

> 一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行（空行的定义是显示上看起来像是空的，便会被视为空行。比方说，若某一行只包含空格和制表符，则该行也会被视为空行）。普通段落不该用空格或制表符来缩进。

### 标题

Setext 用底线的形式

	this is an h1
	=
	this is an h2
	-
	ps:任何数量的 = 和 - 都可以有效果。

> 利用 `=` （最高阶标题）和 `-` （第二阶标题）**

Atx 在行首插入 1 到 6 个 `#` ，对应到标题 1 到 6 阶

	# 这是 H1
	## 这是 H2
	...
	###### 这是 H6

### 区块引用 Blockquotes

> 若区块的整个段落超过一行，在第一行最前面加上 `>` 即可，区块可以嵌套使用，根据不同层次加上不同数量的 `>`，区块也可以使用其他的语法，包括标题，列表，代码区块等

### 列表

* 无序列表：使用 `*` 、 `+` 或是 `-` 作为列表标记
* 有序列表则使用数字接着一个`.`（英文句点）

### 代码区块

> 创建代码区块很简单，只要缩进 4 个空格或者是 1 个制表符

### 分割线

> 你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格

## 区段元素

### 链接

行内式

		This is [an example](http://example.com/ "Title") inline link.
		See my [About](/about/) page for details.

> 只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可

参考式

	This is [an example](http://example.com/ "Title") inline link.

	This is [an example] [id] reference-style link.
	[id]: http://example.com/  "Optional Title Here"

	[Google][]
	[Google]: http://google.com/

> 在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记

### 强调

	*single asterisks*
	_single underscores_
	**double asterisks**
	__double underscores__

> Markdown 使用 `*` 和 `_` 作为标记强调字词的符号

### 代码

如果要标记一小段行内代码，你可以用反引号把它包起来（`），例如
	Use the `printf()` function.
如果要在代码区段内插入反引号，你可以用多个反引号来开启和结束代码区段：
	``There is a literal backtick (`) here.``

### 图片

行内式

	![Alt text](/images/111.png)
	![Alt text](/images/111.png "Optional title")

> 详细叙述如下：
> * 一个惊叹号 !
> * 接着一个方括号，里面放上图片的替代文字
> * 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上 选择性的 'title' 文字。

参考式

	![Alt text][id]
	[id]: url/to/image  "Optional title attribute"

## 其他

### 自动链接

	<http://example.com/>

> Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用尖括号包起来， Markdown 就会自动把它转成链接。

### 反斜杠

	\   反斜线
	`   反引号
	*   星号
	_   底线
	{}  花括号
	[]  方括号
	()  括弧
	#   井字号
	+   加号
	-   减号
	.   英文句点
	!   惊叹号

> Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号

## Markdown 免费编辑器

Windows
*	[MarkdownPad][]
*	[MarkPad][]

Linux
*	[ReText][]

Mac
*	[Mou][]

在线编译器
*	[Markable.in][]
*	[Dillinger.in][]

浏览器插件
*	[MaDe][]


[MarkdownPad]: http://markdownpad.com/
[MarkPad]: http://code52.org/DownmarkerWPF/
[ReText]: http://sourceforge.net/p/retext/home/ReText/
[Mou]: http://25.io/mou/
[Markable.in]: https://markable.in/
[Dillinger.in]: http://dillinger.io/
[MaDe]:https://chrome.google.com/webstore/detail/made/oknndfeeopgpibecfjljjfanledpbkog
