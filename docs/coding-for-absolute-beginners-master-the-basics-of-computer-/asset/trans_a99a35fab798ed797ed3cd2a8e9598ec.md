
## 外边距与内边距

### 外边距

在 CSS 中，外边距属性用于在元素周围创建空间。我们可以为每个边设置不同的外边距大小。外边距属性具有不同的值，例如长度、宽度和外边距，由浏览器计算。

语法：

```css
body {
    margin: size;
}
```

### 内边距

CSS 内边距可用于定义边框或在元素周围创建空间。在 HTML 网站上，可以通过不同方式为各个边（如上、右、下和左）设置 CSS 内边距。内边距具有长度和宽度值，可使用以下 CSS 语法实现：

```css
body {
    padding: size;
}
```

## 字体与文本

### 字体

CSS 中的字体属性用于指定其他字体属性并设置内容的字体。CSS 中的不同字体属性包括字体样式、字体系列、字体粗细、字体变体、字体粗细和字体大小。
以下是每个字体属性的简单 CSS 语法：

### 字体样式

在线演示

```html
<html>
<head>
</head>

<body>
    <p style = "font-style:calibri;">
        This text will be rendered in calibri style
    </p>
</body>
</html>
```

### 字体系列

```html
<p style = "font-family: georgia, calibri, serif;">
```

### 字体变体

```html
<p style = "font-variant: small-caps;">
```

### 字体粗细

```html
<p style = "font-weight:500;">
```

### 字体大小

```html
<p style = "font-size:20px;">
    Font size 20 pixels
</p>
<p style = "font-size:small;">
    Small font
</p>
<p style = "font-size:large;">
    Large font
</p>
```

![](img/9d932bec53e523b8d8b7b8134cf77ca7_127_0.png)

## 文本

现在，使用 CSS 文本属性可以将文本转换为不同的颜色、样式和缩进。这些文本属性包括：

- **文本颜色：** 更改文本的颜色。
- **文本对齐：** 指定文本的水平或垂直对齐方式。
- **文本装饰：** 勾勒文本的装饰。
- **文本转换：** 控制文本的大小写。
- **文本缩进：** 指定首行的缩进。
- **字母间距：** 增加或减少单词之间的间距。
- **行高：** 指定行高。
- **文本方向：** 设置书写方向。
- **单词间距：** 设置单词之间的间距。
- **文本阴影：** 为文本添加阴影效果。

CSS 文本属性的语法：

文本颜色：

```css
body {
    color: Red;
}
```

文本对齐：

```css
h1 {
    text-align: center;
}

h2 {
    text-align: left;
}

h3 {
    text-align: right;
}
```

文本装饰：

```css
h1 {
    text-decoration: overline/underline/line-through;
}
```

### 文本转换

```css
p.uppercase {
  text-transform: uppercase;
}
```

```css
p.lowercase {
  text-transform: lowercase;
}
```

```css
p.capitalize {
  text-transform: capitalize;
}
```

### 文本缩进

```css
p {
    text-indent: 100px;
}
```

### 字母间距

```css
h1 {
  letter-spacing: 3px;
}
```

```css
h2 {
  letter-spacing: -3px;
}
```

### 行高

```css
p.small {
  line-height: 0.6;
}
```

```css
p.big {
  line-height: 1.6;
}
```

### 文本方向

```css
p {
    direction: rtl;
}
```

### 文本阴影

## 使用 CSS 创建简单表格的语法：

```html
<html>
<body>
<table class="Table" border = "1">
<tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Marks</th>
</tr>
<tr>
    <td>John</td>
    <td>Harry</td>
    <td>40</td>
</tr>
</table>
</body>
</html>
```

输出：

![](img/9d932bec53e523b8d8b7b8134cf77ca7_131_0.png)

### 边框合并

