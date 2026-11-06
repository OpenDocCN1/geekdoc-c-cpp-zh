
环境，等等）。上面显示的两个语句只是创建了两个值（即 0 和 false）。它们不会改变或改进任何东西。如果你执行这个程序，你不会观察到任何显著的现象。

## 变量

JavaScript 程序如何维持自身？它们如何存储事物？你已经看到如何使用旧值创建新值。然而，这个过程不会修改既有的值。你还需要立即使用产生的<|message|>值，否则它们就会简单地消失。为了捕获和保存值，JavaScript 提供了变量。

```
var example = 3 * 3;
```

在这个例子中，var（JavaScript 中的一个关键字）表示该行将创建一个变量。关键字后面跟着变量的名称，如果你想立即赋值，则后面跟着一个“ = ”符号和你想要的表达式。

该语句生成一个名为“ example ”的变量，并用它来存储 3 * 3 的乘积。

一旦你定义了变量，你就可以在未来的 JavaScript 语句中将其名称用作普通表达式。从该“ expression ”获得的值与你在创建时赋给它的值相同。请查看以下示例：

```
var three = 3;
console.log(three * three);
// -> 9
```

命名变量时，你可以使用任何不是关键字的词（例如 var）。你可以在变量名中包含数字，但不能用数字作为初始字符。例如，programming1 是有效的，但 1programming 不是。此外，你不能在命名变量时使用空格。就特殊字符而言，你只能使用美元符号（即 $）和下划线（即 _）。JavaScript 不允许你在变量名中使用标点符号。

你可以更改分配给变量的值。在 JavaScript 中，你只需在任何变量上使用“ = ”符号即可为其赋予新值。

```
var taste = "bitter";
console.log(taste);
// -> bitter
taste = "sweet";
console.log(taste);
// -> sweet
```

一般来说，你应该把变量想象成触手而不是容器。变量抓取值，它不包含它们。这意味着多个变量可以指向同一个值。

让我们分析一个简单的例子。你需要生成一个变量来记住约翰尼欠你的金额。当他付给你 $50 时，你必须为现有变量分配一个新值。请查看下面的行：

```
var JohnnysDebt = 200;
JohnnysDebt = JohnnysDebt - 50;
console.log(JohnnysDebt);
// -> 150
```

如果你在不分配值的情况下创建变量，它将被视为为空。如果你询问它包含的值，它会给你“ undefined ”。

JavaScript 允许你在一条 var 语句中包含多个变量。使用此功能时，你应该用逗号分隔变量。下面是一个示例：

```
var three = 3, four = 4;
console.log(three + four);
// -> 7
```

## JavaScript 中的保留字

如前所述，在命名变量时你不能使用关键字。然而，还有其他你不能用作变量名的词，因为 JavaScript 已为未来发展保留了它们。以下是这种脚本语言中的一些保留字：

- in, do, let, if, new, try, with, case, void, with, while, false, yield, extends, delete, default, const, debugger, class, break, finally, null, private, return, import, protected, switch, super, interface, instanceof, throw, implements

请记住，在定义变量时你不能使用上面给出的词。如果你忘记了这个简单的规则，在使用 JavaScript 程序时可能会遇到问题。

## JavaScript 环境

术语“environment”指的是活动值和变量的集合。基本上，在启动 JavaScript 程序时，环境不能为空。环境保存与语言本身相关的变量，并且通常，它们具有允许与计算机系统交互的变量。例如，在 Web 浏览器中，存在各种函数和变量来检查和影响当前网站并读取鼠标和键盘的输入。

## 函数

默认的 JavaScript 环境涉及函数。函数是与值链接的计算机程序片段。你可以应用这些值来激活链接的程序。例如，在浏览器环境中，alert（即一个变量）包含一个显示对话框的函数。下面是一个示例：

```
alert( "You are not authorized to access this page!" );
```

你可以通过在生成函数值的 JavaScript 表达式后放置括号来执行函数。通常，你会指出包含所需函数的变量的名称。通过将值括在括号中，你是将这些值分配给函数内的程序/。对于前面的示例，“alert”使用分配的字符串在 resulting 对话框中显示消息。程序员在指代分配给函数的 value/s 时使用术语“arguments”。

## “console.log”

当尝试新的字符串或语句时，你可以使用“alert”。然而，由于它要求你关闭 resulting 窗口，你可能会觉得它不方便且耗时。因为这个原因，你可能想使用本书前面各节中出现的函数：console.log。几乎所有 JavaScript 系统（例如 Node.js、Web 浏览器等）都提供此函数将参数传输到文本兼容的输出设备。

就 Web 浏览器而言，代码的输出进入 JavaScript 控制台。虽然浏览器的 GUI 的这一部分通常是隐藏的，但你可以通过按某些键来访问它（即对于 Windows 计算机，按 F12；对于 Mac 计算机，按 Command-Option-I）。如果你在查看此部分时遇到问题，你可以运行设备内搜索“developer tools”或“web console”。分析以下示例：

```
var a = 99;

console.log("one hundred minus one is", a);

// -> one hundred minus one is 99
```

如前所述，在命名变量时你不能使用句点或逗号。然而，上面给出的示例中包含一个。其原因在于 console.log 不是普通变量。它是一个 JavaScript 表达式，它从存储在“console”（它是一个变量）中的值中收集“log”信息。

## 返回值

在屏幕上写入信息和显示对话框框被称为副作用。由于这些副作用，函数在 JavaScript 语言中很重要。你也可以使用函数来生成值——在这种情况下，即使没有其副作用，函数也可能有用。例如，Math.max（一个 JavaScript 函数）接收无限数量的数值并指示其中最高的那个。下面是一个示例：

```
console.log(Math.max(1, 2, 3, 4, 5));
// -> 5
```

在 JavaScript 中，任何生成值的内容都被视为表达式。这意味着你可以在大型表达式中执行函数调用。在下面的示例中，你将使用 Math.min 函数作为“ + ”操作符的输入：

```
console.log(Math.min(1, 2) + 98);
// -> 99
```

## 第 4 章：关于 JavaScript 中函数的更多信息

在上一节中，你已经学习了如何创建和调用函数值。本章将帮助你进一步理解这个重要主题。根据专家程序员的说法，函数在使用 JavaScript 时是你的主要工具。函数是强大的工具，可以帮助你设计大型程序、最小化冗余、命名子程序并为每个子程序提供隔离。这意味着如果你想有效地使用 JavaScript，你必须掌握函数。本章将帮助你在两周内学习这种脚本语言。

许多人应用函数来定义新词汇。这意味着你可以用它们来创建单词并赋予含义。

一个平均的英语使用者词汇量约为 20,000 个词。好吧，编程语言通常没有那么多内置命令。这意味着编程中的词汇比人类语言使用的更精确。如果你想最小化冗余，你必须将自己的单词添加到 JavaScript 中并创建自己的词汇。
