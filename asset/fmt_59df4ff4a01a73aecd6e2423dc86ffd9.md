
虽然 `id` 和类是用于选择器最常用的属性，但任何属性属性值都可以作为选择器的基础。图 2-15 列出了所有基于属性和属性值的 CSS 选择器模式。

![](img/bf90ebf56b5f948b05e7a26851204c31_128_0.png)

# HTML 112 HTML 与 CSS | 教程 2 开始使用 CSS

图 2-15 属性选择器示例

| 选择器 | 匹配 | 示例 | 匹配 |
|---|---|---|---|
| `elem#id` | 任何 ID 值为 id 的元素 | | id 为 intro 的 h1 标题 |
| `#id` | 任何 ID 值为 id 的元素 | `#intro` | 任何 id 为 intro 的元素 |
| `elem.class` | 所有 class 属性值为 class 的元素 | `p.main` | 属于 main 类的类的所有段落 |
| `.class` | 所有 class 值为 class 的元素 | `.main` | 属于 main 类的类的所有元素 |
| `elem[att]` | 所有包含 att 属性的元素 | `a[href]` | 所有包含 href 属性的超元素 |
| `elem[att="text"]` | 所有 att 属性等于 text 的元素 | `a[href="top.html"]` | 所有属性等于 top.html 的超元素 |
| `elem[att*="text"]` | 所有 att 属性包含单词 text 的元素 | `a[rel="glossary"]` | 所有 rel 属性包含单词 glossary 的超元素 |
| `elem[att~="text"]` | 所有属性值为以 text 开头的由连字符分隔的单词列表的元素 | `p[id="first"]` | 所有 id 以连字符分隔单词列表中的 first 开头的段落 |
| `elem[att^="text"]` | 所有属性以 text 开头的元素 [CSS] | `a[rel="prev"]` | 所有 rel 属性以 prev 开头的超元素 |
| `elem[att$="text"]` | 所有属性以 text 结尾的元素 [CSS] | `a[href="org"]` | 所有属性以 org 结尾的超元素 |
| `elem[att+="text"]` | 所有 att 属性包含值 text 的元素 [CSS] | `a[href="faq"]` | 所有属性包含文本字符串 faq 的超元素 |

请注意，图 2-15 中列出的某些属性选择器首次在 CSS3 中引入，因此在旧版浏览器中可能不受支持。

- 根据 ID 选择元素，使用 `elem#id` 或 `id` 选择器，其中 `elem` 是元素名称，`id` 是 id 属性的值。
- 根据类值选择元素，使用 `.class` 或 `elem.class` 选择器，其中 `class` 是 class 属性的值。
- 选择包含 `att` 属性的元素，使用 `elem[att]`。
- 根据属性值是否等于指定值来选择元素，使用 `elem[attr="val"]`。

## 教程 2 开始使用 CSS | HTML 与 CSS

在 Tri and Succeed Sports 首页中，主要内容被封装在一个 ID 为 `about_tss` 的 `article` 元素中。Alison 写了她在会话中输入的 h1 和 h2 标题样式，这些样式仅适用于具有此特定 ID 的 h1 和 h2 元素。现在修改样式表。

### 应用 id 选择器：

1. 回到编辑器中的 `tss_styles.css` 文件。
2. 将标题样式（Heading Styles）中 `h1` 和 `h2` 元素的选择器分别改为 `article#about_tss h1` 和 `article#about_tss h2`。

图 2-26 显示了样式表中修改后的选择器。

![](img/bf90ebf56b5f948b05e7a26851204c31_130_0.png)

```css
/* Heading Styles */

selects h1 headings

within an article element

with the about_tss id

article#about_tss h1 {
  color: white;
  background-color: rgb(222, 128, 60);
}

selects h2 headings

within an article element

with the about_tss id

article#about_tss h2 {
  color: white;
  background-color: rgb(235, 177, 131);
}
```

3. 保存文件中的更改，并在浏览器中重命名 `tss_home.html` 文件。验证 h1 和 h2 标题的设计是否仅应用于 article 区域的标题，而不应用于页面上的其他标题。

该 `article` 元素将用在 Tri and Succeed Sports 网站的其他页面中。Alison 为你提供了三个额外的 HTML 文件，其中包含了针对跑步者、自行车运动员和游泳者提供的说明描述。在这些页面上，`article` 元素具有值为 `syllabus` 的 class 属性。为其他页面中的 h1 和 h2 元素创建样式规则。

### 应用类选择器：