```html
<html>
    <head>
        <style type = "text/css">
            table.one {border-collapse:collapse;}
            table.two {border-collapse:separate;}

            td.a {
                border-style:dotted;
                border-width:3px;
                border-color:#000000;
                padding: 10px;
            }
            td.b {
                border-style:solid;
                border-width:3px;
                border-color:#333333;
                padding:10px;
            }
        </style>
    </head>
```

### 边框间距

```html
<html>
<head>
    <style type="text/css">
        table.one {
            border-collapse: separate;
            width:400px;
            border-spacing:10px;
        }
        table.two {
            border-collapse: separate;
            width:400px;
            border-spacing:10px 50px;
        }
    </style>
</head>

<body>

    <table class="one" border="1">
        <caption>Separate Border Table with border-spacing</caption>
        <tr><td>Cell A</td></tr>
        <tr><td>Cell B</td></tr>
    </table>
    <br />

    <table class="two" border="1">
        <caption>Separate Border Table with border-spacing</caption>
        <tr><td>Cell A</td></tr>
        <tr><td>Cell B</td></tr>
    </table>

</body>
</html>
```

输出：

### 带边框间距的分离边框表格

|  |
| --- |
| 单元格 A |
| 单元格 B |

### 带边框间距的分离边框表格

|  |
| --- |
| 单元格 A |
| 单元格 B |

### 标题侧属性的语法：

```html
<head>
  <style type = "text/css">
    caption.top {caption-side: top; }
    caption.bottom {caption-side: bottom;}
    caption.left {caption-side: left;}
    caption.right {caption-side: right;}
  </style>
</head>
```

### 空单元格属性的语法

```html
<head>
  <style type = "text/css">
    table.empty {
      width:350px;
      border-collapse:separate;
      empty-cells:hide;
    }
    td.empty {
      padding:5px;
      border-style:solid;
      border-width:1px;
      border-color:#999999;
    }
  </style>
</head>
```

### 表格布局的语法

```html
<head>
    <style type = "text/css">
        table.auto {
            table-layout: auto;
        }
        table.fixed {
            table-layout: fixed;
        }
    </style>
</head>
```

## 外边距

CSS 外边距属性用于在 HTML 元素周围创建空间或外边距。通过 CSS 可以通过不同属性设置元素外边距，例如 margin、margin-bottom、margin-top、margin-left 和 margin-right。实现外边距属性的语法：

```html
<p style = "margin: 10px; border:1px solid black;">
    all four margins will be 10px
</p>
```

## 列表、图标和下拉菜单

### 列表

CSS 中使用的列表有两种类型，称为有序列表和无序列表。在有序列表中，所有列表项都使用序号或字母标记，而在无序列表中，列表项通常使用项目符号标记。列表值可以通过使用 circle、decimal、lower-roman、upper-roman、decimal-leading-zero、lower-alpha、upper-alpha 和 square 等值来创建。

例如：

```html
<html>
    <head>
        <style>
            ul.a
            {
                list-style-type:square;
            }
            ol.c
            {
                list-style-type:lower-alpha;
            }
        </style>
    </head>
    <body>
            <h2>
    CSS ORDERED & UNORDERED LISTS
            </h2>
            <p>
                Unordered lists
            </p>
            <ul class="a">
                <li>one</li>
                <li>two</li>
                <li>three</li>
            </ul>
            <ul class="b">
                <li>one</li>
                <li>two</li>
                <li>three</li>
            </ul>
            <p>
                Ordered Lists
            </p>
            <ol class="c">
                <li>one</li>
                <li>two</li>
                <li>three</li>
            </ol>
            <ol class="d">
                <li>one</li>
                <li>two</li>
                <li>three</li>
            </ol>
    </body>
</html>
```

输出：

**CSS 有序与无序列表**

**无序列表**

- 一
- 二
- 三
- 一
- 二
- 三

**有序列表**

- a. 一
- b. 二
- c. 三
- 1. 一
- 2. 二
- 3. 三

### 图标

通过使用 HTML 中的图标库，我们还可以通过 CSS 添加不同类型的图标。这些类型的图标包括 Font Awesome 图标、Bootstrap 图标和 Google 图标。

