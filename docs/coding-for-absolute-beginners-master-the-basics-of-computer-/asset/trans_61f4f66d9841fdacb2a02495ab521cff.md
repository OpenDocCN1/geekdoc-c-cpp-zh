
```html
<frameset rows = "10%,80%,10%">
    <frame name = "top" src = "/html/top_frame.htm" />
    <frame name = "main" src = "/html/main_frame.htm" />
    <frame name = "bottom" src = "/html/bottom_frame.htm" />

    <noframes>
    <body>Your browser does not support frames.</body>
    </noframes>

</frameset>
</html>
```

### iFrame

要创建嵌套浏览上下文，可以使用 iFrame 标签将新的 HTML 文档添加到现有文档中。要创建 iFrame，可以配合 `<iframe>` 标签使用以下语法：

```html
<iframe src="https://www.samplewebsite.com"></iframe>
```

基本 HTML 标签完整表格：

|  |  |  |  |  |
|---|---|---|---|---|
| `<a>` | `<abbr>` | `<acronym>` | `<address>` | `<applet>` |
| `<area>` | `<article>` | `<aside>` | `<audio>` | `<b>` |
| `<base>` | `<basefont>` | `<bdi>` | `<bdo>` | `<big>` |
| `<blockquote>` | `<body>` | `<br>` | `<button>` | `<canvas>` |
| `<caption>` | `<center>` | `<cite>` | `<code>` | `<col>` |
| `<colgroup>` | `<data>` | `<datalist>` | `<dd>` | `<del>` |
| `<details>` | `<dfn>` | `<dialog>` | `<dir>` | `<div>` |
| `<dl>` | `<dt>` | `<em>` | `<embed>` | `<fieldset>` |
| `<figcaption>` | `<figure>` | `<font>` | `<footer>` | `<form>` |
| `<frame>` | `<frameset>` | `<h1> - <h6>` | `<head>` | `<header>` |
| `<hr>` | `<html>` | `<i>` | `<iframe>` | `<img>` |
| `<input>` | `<ins>` | `<kbd>` | `<label>` | `<legend>` |
| `<li>` | `<link>` | `<main>` | `<map>` | `<mark>` |
| `<meta>` | `<meter>` | `<nav>` | `<noframes>` | `<noscript>` |
| `<object>` | `<ol>` | `<optgroup>` | `<option>` | `<output>` |
| `<p>` | `<param>` | `<picture>` | `<pre>` | `<progress>` |
| `<q>` | `<rp>` | `<rt>` | `<ruby>` | `<s>` |
| `<samp>` | `<script>` | `<section>` | `<select>` | `<small>` |
| `<source>` | `<span>` |  | `<strong>` | `<style>` |
| `<sub>` | `<summary>` | `<sup>` | `<svg>` | `<table>` |
| `<tbody>` | `<td>` | `<template>` | `<textarea>` | `<tfoot>` |
| `<th>` | `<thead>` | `<time>` | `<title>` | `<tr>` |
| `<track>` | `<tt>` | `<u>` | `<ul>` | `<var>` |
| `<video>` | `<wbr>` |  |  |  |

## 表单

HTML 表单是网站与用户之间交互的关键方面之一。表单通过使用文本字段、按钮、选择框、单选按钮、文件选择框、隐藏控件和可点击控件等小部件来创建。通过表单收集的数据会发送到 Web 服务器，网页也可以自行拦截这些数据。大多数情况下，小部件会与标签关联，以描述其用途。

在 HTML 中创建表单的语法：

```html
<form action = "Script URL" method = "GET|POST">
    form elements like input, buttons etc.
</form>
```

用于从用户处获取姓名和年龄的输入表单：

```html
<html>

    <head>
        <title>My first HTML form</title>
    </head>

    <body>
        <form>
            Name: <input type = "text" name = "Name" />
            <br>
            Age: <input type = "text" name = "last name" />
        </form>
    </body>
</html>
```

输出：

![](img/9d932bec53e523b8d8b7b8134cf77ca7_114_0.png)

### 文本字段

HTML 中的文本字段允许用户向表单中输入文本。创建文本字段的通用语法定义如下：

```html
<input type = "text" value = "text">
```

### 按钮控件

向表单提交数据有不同的方式。我们可以使用以下 HTML 标签添加可点击按钮：

```html
<input type = "submit" name = "submit" value = "Submit" />
<input type = "reset" name = "reset" value = "Reset" />
<input type = "button" name = "button" value = "button" />
```

输出：

![](img/9d932bec53e523b8d8b7b8134cf77ca7_114_1.png)

