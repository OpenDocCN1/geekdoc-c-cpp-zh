

![](img/9d932bec53e523b8d8b7b8134cf77ca7_104_0.png)

## 第八章

### HTML

#### 引言与概述

超文本标记语言（HTML）是一种标准标记语言，用于创建网站，以显示颜色、字体、图形、媒体和图像。HTML 由不同的标签组成，这些标签可用于描述网页的结构，并告知浏览器通过互联网显示内容。

#### 什么是标签？

标签为 Web 浏览器提供有关任何网页的结构、显示和内容的指令。由于标签通过尖括号 `<>` 包围定义，因此标签由属性和元素组成。元素是页面上的对象，而属性描述该元素的质量或细节。请记住，标签应成对使用：开始标签 `<tag>` 和结束标签 `</tag>` 通过斜杠来区分。

你可以使用以下标签创建第一个示例 HTML 网页：

```html
<html>
<head>
</head>
<body>
<h1>My First Heading</h1>
<p>My first paragraph</p>
</body>
</html>
```

#### 标签说明

在上述 HTML 文档中，`<html>` 标签包含整个 HTML 文档，并由其他主要标签组成，包括 `<head>`、`<body>` 和 `<p>`。`<head>` 标签表示文件的头部，而 `<title>` 标签用于显示文档的标题。`<body>` 包含多个其他标签，用于创建网页，例如标题 `<h1>` 和段落 `<p>`。

HTML 标签不区分大小写，但应使用小写形式。要定义 HTML 的版本，我们可以使用以下标签：

```html
<!DOCTYPE html>
```

初学者可以在 PC 上使用记事本运行 HTML 页面，并将文件保存为 `.html` 格式。这样他们就可以在浏览器中查看网页。

#### 基本标签和属性

##### 基本标签

每个 HTML 文档都应从标题、标题和段落开始。在 `<body>` 标签之后，下一个要使用的主要标签是 `<h1>` 或标题标签。根据你的内容需求，标题标签使用 `<h1>` 到 `<h6>` 定义。例如：

标题：

```html
<html>
<body>
<h1> First heading </h1>
<h2> Second heading </h2>
<h3> Third heading </h3>
<h4> Fourth heading </h4>
<h5> Fifth heading </h5>
<h6> Sixth heading </h6>
</body>
</html>
```

输出：

![](img/9d932bec53e523b8d8b7b8134cf77ca7_106_0.png)

##### 段落

要添加内容，我们需要在 HTML 文档中包含段落。  
例如：

```html
<html>
<head>
<h1> heading </h1>
</head>
<body>
    <p> First Paragraph </p>
    <p> Second Paragraph </p>
</body>
</html>
```

输出：

**heading**

First Paragraph

Second Paragraph

要在段落之间添加换行，我们可以使用换行标签 `<br>`。

##### 摘要标签

要为段落添加摘要，带有 Summary 标签的 HTML 语法定义如下：

```html
<details>
    <summary>Sample Text</summary>
    <p> Web development tutorials</p>
</details>
```

##### Span

span 标签用于为文本的特定部分着色。例如：

```html
<p> Web development is <span style="color:red"> interesting </span> to learn </p>
```

##### Select

select 标签用于从下拉列表中选择一个选项。例如：

```html
<select>
    <option value="Red">Red</option>
    <option value="Blue">Blue</option>
    <option value="Green">Green</option>
    <option value="White">White</option>
</select>
```

##### Thead

thead 标签用于创建组标题内容，并与 `<tbody>` 和 `<tfoot>` 元素一起使用。例如：

```html
<table>
<thead>
    <tr>
        <th>Course</th>
        <th>Max Marks</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td>Web Engineering</td>
        <td>85</td>
    </tr>
    <tr>
        <td>English</td>
        <td>90</td>
    </tr>
</tbody>
<tfoot>
    <tr>
        <td>Sum</td>
        <td>$180</td>
    </tr>
</tfoot>
</table>
```

| Course | Max Marks |
|---|---:|
| Web Engineering | 85 |
| English | 90 |
| Sum | $180 |

#### 格式化标签

HTML 文档中的文本可以格式化为不同的样式、字体和大小。用于格式化文本、标题、段落和表格的标签如下：

##### 粗体

写在 `<b>` 和 `</b>` 标签之间的任何文本都以粗体样式显示。例如：

