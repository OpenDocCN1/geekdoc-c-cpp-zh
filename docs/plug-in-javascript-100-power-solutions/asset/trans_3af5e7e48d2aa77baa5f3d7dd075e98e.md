

## 16 插件式 JavaScript：100 种解决方案

记住 HTML 的这两个部分属于同一个文档，将它们组合在一个 `<html>` 标签内部，如下所示：

```html
<html>
<head>
  <meta name="robots" content="index, follow" />
  <title>Hello</title>
</head>
<body>
  <a href="http://google.com">访问 Google</a>
  <form id="login" method="post" action="program.php">
    <input id="name" type="text" name="username" value="fred" />
    <input type="submit" />
  </form>
  <img src="photos/vacations/cancun/photoll.jpg" />
</body>
</html>
```

当然，一个页面的外观可能与此大不同，但它应该遵循相同的格式。尽管浏览器的兼容性很高，允许你省略很多内容（包括起始和结束标签），但我不建议你这样做，因为某一天你可能想将页面转换为 XHTML，后者的要求要严格得多。关闭每个标签并确保按顺序关闭总是一个好主意。例如，你不应该通过输出 `<html>` 后紧跟 `</body>` 来结束文档，这样标签的正确嵌套就会被破坏。

出于相同的原因，你还应该养成关闭没有结束标签的标签的习惯，例如 `<img src="*" />`，它没有匹配的 `<img>` 标签，因此在最后一个 `>` 之前需要一个 `/` 字符来正确关闭它。同样地，`<br>` 变成 `<br />`，以此此类推。

你还应该记住，为了兼容 XHTML，标签必须带有单引号或双引号，尽管几乎所有浏览器都允许你省略它们。

> [!NOTE] 注意
> 在 Web 早期，当大多数用户使用速度非常慢的拨号调制器时，经常看到网页上省略了各种内容，如引号和各种标签。如今，你的大多数用户将拥有相当不错的带宽速度，不再有理由这样做了。

## 从 JavaScript 访问 DOM

你可能奇怪，我为什么给给 ID 设置为 "login"，并给第一个输入标签命名为 "name"（以及值为 "fred"）。其原因是为了展示 JavaScript 如何通过点符号 `.` 非常轻松地处理所有的 DOM 嵌套。例如，可以像这样读取文档标题等标准属性：

```javascript
title = document.title
```

## 第 2 章：JavaScript、CSS、DOM

图 2-2
弹出窗口显示了输入值。

![](img/95e4c43b430487125c342550cc090977_37_0.png)

但为了访问其他对象属性，你需要为对象分配一个 ID。例如，一旦为字段分配了名称，你可以通过以下方式找到它的当前值（如果有），这种方式会将值赋值给变量 `username`：

```javascript
username = document.forms.name.value
```

在 `.name` 之后添加 `.value` 的原因（在上一个示例中 `.title` 之后没有添加）是因为 `.title` 已经是一个属性，而 `.name` 是一个表单对象，它本身拥有属性，包括位于 `.value` 中的值。

在输入语句中预填充值 "fred" 的原因，如果你在 `</body>` 结束标签之前添加以下四行代码，然后在浏览器中加载之前的示例，就会变得显而易见：

```html
<script>
document.write(document.title)
alert(document.forms.name.value)
</script>
```

浏览器随后将在缺失的图形图标之后显示 `document.title` 的值，因为图片 `photo1.jpg` 不存在，并且输入语句的当前值 "fred" 也会显示在弹出警框中（如图 2-2 所示）。

## 层级样式表 (CSS)

使用 CSS，你可以为网页应用样式，使其看起来完全符合你想要的样子。这之所以有效，是因为 CSS 与 DOM 连接在一起，因此你可以快速轻松地为任何元素设置样式。例如，如果你不喜欢 `<h1>`、`<h2>` 和其他标题标签的默认外观，你可以分配新样式来覆盖默认的字体族、大小设置，或者是否加粗或斜体以及许多其他属性。

## 插件式 JavaScript：100 种强力解决方案

为网页添加样式的主要方法与引入 JavaScript 类似；你可以在网页头部的 `<head>` 和 `</head>` 标签之间插入所需的语句。要更改 `<h1>` 标签的样式，你可以使用以下代码之一：

```css
<style>
h1 { color:red; font-size:3em; font-family:Arial }
</style>
```

在 HTML 页面中，这可能如下所示（见图 2-3）：

```html
<html>
<head>
  <style>
    h1 { color:red; font-size:3em; font-family:Arial }
  </style>
</head>
<title>Hello World</title>
<body>
  <h1>Hello there</h1>
</body>
</html>
```

或者，你可以使用包含样式表的常用方法之一，当你想要为整个网站而不是单个页面设置样式时，这种方法特别有用。在 HTML 页面中，这可能如下所示（见图 2-3）：

```html
<link rel="stylesheet" type="text/css" href="styles.css" />
```

在输入语句中预填充值 "fred" 的原因，如果你在 `</body>` 结束标签之前添加以下四行代码，然后在浏览器中加载之前的示例，就会变得显而易见：

```html
<script>
document.write(document.title)
alert(document.forms.name.value)
</script>
```

浏览器随后将在缺失的图形图标之后显示 `document.title` 的值，因为图片 `photo1.jpg` 不存在，并且输入语句的当前值 "fred" 也会显示在弹出警框中（如图 2-2 所示）。

在 `.name` 之后添加 `.value` 的原因（在上一个示例中 `.title` 之后没有添加）是因为 `.title` 已经是一个属性，而 `.name` 是一个表单对象，它本身拥有属性，包括位于 `.value` 中的值。

