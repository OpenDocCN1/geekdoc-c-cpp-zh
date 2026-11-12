

## Code 4.13 HTML 标签可以具有不同的属性，您可以根据元素的属性为其添加样式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice's Adventures in Wonderland</title>
<style type="text/css" media="all">
a { display: block; font-size: 2em;}
a[title] { color: red; }
a[title="Author"] {color: orange; }
a[title="white"] { color: yellow; }
a[title="illustrations"] { color: green; }
a[href~="http://"] {color: blue; }
a[href*="order"] { color: indigo; }
a[href$="css3-vqs"] {color: violet; }
</style>
</head>
<body class="chaptertext">
<article>About the Book:</article>
<ul>
<li><a href="index.html" title="Alice's Adventures in Wonderland">Alice's Adventures in Wonderland</a></li>
<li><a href="index.html">Wonderland</a></li>
<li><a href="index.html">Alice</a></li>
<li><a href="index.html" title="Illustrations black white">John Tenniel</a></li>
<li><a href="index.html" title="Illustrations full-color">Arthur Rackham</a></li>
<li><a href="http://www.jasonspeaking.com">Download Examples</a></li>
<li><a href="http://www.jasonspeaking.com/css3-vqs/order">More Info</a></li>
<li><a href="http://www.jasonspeaking.com/css3-vqs">Order The Book</a></li>
</ul>
</body>
</html>
```

只有当标签被赋予此属性时，无论其值如何，都会分配您声明的样式。

### 2. 如果字符串与属性的值完全匹配，则设置样式。

要根据属性的精确值设置样式，请键入要设置样式的选择器（HTML、类或 ID）、左方括号 ([)、要检查的属性名称、等号 (=)、引号中的要测试的值 ('...')，以及右方括号 (])。值区分大小写。

```
a[title='home'] {...}
```

只有当标签被赋予此属性且具有精确的指定值时，才会分配您声明的样式。

### 3. 如果字符串在空格分隔的值列表中，则设置样式。

要根据属性的值（该值位于空格分隔的值列表中，例如句子中的某个特定单词）设置样式，请键入要设置样式的选择器（HTML、类或 ID）、左方括号 ([)、要检查的属性名称、波浪号 (~)、等号 (=)、引号中的要测试的值 ('...')，以及右方括号 (])。

```
a[title~="email"] {...}
```

只有当标签被赋予此属性且其值作为空格分隔列表的一部分包含该字符串时，才会分配您声明的样式。通常，这意味着它是句子中的一个单词。部分单词不计入。因此，在此示例中，测试 'mail' 将不起作用。

### 4. 如果字符串在分配给属性的连字符分隔值列表中，则设置样式。要根据属性的值作为连字符分隔列表中的第一个值来设置样式，请键入要设置样式的选择器（HTML、类或 ID）、左方括号 ([)、要检查的属性名称、竖线 (|)、等号 (=)、引号中的要测试的值 ('...')，以及右方括号 (])。

```
a[title|="resume"]
```

只有当标签被赋予此属性且其值在连字符分隔列表的开头包含该字符串时，才会分配您声明的样式。通常，这用于为语言设置样式，作为使用语言伪类的替代方案。

### 5. ★如果字符串是值的前缀，则设置样式。要根据属性开头的值设置样式，请键入要设置样式的选择器（HTML、类或 ID）、左方括号 ([)、要检查的属性名称、插入符号 (^)、等号 (=)、引号中的要测试的值 ('...')，以及右方括号 (])。

```
a[href^="http://"]
```

只有当值字符串在引号中完全按原样出现在属性值的开头时，才会分配您声明的样式。

### 6. ★如果字符串是属性值的后缀，则设置样式。要根据属性的值作为连字符分隔列表中的第一个值来设置样式，请键入要设置样式的选择器（HTML、类或 ID）、左方括号 ([)、要检查的属性名称、美元符号 ($)、等号 (=)、引号中的要测试的值 ('...')，以及右方括号 (])。

```
a[href$=".info"]
```

只有当值出现在属性值的末尾时，才会分配您声明的样式。

### 7. 如果字符串在属性值的任何位置，则设置样式。要根据属性的值作为连字符分隔列表中的第一个值来设置样式，请键入要设置样式的选择器（HTML、类或 ID）、左方括号 ([)、要检查的属性名称、星号 (*)、等号 (=)、引号中的要测试的值 ('...')，以及右方括号 (])。

```
a[href*="speakinginstyles"]
```

如果值出现在属性值的任何位置，则会分配您声明的样式。

值区分大小写。换句话说，'Alice' 和 'alice' 是两个不同的值。

## ★查询媒体

在第 3 章中，您学习了如何为特定媒体类型指定样式表，从而可以根据 HTML 是输出到屏幕、打印、电视、手持设备或其他设备来设置样式（表 4.7）。CSS3 添加了一项重要的新功能，允许您根据常见界面属性（如宽度、高度、宽高比和可用颜色数量）设置样式。

媒体查询和 @media 规则可用于定制您的页面，不仅针对一般设备类型，还针对网站访问者使用的特定设备。这包括针对打印、移动设备的大小调整，或以最佳适应打开的浏览器窗口的大小。

### 媒体查询

如果您想知道浏览器窗口的当前大小，为什么不直接询问浏览器呢？JavaScript 赋予您这种能力，但这是一种获取设计试图适应的 Web 环境基本事实的笨拙方式。

媒体查询为您提供了几个可测试的常见媒体属性（4），然后交付最适合环境的样式表。

尽管媒体查询具有许多属性（表 4.8），但它们有五种基本类型：

- 宽高比查找以比率表示的设备相对尺寸，例如 16:9。

- 宽度和高度查找显示区域的尺寸。这些也可以表示为最大值和最小值。

| 值 | 用途 |
|---|---|
| screen | 计算机显示器 |
| tty | 电传打字机、计算机终端和旧式便携设备 |
| tv | 电视显示器 |
| projection | 投影仪 |
| handheld | 便携式电话和 PDA |
| print | 纸张 |
| braille | 盲文触觉阅读器 |
| speech | 语音合成器 |
| all | 所有设备 |

```
media="
screen
and (min-width: 740px)
and (max-width: 980px)"
```

媒体查询的一般语法。

### 表 4.8 媒体查询属性

| 属性 | 值 |
|---|---|
| aspect-ratio | <ratio> |
| max-aspect-ratio | <ratio> |
| min-aspect-ratio | <ratio> |
| device-aspect-ratio | <ratio> |
| max-device-aspect-ratio | <ratio> |
| min-device-aspect-ratio | <ratio> |
| color | <integer> |
| max-color | <integer> |
| min-color | <integer> |
| color-index | <integer> |
| max-color-index | <integer> |
| min-color-index | <integer> |
| device-height | <length> |
| max-device-height | <length> |
| min-device-height | <length> |
| device-width | <length> |
| max-device-width | <length> |
| min-device-width | <length> |
| height | <length> |
| max-height | <length> |
| min-height | <length> |
| monochrome | <integer> |
| max-monochrome | <integer> |
| min-monochrome | <integer> |
| orientation | portrait, landscape |
| resolution | <resolution> |
| max-resolution | <resolution> |
| min-resolution | <resolution> |
| scan | progressive, interlaced |
| width | <length> |
| max-width | <length> |
| min-width | <length> |

- 方向查找 *横向*（高度大于宽度）或 *纵向*（宽度大于高度）布局。这允许您为可以翻转的设备定制设计。

- 颜色、颜色索引和单色查找颜色数量或每种颜色的位数。这些允许您为黑白移动设备定制设计。

- 分辨率查看输出中的像素密度。当您想要利用分辨率高于 72 dpi 的显示设备时，这尤其有用。

默认情况下，媒体查询针对视口（有关视口的详细信息，请参见第 11 章），但指定 *设备* 的查询除外，在这种情况下，它们针对整个屏幕或输出区域。例如，width 是屏幕内可见浏览器视口的宽度，而 device-width 是整个屏幕的宽度。

