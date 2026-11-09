
```html
<ul>
<li>Basics of html</li>
<li>CSS</li>
<li>JavaScript</li>
</ul>
</body>
</html>
```

## 这是我们得到的输出

![](img/443990a0ec620659ce8be783c0758bc6_127_0.png)

然后让我们将输出与代码中的标签关联起来。

![](img/443990a0ec620659ce8be783c0758bc6_127_1.png)

## 练习题

- 1. 创建一个介绍你自己的 HTML 网站。创建一个标题标签，内容为“自我介绍”。使用 h1 和 h2 标签为自己创建一个标题。然后创建一个段落，在其中谈论你自己、你的年龄、学校和家乡。最后，创建一个你爱好的项目符号列表。
- 2. 创建一个谈论你最喜欢的运动队或电视节目的 HTML 网站。创建一个标题标签，内容为节目/运动队的名称。使用 h1 和 h2 标签创建一个标题。然后创建一个段落，在其中谈论你为什么喜欢这个团队/电视节目，以及他们为什么如此棒。最后，创建一个你最喜欢的球员/节目中人物的项目符号列表。

## 灯泡示例 - HTML

### 本项目做什么

这是一个简单的 HTML 项目，它创建一个按钮，可以在页面上打开/关闭灯泡。我们将使用两张灯泡图片来实现这一点。按钮将在两张图片之间切换。

### 本章需要理解的概念

对于这个示例，我们需要理解按钮标签和图像标签。

### 按钮标签

```html
<button onclick=Action >Button text</button>
```

按钮元素有两个元素：动作和按钮文本。按钮文本是显示在按钮上的文本；动作是用户点击按钮时发生的事情。

### 图像标签

```html
<img id=ImageId src=ImageUrl style=ImageSize>
```

图像标签有三个元素。

ImageId 是你为图像指定的名称。这个名称用于在代码中引用图像。

ImageUrl 是标签所引用图像的 URL。如果图像与 HTML 文件位于同一文件夹中，那么你可以只使用文件名，而不使用完整 URL。

ImageSize 设置图像的宽度和高度。

### 文件

将灯泡打开和关闭的两张图像包含在我们使用的 HTML 代码的同一文件夹中。你可以点击下面的链接并下载来获取文件：

