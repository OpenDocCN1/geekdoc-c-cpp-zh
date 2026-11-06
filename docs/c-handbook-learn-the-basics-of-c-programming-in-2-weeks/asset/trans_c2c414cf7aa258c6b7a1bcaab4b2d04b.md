
## 如何定义函数

你必须先定义函数，然后才能使用它们。定义函数最流行的方法涉及使用 **函数**（即 JavaScript 关键字）。输入 **函数** 后，指定你想要使用的名称和参数。然后，添加由大括号括起来的 JavaScript 语句块。

注意：你可以在不定义任何参数的情况下创建函数。因此，参数列表可能为空。

定义函数时必须使用的语法如下：

```html
<script type="text/javascript">
<!--
function functionname(parameter-list)
{
    statements
}
//-->
</script>
```

## 如何调用函数

在脚本中调用函数时，你只需指定函数名称。你可以使用下面的代码作为示例：

```html
<html>
<head>
<script type="text/javascript">
function sayHello()
{
    document.write ("Hello there!");
}
</script>
</head>

<body>
<p>click the following button to call the function</p>
<form>
<input type="button" onclick="sayHello()" value="Say Hello">
</form>

<p>Use different text in write method and then try...</p>
</body>
</html>
```

该代码将给出以下结果：

![](img/4fa8a5f30786d4f308acc92572dd6e8f_803_0.png)

## 函数的参数

到目前为止你看到的函数都没有参数。然而，在调用/执行函数时，你可以轻松地分配各种参数。你可以在函数内部捕获这些参数。捕获后，你可以根据需要修改这些参数。

## 返回语句

JavaScript 允许你在函数中添加 **返回** 语句。这个 **返回** 语句完全是可选的，尽管如果你想从函数中获取值，就必须使用它。通常，你应该将返回语句放在函数的最后一部分。

例如，你可以将两个值传递给你的函数。然后，你可以期望该函数将这些值相乘并在你调用的程序中显示结果。

## 嵌套函数

JavaScript 允许你将一个函数放在另一个函数内部。这个过程称为“嵌套函数”。作为一般规则，你不能在循环或条件语句内部包含函数定义。

下面的代码将教你如何嵌套自己的函数：

```html
<head>
<script type="text/javascript">
<!--
function hypotenuse(a, b) {
    function square(x) { return x*x; }

    return Math.sqrt(square(a) + square(b));
}
function secondFunction(){
    var result;
    result = hypotenuse(1,2);
    document.write ( result );
}
//-->
</script>
</head>

<body>
<p>Click the following button to call the function</p>

<form>
<input type="button" onclick="secondFunction()" value="Call Function">
</form>

<p>Use different parameters inside the function and then try...</p>
</body>
</html>
```

上面的代码给出以下结果：

![](img/4fa8a5f30786d4f308acc92572dd6e8f_805_0.png)

## 如何使用“Function()”创建函数

除了上面讨论的函数语句之外，你还可以使用 **函数()**（即 JavaScript 构造函数）和 **new**（即 JavaScript 运算符）创建函数。

要使用此构造函数，你必须使用以下语法：

```html
<script type="text/javascript">
<!--
var variablename = new Function(Arg1, Arg2..., "Function Body");
//-->
</script>
```

这种语法可以包含任意数量的字符串参数。最后一个参数充当函数体——它可能包含由分号分隔的任意语句。

重要说明：**函数()** 不为其生成的函数指定名称。程序员将这些未命名的函数称为“匿名”函数。

## 结论

再次感谢你下载这本书！

我希望这本书能够帮助你学习 JavaScript 的基础知识。

下一步是使用 JavaScript 编程语言编写自己的网页或程序。

最后，如果你喜欢这本书，我想请你帮个忙，你能为这本书在亚马逊上留下评论吗？将不胜感激！

[点击此处为本书在亚马逊上留下评论！](#)

感谢你，祝好运！

## 奖励：获取我提供的更多免费书籍！

感谢阅读我的书！我希望你从中获得了极大的价值。我想通过赠送更多免费书籍以及与编程和技术相关的信息来感谢你！

只需点击下面的链接并在我的网站上输入你的电子邮件地址！

如果你认真想提升编程技能，你将获得的一切对你都很有用。我将提供：

- 我写的更多书籍
- 我如何在创纪录的时间内学习编程
- 与编程相关的我最喜欢的产品信息
- 以及更多！

点击此处获取所有这些信息！

## Windows 10 学院

### 无压力学习 Windows 10 全面精通的方式

## 目录

- 引言
- 第1章：有什么新功能？
- 第2章：Cortana 的出现
- 第3章：使用开始菜单
- 第4章：管理设置
- 第5章：玩转功能
- 第6章：使用 Microsoft Edge
- 第7章：最大化 Windows 10 的使用
- 结论

## 奖励：获取我提供的更多免费书籍！

感谢阅读我的书！我希望你从中获得了极大的价值。我想通过赠送更多免费书籍以及与编程和技术相关的信息来感谢你！

只需点击下面的链接并在我的网站上输入你的电子邮件地址！

如果你认真想提升编程技能，你将获得的一切对你都很有用。我将提供：

- 我写的更多书籍
- 我如何在创纪录的时间内学习编程
- 与编程相关的我最喜欢的产品信息
- 以及更多！

[点击此处获取所有这些信息！](#)

## 第1章：有什么新功能？

Windows 10 最初你会注意到的事情之一是，虽然 Charms Bar 仍然存在，但你可以在没有它的情况下使用 Windows 10。

自从 Windows 8 创建以来，Charms Bar 就一直存在。然而，它的问题是很多人觉得它并没有真正有帮助，只是让界面变得混乱。

在 Windows 10 中，你只需隐藏 Charms Bar——但请先确保隐藏系统托盘图标。方法如下：

### 暂时隐藏托盘

隐藏系统托盘有两种方法。第一种是临时修复，方法如下：

- 1. 如果你看不到托盘中需要的全部项目，只需在箭头下方单击即可。
- 2. 现在，如果所有图标都已出现，请继续打开任务管理器（CTRL+ALT+DEL），然后终止 GWX/GWXUX 进程。

### 永久隐藏托盘

现在，如果你真的觉得永远不会使用托盘，你可以通过以下操作永久隐藏它：

- 1. *转到控制面板 > Windows 更新。*
- 2. 在屏幕左侧选择 *已安装的更新*，然后选择 *查看已安装的更新*。现在你会在屏幕顶部看到已安装的更新。
- 3. 当你看到标记为 *Update for Microsoft Windows KB3035583* 的更新时，继续将其删除。
- 4. 如果它再次出现，只需跳过此更新，以防万一。

### 隐藏 Charms Bar

然后，你可以继续隐藏 Charms Bar。

基本上，你只需单独选择 *设置*，而不是让它出现在 Charms 菜单中。通过点击 *设置*，你已经可以关闭 Charms Bar。

为了在没有 Charms Bar 的情况下访问完整设置，你需要执行以下操作：

- 1. 点击 *Charms* 栏。
- 2. 点击 *更改 PC 设置*。
- 3. 然后，访问你在 Windows 10 上会看到的第一个屏幕。
- 4. 点击开始按钮，以便显示新的开始菜单。
- 5. 点击 *设置* 链接。
- 6. 哇！你已准备就绪！