1. 使用编辑器打开 `html02` 教程文件夹中的 `tss_run_txt.html`、`tss_bike_txt.html` 和 `tss_swim_txt.html` 文件。在每个文件的注释部分输入你的名字和日期，并将其分别保存为 `tss_run_txt.html`、`tss_bike_txt.html` 和 `tss_swim.html`。
2. 在三个三个文件的 `</head>` 标签之前插入 `<link>` 元素，将这些文件分别链接到 `tss_layout.css` 和 `tss_styles.css` 文件：

```html
<link href="tss_layout.css" rel="stylesheet" />
<link href="tss_styles.css" rel="stylesheet" />
```

3. 花些时间研究文件的内容和结构。注意 `article` 具有 class 属性值 `syllabus`。保存你的更改。
4. 回到编辑器中的 `style.css` 文件。
5. 在标题样式（Heading Styles）部分，添加以下样式规则，在浅紫色背景上以中灰色显示 h1 和 h2 标题：

```css
article.syllabus h1, article.syllabus h2 {
  background-color: lightpurple;
  color: mediumgray;
}
```

图 2-17 显示了具有类 `syllabus` 的文章。![](img/bf90ebf56b5f948b05e7a26851204c31_131_0.png)
图 2-18 显示了类 `syllabus` 的样式规则。![](img/bf90ebf56b5f948b05e7a26851204c31_131_1.png)

```css
/* Aside and Blockquote Styles */
/* (Wait, the text continues) */
```

6. 保存样式表并在浏览器中打开 `run.html` 文件。图 2-19 显示了页面上的 h1 和 h2 标题外观。
7. 使用页面上的导航链接查看自行车和游泳页面的内容，然后确认这些页面上的 h1 和 h2 标题格式相同。

## 计算选择器权重

CSS 的通用规则是更具体的选择器优于通用的选择器；但该规则的适用并不总是清晰。例如，以下选择器中哪个更具体？

```css
header h1
vs.
#main h1
```