### 选择框

要在 HTML 表单中创建下拉列表，我们可以使用 `<select>` 和 `<option>` 元素。

例如：

```html
<html>
    <head>
        <title>File Upload Box</title>
    </head>
    <body>
        <form>
            <label for="Course">Course:</label>
            <select name="Course" id="course">
                <option value="Web Engineering">Web Engineering</option>
                <option value="Calculus">Calculus</option>
                <option value="Data Science">Data Science</option>
            </select>
        </form>
    </body>
</html>
```

输出：

![](img/9d932bec53e523b8d8b7b8134cf77ca7_115_0.png)

### 选择框

Select Box 元素提供了一种在 HTML 表单中列出多个选项的方式。

例如：

```html
<html>
    <head>
        <title>Select your course</title>
    </head>

    <body>
        <form>
            <select name = "dropdown">
                <option value = "Math" selected>Math</option>
                <option value = "Physics">Physics</option>
            </select>
        </form>
    </body>
</html>
```

输出：

![](img/9d932bec53e523b8d8b7b8134cf77ca7_116_0.png)

### 表单元素

HTML 表单完成后，需要使用 Action 和 Method 两个属性来存储和发送表单数据。Action 包含定义表单数据将发送到哪里的地址，而 Method 可以是 GET 或 POST，因为它定义了如何处理表单信息。创建 Form 元素的语法定义如下：

```html
<form action = "/login" method = "POST">
```

## 设计

在 HTML 中，任何网页的默认背景颜色都是白色。要更改背景颜色，可以使用以下标签和属性：

```html
<tagname bgcolor = "color value/color name">
```

例如：

```html
<table bgcolor = "green">
<table bgcolor = "#f1f1f1">
```

### 字体

字体是任何网站的重要组成部分，并能增强内容的可读性。可以使用 `<font>` 标签为文本指定特定的样式、大小和颜色，其属性包括 size、color 和 face。

要设置字体大小，标签和属性为：

```html
<font size = "14"> Text </font>
```

字体名称标签和属性：

```html
<font face = "Times New Roman" size = "14"> Text </font>
```

### 字体颜色

要更改字体颜色，可以使用以下 HTML 标签和属性：

```html
<html>
    <head>
        <title>Setting Font Color</title>
    </head>

    <body>
        <font color = "Blue">This text is blue</font>
    </body>
</html>
```

输出：**这段文字是蓝色的**

### 标记文本

写在 `<mark>` 和 `</mark>` 元素之间的文本会以黄色标记显示。

例如：

```html
<p> This text is marked as <mark> Yellow </mark> </p>
```

输出：这段文字被标记为**黄色**。

### 元标签

在 HTML 中，元标签可用于向网页添加元数据。元标签的属性包括 Name、Content、Scheme 和 http-equiv。我们可以使用 `<meta>` 标签为文档提供简短描述，这也可以改善网页的搜索引擎索引。

例如：

```html
<html>

    <head>
        <title>Meta Tags Example</title>
        <meta name = "keywords" content = "HTML, Meta Tags, Metadata" />

        <meta name = "description" content = "Meta Tags." />
        <meta name = "revised" content = "3/7/2019" />
        <meta http-equiv = "cookie" content = "userid = abc; expires = Monday, 08-Sep-19 23:59:59 GMT;" />

    </head>
    <body>
        <p>Welcome to HTML</p>
    </body>

</html>
```

### 注释

要在 HTML 代码中添加注释，可以遵循以下语法：

```html
<html>
    <head> <!-- Document Header Starts -->
        <title>Document title</title>
    </head> <!-- Document Header Ends -->
    <body>
        <p>Document content goes here.....</p>
    </body>
</html>
```

### HTML 样式表

为了进一步设计 HTML 文档，网站中会使用层叠样式表（CSS）。它们为指定网站的某些属性提供了简单、有效且易于管理的替代方案。我们将在下一章详细讨论 CSS。

### 布局与响应式设计

HTML 包含多种语义元素，用于定义网页的不同部分。这些元素包括 Header、Container、Section、Article、Aside、Details 和 Footer。尽管 CSS 是设计网页布局的最佳方法，但我们也可以通过这些 HTML 元素完成该过程。

响应式网页设计是通过使用 HTML 和 CSS 创建的。此过程会自动调整网站大小并进行调整，使其在桌面电脑、智能手机和平板电脑等所有设备上都看起来合适。有关响应式的更多详细信息，学习 CSS 和 Bootstrap 语言将大有裨益。