- [灯泡打开图片](#)
- [灯泡关闭图片](#)

点击“打开灯泡”按钮后：

### 使用 JavaScript 的灯泡

![](img/443990a0ec620659ce8be783c0758bc6_134_0.png)

灯泡关闭

灯泡打开

点击“关闭灯泡”按钮后：

### 使用 JavaScript 的灯泡

![](img/443990a0ec620659ce8be783c0758bc6_135_0.png)

灯泡关闭

灯泡打开

## 练习题：

- 1. 创建一个带有 2 个按钮的程序，按钮标题为“白天”和“夜晚”。当你点击“白天”按钮时，显示一张太阳的图片；当你点击“夜晚”时，显示一张月亮的图片。
- 2. 创建一个有 4 个按钮的程序，这些按钮在 4 种不同的野生动物之间切换。每个按钮的文本分别为“老虎”、“狮子”、“野猪”和“大象”。当你点击每个按钮时，显示相关的动物图片。

## 作者简短留言：

嘿，你喜欢这本书吗？我很想听听你的想法！

许多读者不知道评论多么难得，也不知道它们对作者有多大帮助。

![](img/443990a0ec620659ce8be783c0758bc6_137_0.png)

如果你能只花 60 秒在亚马逊上写一段简短评论，即使只有几句话，我也会无比感激！

[>> 点击这里留下快速评论](#)

感谢你抽出时间分享想法！你的评论会真正对我产生影响，并帮助我的作品获得曝光。

## HTML 表单

### 什么是 HTML 表单？

HTML 表单是网页上可以输入信息的空框。就是你在网上看到的那些输入姓名、年龄、密码等的表单。

表单看起来像这样：

![](img/443990a0ec620659ce8be783c0758bc6_139_0.png)

### 表单 HTML 标签格式

下面是一个表单 HTML 标签的示例，它接收姓名、职业和性别。

```html
<form id="form1">
Name: <input name="Enter Name" type="text" id="name" size="20"><br>
Occupation: <input type="text" id="occupation" size="20"><br>
Age: <input type="number" id="gender" size="20"><br>
</form>
```

运行程序后，输出如下所示。你可以在输出的空框中输入任何内容。空框也称为文本框。

![](img/443990a0ec620659ce8be783c0758bc6_140_0.png)

### 表单 HTML 标签的不同部分

`<form id="form1">`

表单 id 标签是表单的名称，将在其余代码中用作引用。

- `Name:`
- `Occupation:`
- `Age:`

这是写在框左侧的文本。它用于向用户描述应该在框中填写什么。

`input type="text"`

这意味着你在框中输入的内容是文本或字符串类型。例如，姓名和职业使用 text，因为你在框中输入字母。

`input type="number"`

这意味着你在框中输入的内容是数字。例如，年龄和电话会使用 number，因为它们完全是数字。

```
id="name"
id="occupation"
id="gender"
```

id 是框在程序其余部分中的名称。我们将在程序其余部分使用 id 来引用该框。

```
size="20"
```

这意味着框的长度是 20 像素。要更改这一点，请更改 size 的值。例如，如果你想把框的长度加倍，请将 size 改为 40。

## JavaScript 示例

### 什么是 JavaScript？

JavaScript 是一种高级编程语言。它最常用于在 HTML 页面上执行用户操作。它还有助于增强用户在网页上的交互。

### 如何在 HTML 中使用 JavaScript

在 HTML 页面上使用 JavaScript 有两种方式：

第一种方式是直接将 JavaScript 代码包含在 `<script>` 标签中。如下所示：

```html
<html>
<head>
<title> </title>
</head>
<body>
<script>
</script>
</body>
</html>
```

JavaScript 代码将位于上方以红色显示的两个 script 标签内。

第二种方式是创建一个 JavaScript 文件并将其保存为 .js 文件。然后你在 HTML 代码中引用该 JavaScript 文件。如下所示。

```html
<html>
<head>
<title> </title>
</head>
<body>
<script src="newfile.js"></script>
</body>
</html>
```

你将把所有 JavaScript 代码包含在 **newfile.js** 文件中。

## 你需要了解的 JavaScript 术语

接下来我们会看几个 JavaScript HTML 代码示例。我们需要了解以下术语才能理解代码。

### 函数

JavaScript 函数是执行任务的一组代码行。函数通常用于执行当用户点击 HTML 按钮时需要发生的任务。每个函数都有一个名称，并在 HTML 代码中被引用。示例如下：

```
function abcd()
```

abcd 是执行特定任务的函数名称。在 HTML 代码中将通过 abcd 引用它。

### 变量

变量用于在 JavaScript 中存储名称或数字。可以把它想象成一个只能存储一个值的盒子。每次需要该值时都会引用这个盒子。定义如下：

```
var flag=1;
```

`flag` 是变量的名称，它存储值 1。因此，每当在 JavaScript 程序中引用 `flag` 时，它的值都是 1（除非你更改 flag 的值）。这个 flag 的值可用于定义其他变量。例如：

```
var king=flag*2;
```

king 现在的值为 1*2=2。因此变量是处理未知量的好方法。

### document.getElementById().value

这个 JavaScript 术语用于获取 HTML 表单文本框中某一项的值。因此，如果你在表单文本框中填写姓名并点击按钮，document.getElementById() 会获取你在框中输入的值。例如：

```
var yname=document.getElementById("name").value;
```

“name”是在 HTML 中定义的表单文本框的 id。要了解这在 HTML 中如何实现，请查看上一章关于 HTML 标签的部分。文本框中输入的任何内容都会存储在名为 `yname` 的变量中。从现在起，在 JavaScript 中将通过 yname 引用它。

### Document.write()

此函数用于在网页浏览器上打印任何内容。
例如，

```
document.write("xyz");
```

在屏幕上打印 **xyz**

你还可以使用“+”按钮添加两个不同的项。

```
document.write("xyz"+"123");
```

在屏幕上打印 **xyz123**。
当你想向变量添加文本时，这很有用。例如。

```
var yname=document.getElementById("name").value;
document.write("My name is "+yname);
```

如果你在文本框中输入了“Matt”，它会在屏幕上打印出 **“我的名字是 Matt”**。