为了回答这个问题，CSS 为选择器的权重分配一个数值，使用（内联、类、元素），其中 inline 代表内联样式为 1，其他代表选择器中的每个 id 或类为 0，elements 代表选择器中的每个元素为 1。选择器 `#links.first` 的值为 (0, 1, 1, 2)，因为它包含一个 id 值 (#links)、一个类值 (.first) 和两个元素 (u 和 li)。

回答我们之前的问题：选择器 `header h1` 的值为 (0, 0, 1, 2)，而 `#main h1` 的值为 (0, 1, 0, 1)，因此被认为更具体，因为 011 大于 012。

顺便说一下，每个内联样式都是 (1, 0, 0, 0)，因此将优于嵌入或外部样式表中的任何类型。

## 使用字体

排版是设计页面字符和字母外观的艺术。到目前为止，你使用的唯一属性样式是设置文本颜色的 color。在接下来的会话中，你将探索 CSS 字体族的其他属性，从选择字体开始。

### 选择字体

文本字符基于定义字母样式和外观的字体。大多数浏览器显示文本的默认字体是 Times Roman，但你可以使用 `font-family` 属性为任何页面元素指定不同的字体：

```css
font-family:
```

其中 fonts 是一个逗号分隔的列表，也称为字体栈或通用名称。特定字体是通过名称标识的字体（例如 Times New Roman 或 Helvetica），通用字体是存储在你的计算机或网络上的字体定义文件。通用字体描述文本字符的一般外观，但不指定特定的字体定义文件。相反，

## HTML 和 CSS | 教程 2 开始使用 CSS

字体定义文件由浏览器选择，以匹配通用字体族的一般特征：CSS 支持以下通用字体族：

- serif（衬线字体）：在每个字符末尾带有细小装饰线条的字体。
- sans-serif（无衬线字体）：没有任何衬线方向的字体。
- monospace（等宽字体）：每个字符宽度相同的字体；通常用于显示编程代码。
- cursive（手写体）：模仿手写体并具有高度风格化元素和装饰笔的字体；最适用于装饰性页面元素的细小细节。
- fantasy（装饰字体）：一种用于页面装饰的极具装饰性的字体；绝对不应用于正文文本。

由于你无法控制浏览器为通用字体选择哪种字体定义，常见的做法是按照偏好顺序列出特定字体，并以通用字体结束字体族栈。如果浏览器找不到任何特定字体，它将使用它自己选择的通用字体。例如，以下样式：

```
font-family: 'Arial Black', Gadget, sans-serif;
```

该样式告诉浏览器寻找 Arial Black 字体（如果可用）；如果这些都不可用，则使用它的无衬线字体。注意，包含一个或多个空格（如 Arial Black）的字体将用单引号或双引号括起来。

由于可用字体随操作系统和设备不同而异，挑战在于选择一个字体列表来匹配网络字体，网络字体是在所有操作系统和所有设备上都以相同方式显示的字体。图 2-19 列出了常用的网络字体字体栈。

### 网络字体字体栈

```
Arial
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Helvetica, Arial, sans-serif;
```

```
Arial Black
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Gadget, sans-serif;
```

```
Century Gothic
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Courier New, sans-serif;
```

```
Comic MS
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Comic Sans MS, sans-serif;
```

```
Courier New
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Courier New, Courier, monospace;
```

```
Georgia
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Georgia, sans-serif;
```

## Lucida Console

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Lucida Console, monospace;
```

## Lucida Sans

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Lucida Sans, Lucida, sans-serif;
```

## Palatino Linotype

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Palatino Linotype, Antiqua, serif;
```

# Tahoma

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Tahoma, sans-serif;
```

# Times New Roman

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Times New Roman, Times, serif;
```

## Trebuchet MS

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Trebuchet MS, Helvetica, sans-serif;
```

## Verdana

```
`abcdefdefghijkmnopqrstopqrstuvwxyzxyz:1234567890`
Verdana, Geneva, sans-serif;
```

![](img/bf90ebf56b5f948b05e7a26851204c31_133_0.png)

包含过多字体会让你的文本难以阅读。单个页面内使用的字体类型不要超过两种。

通常规则是标题使用无衬线字体，正文使用衬线字体。另一个通用的规则是标题和正文使用无衬线字体，特殊效果和大号字体使用衬线字体。

一个例外是 Tric Sports 网站，基于浏览器应用的一种字体。你将为无衬线字体添加以下字体：

```
font-family: 'Verdana', Geneva, sans-serif;
```

# 教程 2 开始使用 CSS | HTML 和 CSS

由于这种类型样式，浏览器将首先尝试加载 Verdana 字体，然后是 Geneva 字体。如果这两个字体都不可用，浏览器将加载它自己选择的通用字体。将此字体添加到页面正文样式规则中。

### 为页面正文指定字体族：

1. 回到编辑器中的 `tss.css` 文件。
2. 为 `body` 元素的样式规则添加以下样式：
`font-family: Verdana, Geneva, sans-serif;`

图 2-20 高亮显示了 `body` 元素的新的新样式。

![](img/bf90ebf56b5f948b05e7a26851204c31_134_0.png)

```
body {
  color: rgb(91, 91, 91);
  background-color: ivory;
  font-family: Verdana, Geneva, sans-serif;
}
```

3. 在浏览器中保存对 `tss.html` 文件的更改。图 2-21 显示了使用无衬线字体正文文本的重新出现。

![](img/bf90ebf56b5f948b05e7a26851204c31_134_1.png)

| 链接 | 关于 | 评论 |
| :--- | :--- | :--- |
| 首页 | 自2002年以来，TSS and Success 为运动员提供了一流的训练中心，帮助你实现目标。 | 感谢你的帮助！我已尽所力提高我的进度。我有目标，你帮助了我非常多。 |
| 游泳 | 有兴趣提高你的水平吗？加入我们吧。或者你只是想匹配你的目标？追求梦想为像我这样的运动员创造了支持性的环境。谢谢！ |
| 自行车 | | |
| 田径运动 | | |
| 商业世界 | | |
| 自行车杂志 | | |
| 自行车之旅 | | |
| 游泳世界 | | |
| Webathlon.com | | |
| 三项全锦 | | |

4. 这种这种类型样式的结果，浏览器将首先尝试加载 Verdana 字体，然后是 Geneva 字体。如果这两个字体都不可用，浏览器将加载它自己选择的通用字体。将此字体添加到页面正文样式规则中。

### 为页面正文指定字体族：

1. 回到编辑器中的 `tss.css` 文件。
2. 为 `body` 元素的样式规则添加以下样式：
`font-family: Verdana, Geneva, sans-serif;`

图 2-20 高亮显示了 `body` 元素的新样式。

![](img/bf90ebf56b5f948b05e7a26851204c31_134_0.png)

```
body {
  color: rgb(91, 91, 91);
  background-color: ivory;
  font-family: Verdana, Geneva, sans-serif;
}
```
