# Markdown笔记

> [Bilibili参考视频](https://www.bilibili.com/video/BV1jV411j7mz)
>
> [参考网站]([Markdown - Tutorial](https://thu-ios.github.io/tutorials/lecture/markdown.html))

## 使用markdown的原因

我们要向别人传达信息时，需要承载信息的载体，这个载体可以是语言、文字、图像等等，或者结合起来一起使用，比如`PPT`。

但是一般来说，文字是最方便的载体，但是很多时候如果只有文字会让人觉得枯燥，因此带格式的文字作为一种增强的表达方式被人们采用，使用率最高的可能是众所周知的`Microsoft Word`等。

但对于程序员来说，`Word`不够高效，因为很多功能是我们不需要的，并且需要一个庞大的`Word`软件才能够看到、编辑，甚至我们如果只是想对文字进行处理只需要`txt`文件以及系统自带的文本编辑器即可，而且如果我们想用`Git`进行管理，`Word`生成的`.doc`文件(二进制文件)无法使用`Git`进行管理（逐行管理）。

因此，为了兼顾上述所有的要求找到其中的平衡，我们使用`Markdown`。`Markdown`其实是一种写作风格/方式，我们用这种风格/方式写出来的**纯文本文件**（和`.txt`是一样）叫做**markdown文件**，一般以`.md`作为文件后缀（而不是`.txt`）。`.md`文件虽然是纯文本，但其中用一些特殊的字符（如`* # [] () …`）给纯文本带来格式（这与`html`文件是相似的，也可以将`markdown`看作是简单的`html`）。这些格式通过某种方式进行渲染（注：渲染：指将计算机中的某些数据呈现在屏幕上）你就可以看到它们代表的格式了！

## Markdown语法

`markdown`用一些特殊的字符（如`* # [] () …`）给纯文本带来格式，其实语法指的就是这些规则。那么下面学习如何用这些特殊符号来在纯文本中表达格式。

### 具体语法

[GitHub Guides | Mastering Markdown]([基本撰写和格式语法 - GitHub 文档](https://docs.github.com/zh/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax))

`Markdown`有很多扩展语法，我们主要学习它最基础的语法，和一些`GitHub`支持的语法。

#### Headers 标题

`1`~`6`个井号  空格  标题名称

```
# 一级标题
##  二级标题
......
######  六级标题
```

实际上，五级标题和六级标题都很少用到，因此没有更小的标题了。  

#### Emphasis 加粗和斜体

斜体：一对`*`或者一对`_`

加粗：两对`*`或者两对`_`

```
*This is will be italic*
_This is will be  italic_

**This is will be bold**
__This is will be bold__

_You  **can** combine them_
```

*This is will be italic*
_This is will be italic_

**This is will be bold**
__This is will be bold__

_You **can** combine them_

一般我们单个使用的时候用`*`多一些，但是两种格式组合使用的时候就随意了。

#### Lists 列表

##### Unordered 无序列表

无序列表：`*`  空格  列表项

可以进行`tab`缩进来控制列表

```
* item 1
* item 2
  * item 2a
  * item 2b
```



* item 1
* item 2
     * item 2a
     * item 2b

##### Ordered 有序列表

有序列表：`1.`  空格  列表项

这里可以缩进的哦，缩进会重新编号，或者变成小标题（如`1.1` `2.1.3`这样）

回车即可生成下一个列表项

```
1. Item 1
1. Item 2
1. Item 3
    1. Item 3a
    1. Item 3b
```

1. Item 1
2. Item 2
3. Item 3
    1. Item 3a
    1. Item 3b

##### Task Lists 任务列表

任务列表：`-`  空格  `[]`  空格 列表项

其中如果完成了任务，在`[]`中添加x，为`[x]`

```
- [x] this is a complete item
- [ ] this is an incomplete item
```

- [x] this is a complete item
- [ ] this is an incomplete item

#### Links 链接

`[Text](url)`：中括号，后面小括号。小括号里面放链接，中括号里面放说明（必须）；不需要说明的话，可以直接写链接

直接写链接会直接被转换为可以点击的链接；也可以在两侧加上`<`和`>`

```
[GitHub Official Site](https://github.com)

https://github.com

<https://github.com>
```

[GitHub Official Site](https://github.com)

https://github.com

<https://github.com>



#### Images 图片

`![Text](url)`：感叹号，中括号，小括号。小括号里面放图片链接，中括号里面放图片说明（不必须；写了的话会在图片下方或某处显示说明，当因为某种原因图片无法加载的时候，显示时也会用说明替代图片）

```
![GitHub Logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)
```

![GitHub Logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)

#### Inline Code 行内代码

行内代码：\` 代码 \`

```
`Swift`中，`var`定义变量，`let`定义常量
```

`Swift`中，`var`定义变量，`let`定义常量

#### Code Block 代码块

用一对三个反撇\`\`\`包裹，在最开始三个反撇后可以加代码的语言名称或简写以在渲染时获得高亮支持。

\`\`\`swift

var natural_numbers: Array<Int> = [0,1,2,3]

print(natural_numbers.capacity)

\`\`\`

```swift
var natural_numbers: Array<Int> = [0,1,2,3]

print(natural_numbers.capacity)
```

一般支持的代码高亮会有很多，比如：`shell`、`bash`、`c`、`cpp`、`java`、`objectivec`、`python`、`swift`、`yaml`、`html`、`xml`等

#### Blockquotes 引用

```
As Tim Cook said:

> Fearlessness means taking the frst step, 
> even if you don't know where it will take you.
>
> ——Tim Cook's Commencement Address at Duke University, 2018
```

As Tim Cook said:

> Fearlessness means taking the frst step, 
> even if you don't know where it will take you.
> 
> ——Tim Cook's Commencement Address at Duke University, 2018

一般会用它来在文章开头写一下文档的更新日期和作者。

#### Tables 表格

若想创建表格，你可以先列出一组单词，接着使用连字符 “-”（将其用于首行）把这些单词分隔开，之后再运用竖线 “|” 来分隔各个列，如此操作便能创建出表格了。

```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

#### 警报

警报是基于块引用语法的 Markdown 扩展，可用于强调关键信息。 在 GitHub 上，它们以独特的颜色和图标显示，以指示内容的显著性。

只有在对用户成功至关重要时才使用警报，并将每篇文章的警报限制在一到两个，以防止读者负担过重。 此外，应避免连续发出警报。 警报无法嵌套在其他元素中。

要添加警报，请使用指定警报类型的特殊块引用行，然后在标准块引用中添加警报信息。 可以使用以下五种类型的警报：

```markdown
> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
```

下面是呈现的警报：

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.



#### 其他GitHub支持的语法

更多`Github`支持的`markdown`语法可以查看[GitHub Guides | Mastering Markdown](https://guides.github.com/features/mastering-markdown/)

###  对文件路径的理解

我们在插入链接的时候，会使用：

```
[Google](https://www.google.com) is your best friend!
```

[Google](https://www.google.com) is your best friend!

方括号里面放你要呈现的名字，圆括号里面放网页的链接。

更普通的，这个链接还可以换成文件：

```
点击查看[帮助文档](../../help.md)
```

点击查看[帮助文档](../../help.md)

这个路径是相对路径，表示和当前的md文件在同一个路径下的`docs`文件夹里面的`help.md`文件，一般我们都会将md文件放在一个总的文件夹中，这样它们之间就可以使用相对路径相互引用了。

如果是在自己电脑上写md，也可以写绝对路径。但是这样一旦那个文件移动位置，使用绝对路径就找不见那个文件了。使用相对路径的话，由于一般md文件会随着总文件夹跟着其他的文件一起走，所以一般不会出现找不到的问题。

更普通的，还可以换成当前文档中的某个大标题：

```
点击跳转到这篇markdown的[Intro部分](#使用markdown的原因)
```

点击跳转到这篇markdown的[Intro部分](#使用Markdown的原因)

### 对url资源的理解

在我们插入图片的时候，我们使用了这样的语法：

```
![图片名称](图片链接)
```

本质上来说，你获取一张网络上的图片，是在服务器（24h不关机的电脑）的文件系统里面获取了这张图片。但为了能保证一张图有一个唯一的标志，一般一张图都会有一个自己的链接。

打开带图片的网站，右键图片，就可以看到`复制图片链接`的按钮从而获取图片的链接。

这里的`图片链接`也可以是刚刚的相对路径，比如：

```
![Markdown图标](./media/markdown_icon.png)
```

但这样，你就需要在和你现在写的`markdown`的同一目录下，放一个`media`文件夹，里面有这张`markdown_icon.png`的图片。

有的时候，图片和代码相比起来，是个庞然大物（`1KB` vs `1MB`），这时我们不希望将图片加入到项目中（指不希望项目的体积很大，别人从`GitHub`上下载项目时花的时间过久），可是在项目说明中还需要加入图片进行说明，这时怎么办呢？最简单的，将图片压缩一下（`1MB->100KB`）扔进项目文件夹，这是最省心的…但要是图比较多，一般来说，我们会选择某些厂商的对象存储服务，将这些图片资源放到比如阿里云的服务器上，然后这个服务把图片的网络链接给你，你就可以在`markdown`中使用这个链接了。如果没有那么正式，那么这种服务叫做图床。比如我一直在用的[聚合图床](https://www.superbed.cn)，你把图片丢进去，它帮你将图片转为一个链接。但是使用这种服务也有需要注意的地方，如果运营图床的工作室哪天跑路了，你放进去的图片可能就没了。

### 添加目录

不少平台都支持使用`[toc]`来添加目录。你只需要输入`[toc]`，平台就会帮你自动渲染生成目录。

但也有一些平台不支持这样，这时你需要使用VS Code中的`Markdown All in One`插件，使用这个插件提供的`自动生成目录`功能来添加目录。

### 其他一些注意事项

有的时候你在`markdown`明明换行了，可是上传到`GitHub`上面一看，文字都粘在一起了。这是为什么呢？

英文在分段的时候，不像我们写文章段前空两格，他们会直接在两段之间多空一行。一般的回车只是用来方便阅读，不然一行的内容太长了。

如果你不希望这种方式生效，可以在一行后面加两个空格；但这样很麻烦，还是多加回车吧；最好在每种语法前后都空行，这样也能有效减少语法不被识别的情况

（注：多于2个的连续回车markdown会将它们当作一个回车哦）

## 文字编辑效率up技巧

最后呢，再给大家分享一些在 Windows 系统下快速写文档的实用方法，这些方法在 Windows 上常见的文字编辑软件（比如 Microsoft Word、WPS 文字等）以及代码编辑软件（像 Visual Studio Code 等）基本都适用。

〇 双击鼠标左键选中一个词：这里所说的词指的是一个中文的词语或者一个英文的单词。

〇 三击鼠标左键选中一行内容。

〇 Ctrl + 左右方向键：能以词为单位移动光标，方便快速定位到想要的位置。

〇 Home 键、End 键、Ctrl + Home 键、Ctrl + End 键：分别可以将光标移动到行首、行尾、文档开头、文档末尾哦。

〇 按住 Shift 键：再配合上下左右方向键，可以进行文字选中操作；另外，Shift + Ctrl + 左右方向键或者 Shift + Alt + 左右方向键等组合也能实现不同规则的文字选中；Shift + Ctrl + 上下方向键同样可以按照相应规则来选中内容。

〇 按住 Alt 键：然后拖动鼠标可以进行矩形区域的选中，在需要对特定块状区域内容操作时很有用。

〇 Ctrl + Backspace 键、Ctrl + Delete 键：可以分别删除光标前的一个词、光标后的一个词；Backspace 键用于向前删除字符，Delete 键用于向后删除字符；Ctrl + X 快捷键也是一种删除（剪切）内容的常用方式呀，能方便地移除相应文本内容。