```html
<p> <b> Web development </b> is interesting </p>
```

输出：**Web development** is interesting

##### 斜体

写在 `<i>` 和 `</i>` 之间的任何文本都以斜体样式显示。例如：

```html
<p> <i> Web development is interesting </i> </p>
```

输出：*Web development is interesting*

##### 上标/下标

要以上标形式显示内容，我们可以使用 `<sup>...</sup>` 标签，而 `<sub>` 和 `</sub>` 标签用于添加下标。例如：

```html
<p>This text uses a <sup>superscript</sup></p>
```

输出：The following word uses a <sup>superscript</sup>

##### 下划线

写在 `<u>` 和 `</u>` 标签之间的文本带有下划线。

```html
<p><u>Sample text</u></p>
```

输出：<u>Sample text</u>

##### 插入和删除标签

要插入内容，使用 `<ins>` 和 `</ins>` 标签；而要删除任何文本，我们可以使用 `<del>` 和 `</del>` 标签。

##### 链接

要在文本中添加链接，我们可以使用以下标签：

```html
<p><a href="document location"></a></p>
```

##### Marquee 标签

`<marquee>` 标签可以与不同的属性一起使用，包括 width、height、direction、behavior、scrollamount、scrolldelay、loop、bgcolor、hspace 和 vspace。marquee 标签的演示：

```html
<html>
    <head>
        <title>HTML marquee Tag</title>
    </head>
    <body>
        <marquee>Sample text</marquee>
    </body>
</html>
```

##### 容器标签

在 HTML 中，以下容器标签用于格式化文本：

| 开始标签 | 结束标签 | 功能 |
|---|---|---|
| `<p>` | `</p>` | 段落 |
| `<span>` | `</span>` | 在段落内添加内联内容 |
| `<em>` | `</em>` | 用于强调文本 |
| `<ol>` | `</ol>` | 有序列表（数字） |
| `<ul>` | `</ul>` | 无序列表（项目符号） |
| `<li>` | `</li>` | 列表项 |

#### 表格、图像和框架

##### 表格

表格是任何网站的重要组成部分，因为它们帮助我们以适当的方式说明和详细阐述关键信息。在 HTML 中，有预定义的标签可用于创建和设计表格。

###### 在 HTML 中创建表格的标签

要创建表格，我们可以使用以下标签：

```html
<table>…..</table>
```

**表格行**

用于创建表格行的标签：

```html
<tr>….</tr>
```

**表头**

`<th>… </th>`。用于创建表格以显示数据的示例属性是 `scope="row"` 和 `scope="column"`，因为它们定义了给定标签是用于行标题还是列标题。

**表格数据单元格**

`<td>…</td>`。表格数据单元格的属性是 `colspan="number"` 和 `rowspan="number"`，我们需要将标签与 `<th>` 或 `<td>` 元素一起使用，以使单元格跨越多行和多列。

##### 图像

图像是任何网站的重要组成部分。由于它们帮助我们更好地说明概念、服务和信息，因此在 HTML 中插入和管理图像非常简单。

用于插入图像的标签：

```html
<img src="Image URL" />
<img src="desktop/images/image1.png" alt="Sample Image" />
```

要设置图像的特定高度和宽度，可以使用以下语法：

```html
<img src="desktop/images/image1.png" alt="Sample Image" width="100" height="100" />
```

##### 视频

要在 HTML 网页中添加视频，可以使用 `<video>` 标签，语法如下：

```html
<video>
    <source src="Samplevideo.mp4" type="video/mp4">
</video>
```

##### 对齐和边框

在网页上对齐图像有三种位置，称为居中、右和左。为此，我们可以使用 align 属性。例如：

```html
<img src="desktop/images/image1.png" alt="Sample Image" align="center" />
```

要创建图像边框，属性是 border。例如：

```html
<img src="desktop/images/image1.png" alt="Sample Image" border="4" />
```

##### 框架

在超文本标记语言中，添加框架是为了在浏览器窗口中创建多个部分，以便每个部分都可以加载独立的 HTML 文档。要在网页中使用框架，应使用 `<frameset>` 标签代替 `<body>` 标签，然后可以使用特定的 rows 和 cols 属性进行定义。

用于创建框架的示例 HTML 标签：

```html
<html>
    <head>
        <title>HTML Frames</title>
    </head>
```

