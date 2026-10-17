
# C# 编程：快速学习 C# 编程

## 引言

看到数字、字母和符号如何汇聚驱动我们的计算机，是一件非常趣的事情。如果你一直有一个编写计算机程序的想法，现在就是你学习编码的时候了。通过 C#，你成为程序员的梦想可以实现。而且由于 C# 易于理解，这一过程并不会让你感到沮丧。

在本书中，你将学习 C# 编码的基础知识。本书的编写方式即使是让那些零编程基础的人也能读懂。如果你一直认为编程很困难，这本书将证明你是错的。书内有大量的示例来加深你的理解。当你读到最后一页时，你应该能够创建简单的 C# 程序了。

那么，我们可以开始了。如果你还没有打开电脑，请启动它。如果你在书开头不理解某些内容，请继续往下看——随着学习的深入，事情会变得越来越明朗。

## 第1章：C# 101

C#，发音为“C sharp”，是一种通用的面向对象的编程语言。它的优点之一是易于学习、创建高效程序，并且可以在多个系统上编译。它是 `.Net` 框架的一部分。出于这个原因，有些人将其称为 `.Net` 语言。C# 是由微软开发的，这要归于 Anders Helsberg 的一人。

由于它的名字听起来像 C 和 C++，你可能会认为 C# 类似于上述两种语言。事实确实如此。但 C# 进一步模仿了 Java 提供的大部分功能。

如果你已经了解 C 或 C++，那么 C# 将证明非常容易上手。

有了 C#，你可以自由创建 C、C++、Java 以及其他高级编程语言可以生成的程序。你可以创建游戏、Windows 应用程序、Web 应用程序以及 iOS 和 Android 应用程序。

### 设置正确的环境

为了创建 C# 程序，你需要正确的工具。你的计算机是这个环境中最最重要的工具。但你在软件方面还需要其他东西。

#### .Net 框架

我已经提到过 C# 是 `.Net` 框架的一部分。因此，你的计算机需要它来执行 C# 代码。如果你使用的是 Windows 电脑，那么你可能已经安装了 `.Net` 框架。

#### 集成开发环境 (IDE)

微软公司提供了 `Visual Studio` (VS) 作为创建 C# 应用程序以及 C++ 等其他语言的 IDE。通过 VS，你可以创建想象中的任何种应用程序。你可以从微软网站免费下载 VS。

#### Mac OS 和 Linux 上的 C#

`.Net` 框架不适用于 Mac OS 和 Linux。坦率地说，有一个名为 `Mono` 的开源替代方案。它带有一个 C# 编译器。访问 Go Mono 网站了解更多信息。

## 第2章：首个程序与基础语法

### Hello, World!

正如每种编程语言一样，我们将从 Hello World 程序开始练练手。请注意，书中的示例使用的是 `Microsoft Visual C# 2010 Express`，这是 `Visual Studio` 的精简版本。

首先，启动 `Visual C#`。点击 `File`（文件），选择 `New Project`（新建项目），然后选择 `Console Application`（控制台应用程序）。在我的情况下，这将打开一个名为 `Program.cs` 的文件编辑器。

由于编辑器中有些代码，按 `F5` 运行。一个窗口会快速打开并关闭。那是因为代码没有具体的要做的操作。我们需要向它添加更多内容来创建一个“Hello World”程序。它看起来是这样的：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // 我的第一个 C# 程序
            Console.WriteLine("Hello, World!");
            Console.ReadLine();
        }
    }
}
```

注意我添加的那三行了吗？绿色部分的那行，以及紧随其下的一行。当你再次按 `F5`，你会得到如下输出：

```text
Hello, World!
```

#### 解释

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

`using` 是一个用于导入命名空间的关键字。在这种情况下它导入了 `System`。

```csharp
namespace ConsoleApplication1
```

这行代码包含了命名空间声明，在这种情况下是 `ConsoleApplication1`。

```csharp
class Program
```

`class` 是另一个引入类的关键字。在类关键字之后，你可以编写类名，在这种情况下是 `Program`。每个程序必须包含一个类。C# 代码包含在花括号中。

```csharp
static void Main(string[] args)
```

这是程序的入口点，意味着这是程序执行的第一部分。`static` 表示该方法无需实例即可访问。`Void` 表示该方法不返回任何，在这种情况下是空值。

```csharp
// 我的第一个 C# 程序
```

这是一个注释。编译器会忽略它。注释可以帮助你在忘记时记住你的代码的功能。它们会告诉他人你打算通过代码实现什么。双斜线开头的注释限于单行。如果你有跨行的注释，请在星号内进行格式化（`/* */`）。

```csharp
Console.WriteLine("Hello, World!");
```

`Console.WriteLine` 让你能够在控制台输出数据。要显示的数据位于括号内。

```csharp
Console.ReadLine();
```

当程序执行 `Console.WriteLine` 语句时，控制台窗口会打印“Hello, World!”如果没有 `Console.ReadLine()`，窗口会像打开时一样迅速关闭：你甚至看不到你的文本。`Console.ReadLine()` 欺骗程序使其保持开启，直到你提供输入。

你可能注意到我们的代码包含空行和空白。这些是为了代码的可读性。

你必须知道 C# 是区分大小写的。因此 `Main` 和 `main` 不是同一个。还要知道在每个语句或表达式之后，你必须写分号（`;`）。

由于某些原因不想使用 `Visual C#`，可以在文本编辑器中编码。这是创建一个 Hello World 程序：

- 将 Hello World 代码复制到记事本等文本编辑器中
- 将文件保存为 `helloworld.cs`
- 打开命令行并导航到保存文件的文件夹
- 输入 `csc helloworld.cs`
- 如果正确，命令行将创建一个程序的执行文件
- 输入 `helloworld` 运行它

### 标识符与关键字

#### 标识符

这些是你为命名空间、类、变量、方法等分配的名字。你可以使用字母、数字和下划线来创建标识符。然而，标识符只能以字母或下划线开头。如果你想将关键字作为标识符，请在开头包含 `@` 符号（例如 `@class`）。

以下是有效标识符的其他示例：

- `FIRST`
- `first`
- `fir_st`
- `FirstName`
- `_123names`

## 第3章：变量与数据类型

变量在 C# 中非常重要，因为你使用它们来存储数据（值）。在给变量赋值时，你需要指定该变量的数据类型。C# 是一种类型安全的语言，这意味着每个变量都持有相应类型的数据。

以下是声明变量的方法：

`data_type variable_name;`

或者

`data_type variable_name = value;`

`=` 符号是赋值运算符。你将使用它来给变量赋值。以下是声明变量并赋值的方法：

```csharp
static void Main(string[] args)
{
    string message;
    // 在变量声明后赋值
    message = "Hello World!!";

    Console.WriteLine(message);
    Console.ReadLine();
}
```

`string` 是数据类型，`message` 是变量。`message` 持有的值在注释后的行中被赋值，值为 `Hello World!!`。

但你也可以在同一行声明变量并为其赋值：

```csharp
static void Main(string[] args)
{
    string message = "Hello World!!";

    Console.WriteLine(message);
    Console.ReadLine();
}
```

C# 还允许你像这样给多个变量赋值：

`int a, b, c, d = 5;`

你还可以通过这种方式进行多行变量声明：

```csharp
int a, b,
    c,
d = 5;
```

编译器会将上述代码视为一行，直到找到分号。

你可以通过将一个变量赋值另一个变量来很好地声明变量：

```csharp
int r = 56;
int y = r; // 结果 y 的值也将是 56
```

这里有一个你可以复制的程序。将它复制到 `Visual C#` 编辑器中运行：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            string firstname, lastname;

            Console.WriteLine("Enter Your First Name:");
            firstname = Console.ReadLine();

            Console.WriteLine("Enter Your Last Name:");
            lastname = Console.ReadLine();

            Console.WriteLine("Your name is " + firstname + " " + lastname);

            Console.ReadLine();
        }
    }
}
```

记住 `Console.ReadLine()` 用于从用户获取输入。用户输入的任何内容都将成为变量 `firstname` 和 `lastname` 的值。尝试更改代码并观察会发生什么；例如，删除你打印行中 `firstname` 和 `lastname` 之间的引号和一个一个加号。

### 数据类型

本章清楚地说明了在声明变量之前，你必须指定它的数据类型：

`data_type variable_name;`

从上面的示例中，你可能已经了 `string` 和 `int`。但这些并不是唯一的数据类型。

让我们详细查看最常用的类型：

- `string`：用于存储文本。以 `Hello World` 为例。在处理字符串时，务必将它们放在引号中。
- `char`：单个 Unicode 字符。
- `int`：用于存储数字。因此，你可以用它来存储整数。示例有 5、10 和 1003。
- `float`：这代表 32 位单精度浮点类型。其范围是 -3.402823e38 到 3.402823e38。
- `double`：这是 64 位双精度浮点类型。其范围是 -1.797693134862332e-308 到 1.797693134862332e-308。
- `decimal`：这代表 128 位小数值，有效数字为 28 到 29 位。
- `byte`：这表示 8 位无符号整数。其范围是 0 到 255。
- `sbyte`：代表 8 位有符号整数。范围是 -128 到 127。
- `uint`：代表 32 位无符号整数，范围为 0 到 4294967295。
- `short`：意味着 16 位有符号整数。范围是 -32,768 到 32,767。
- `long`：代表 64 位有符号整数。
- `ulong`：表示 64 位无符号整数。
- `bool`：C# 中简单的数据类型。它的范围包含两个值：`True` 和 `False`。你在编写逻辑表达式时会使用它。
- `DateTime`：用于指示日期和时间。

如果变量的值与指定的数据类型不符，编译器将显示错误消息。尝试以下示例：

```csharp
int x = 1;
Console.WriteLine(x);
Console.ReadLine();
```

现在尝试这个错误的示例：

```csharp
int x = "Program";
Console.WriteLine(x);
Console.ReadLine();
```

记住，`int` 只能接受整数；`"Program"` 是一个字符串。

## 第4章：运算符

运算符指示编译器执行特定操作。例如，在表达式 `5 - 3` 中，减号是运算符，而 `5` 和 `3` 是操作数。该表达式告诉编译器从 5 中减去 3。

下面，我们将查看各种运算符。

### 1. 赋值运算符

这是 C# 中可以使用的运算符列表：

| 运算符 | 解释 | 示例 |
| --- | --- | --- |
| `=` | 等于，将值赋予变量。 | `a = b` |
| `+=` | 加法赋值，将右侧加到左侧变量上。 | `a += b` |
| `-=` | 减法赋值，从左侧变量减去右侧值。 | `a -= b` |
| `*=` | 乘法赋值，将左侧变量乘以右侧值。 | `a *= b` |
| `/=` | 除法赋值，将左侧变量除以右侧值。 | `a /= b` |
| `%=` | 取模赋值，对左侧变量对右侧取模。 | `a %= b` |
| `<<=` | 左移。 | `a <<= b` |
| `>>=` | 右移。 | `a >>= b` |

### 2. 算术运算符

这些运算符用于创建数学表达式。以下是 C# 中可以使用的算术运算符：

| 运算符 | 解释 | 示例 |
| --- | --- | --- |
| `+` | 加法，增加操作数。 | `a + b` |
| `-` | 减法，从左侧操作数减去右侧操作数。 | `a - b` |
| `*` | 乘法，乘以操作数。 | `a * b` |
| `/` | 除法，将左侧操作数除以右侧操作数。 | `a / b` |
| `%` | 取模，返回左侧操作数除以右侧操作数的余数。 | `a % b` |

你可以使用以下代码尝试这些运算符：

```csharp
int a = 1;
int b = 2;

Console.WriteLine(b * a);
```

更改 `Console.WriteLine(b * a)` 中的运算符并观察发生什么。

### 3. 逻辑运算符

这些用于检查表达式是否为真或假。以下是逻辑运算符表：

| 运算符 | 解释 | 示例 |
| --- | --- | --- |
| `&&` | 逻辑与，检查两个操作数是否都为真。如果是，则返回真。如果其中一个或两个为假，则返回假。 | `a && b` 为假 |
| `||` | 逻辑或，如果任何一个操作数为真，则返回真。 | `a || b` 为真 |
| `!` | 逻辑非，反转布尔表达式当前的值。 | `!(a && b)` 为真 |

### 4. 关系运算符

这些运算符用于检查表达式中的两个操作数是否为真或假。下表显示了 C# 中可以使用的关系运算符（a = 4, b = 10）：

| 运算符 | 解释 | 示例 |
| --- | --- | --- |
| `==` | 评估运算符两边的操作数是否相等。如果是，则返回真。 | `a == b` 为假 |
| `!=` | 不等于。如果运算符两边的操作数不相等，则返回真。 | `a != b` 为真 |
| `<` | 小于。如果左侧操作数小于右侧操作数，则返回真。 | `a < b` 为真 |
| `>` | 大于。检查左侧操作数是否大于右侧操作数。如果是，则返回真。 | `b > a` 为真 |
| `<=` | 小于等于。检查左侧操作数是否小于或等于右侧操作数。如果是，则返回真。 | `a <= b` 为真 |
| `>=` | 大于等于。如果左侧操作数大于或等于右侧操作数，则返回真。 | `b >= a` 为真 |

## 第 5 章：条件语句

### if 语句

这是编码时最重要的语句之一。它允许你指定在满足特定条件时程序应该采取的操作。

这意味着你需要先指定条件。你的程序将检查该条件是否为真（`true`），之后将执行特定的操作。但如果条件为假（`false`），程序将不会执行 `if` 语句体体。

以下是 `if` 语句的语法：

```csharp
if(boolean expression)
{
    // 如果表达式为真，则执行此代码块
}
```

这里有一个示例可以帮助你理解：



```csharp
static void Main(string[] args)
{
    int a = 5, b = 35;

    if (a >= b)
    {
        Console.WriteLine("a is greater than or equal to b");
        Console.ReadLine();
    }

    if (a <= b)
    {
        Console.WriteLine("a is less than or equal to b");
        Console.ReadLine();
    }

    if (a == b)
    {
        Console.WriteLine("a is equal to b");
        Console.ReadLine();
    }
}
```

在上面的示例中，`a` 等于 5，`b` 等于 35。不用说，`a` 小于 `b`。这意味着第一个 `if` 语句求结果为假。因此，程序将跳过它（不执行其代码块），并移动到下一个 `if` 语句，后者的求结果为真。第二个 `if` 语句的代码块将被执行，显示“a is less than or equal to b”。

C# 给了你使用 `else` 语句的机会，它紧跟在 `if` 语句之后。这告诉程序在 `if` 语句求结果为假（或未执行）时该做什么。这里有一个示例：

```csharp
static void Main(string[] args)
{
    int a = 5, b = 35;

    if (a == b)
    {
        Console.WriteLine("a is equal to b");
        Console.ReadLine();
    }

    else
    {
        Console.WriteLine("a and b are not equal");
        Console.ReadLine();
    }
}
```

由于 `a` 和 `b` 不相等，`if` 语句将不会执行。程序将转向 `else` 语句并执行它。这里是另一个示例：

```csharp
static void Main(string[] args)
{
    int number;

    Console.WriteLine("Input a number that is between 50 and 70");
    number = int.Parse(Console.ReadLine());

    if (number > 70)
    {
        Console.WriteLine("Oops! The number can only be between 50 and 70.");
    }
    else if (number < 50)
    {
        Console.WriteLine("Oops! That's less than 50.");
    }
    else
    {
        Console.WriteLine("You got it. Yeah!!!");
    }

    Console.ReadLine();
}
```

# switch 语句

如果你有多个条件需要检查，你可以自由使用多个 `if` 语句。然而，这会让你的代码难以阅读。而且这运行运行程序的效率较低。最好的办法是使用 `switch` 语句，它类似于拥有多个 `if` 语句。通过这种方式，你创建一个 `switch` 语句并与多个 `cases` 配对。这里有一个示例：

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Choose a color: blue, green, red, or orange.");
    string color = Console.ReadLine();
    switch (color.ToLower())
    {
        case "blue":
        case "green":
        case "red":
            Console.WriteLine("We have this in stock.");
            break;
        case "orange":
            Console.WriteLine("We don't have this color in stock.");
            break;
    }
    Console.ReadLine();
}
```

上述程序的解释：在创建 `switch` 语句时，将标识符（在此例中是变量 `color`）放在关键字 `switch` 之前。`color` 可以取任何值。在上面的示例中，它只能取用户输入的 `switch` 情况。

在 `switch` 语句中，`ToLower()` 告诉我们的编译器将用户输入的内容转换为小写。记住，对于 C# 来说，`blue` 和 `Blue` 是不一样的。`break` 是一个关键字，用于停止执行特定代码块的执行。`switch` 语句允许你添加默认操作。这意味着如果用户输入不符合任何 `case` 的内容，程序将执行默认操作。这里是该功能的示例：

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Choose a color: blue, green, red, or orange.");
    string color = Console.ReadLine();
    switch (color.ToLower())
    {
        case "blue":
        case "green":
        case "red":
            Console.WriteLine("We have this in stock.");
            break;
        case "orange":
            Console.WriteLine("We don't have this color in stock.");
            break;
        default:
            Console.WriteLine("Re-run the program and type the correct color.");
            break;
    }
    Console.ReadLine();
}
```

# 第 6 章：循环

你可能想要重复执行代码的某部分。然而，你必须根据需要的次数重写该代码，这是低效的。你可以通过循环轻松地解决这个问题。让我们讨论一下你可以使用的不同类型的循环。

## 最简单的循环

这是所有循环中最简单的。只要你指定的条件保持为真，它就会执行你的代码。这意味着如果条件求结果为真，`while` 语句的代码块将被执行。程序将重新检查条件，如果它仍然为真，它将继续执行代码中的下一行。一直持续到条件求结果为假。这里有一个示例：

```csharp
static void Main(string[] args)
{
    int x = 0;

    while (x < 5)
    {
        Console.WriteLine("The value of x is {0}", x);
        x++;
    }

    Console.ReadLine();
}
```

输出：

Value of x is 0

Value of x is 1

Value of x is 2

Value of x is 3

Value of x is 4

在上面的示例中，`while` 语句被设计为检查 `x` 的值。如果 `x` 小于 5，它的值将打印在屏幕上。`x++` 告诉我们的程序在任何时刻查看 `x` 的值并加 1。你也可以写为 `x = x + 1`。在第一次运行 `while` 语句时，`x` 等于 0。因为小于 5，0 被打印在屏幕上。程序随后返回 `while` 语句并等同于 `x`。这次，`x` 是 1。所以它被打印在屏幕上。这种情况一直持续到 `x` 变成 5，使得 `while` 语句求结果为假。因此，`while` 语句的代码块不执行，程序移动到下一行（`Console.ReadLine()`）。你可能注意到在在屏幕上打印 `x` 值的语句内部有 `{0}`。零是一个占位符。它代表变量 `x`，该变量位于该语句末尾的位置。

## Do...While 循环

这与 `while` 循环相同。唯一的区别是在 `Do...While` 循环中，代码块首先执行，稍后检查条件。因此你的代码至少会被执行一次。这里有一个示例：

```csharp
static void Main(string[] args)
{
    int x = 0;

    do
    {
        Console.WriteLine("The value of x is {0}", x);
        x++;
    } while (x < 6);
    Console.ReadLine();
}
```

尝试将 `x` 的值改为 7 并观察发生了什么。

## For 循环

这是你可以使用的常用的循环之一。它按指定的次数重复你的代码。以下是它的语法：

```csharp
for (初始化值; 状态条件; 递增/递减)
{
    语句(s);
}
```

这里有一个你可以尝试的示例：

```csharp
static void Main(string[] args)
{
    for (int x = 0; x < 5; x++)
    {
        Console.WriteLine("Value of x: {0}", x);
    }
    Console.ReadLine();
}
```

输出：

Value of x is 0

Value of x is 1

Value of x is 2

Value of x is 3

Value of x is 4

在 `for` 语句中，我们有 `x` 的值为 0。`x < 5` 是一个布尔条件，求结果为真或假。`x++` 给当前的 `x` 值加 1。

## Foreach

它的工作方式与 `for` 循环相同。`foreach` 最适合用于循环数组中的项。`foreach` 比 `for` 循环更容易阅读且不易出错。这里有一个示例：

```csharp
static void Main(string[] args)
{
    string[] boyNames = new string[] {
        "John",
        "Emmanuel",
        "Fred",
        "Tom",
        "Mike"
    };

    foreach (string Name in boyNames)
    {
        Console.WriteLine("Boy Name: {0}", Name);
    }
    Console.ReadLine();
}
```

# 第 7 章：理解方法

我们在书前面的部分简要介绍了方法。在本章中，我们将深入探讨这个主题，因为它非常重要。

到目前为止，我们创建的程序代码都写在 `Main()` 方法中。这没有问题，因为大多数程序只执行单一任务。但随着你代码的增长，你会发现有必要添加其他方法。相似的功能将被在一起，使得你的代码更易读且更具重用性。你还将有机会隐藏某些信息并避免重复。

在创建方法时，请确保将其包含在类中。不要试图在一个方法中包含过多的函数——一个就足够了。

## 如何定义方法

在指定方法时，可以使用以下语法：

```
AccessLevel ReturnValueType MethodName(ParamList)
{
    Statements
}
```

**Access Level（访问级别）**：这使用访问修饰符来指定方法的可见性。`private`（私有）意味着该方法只能对类中的其他元素可见。`public`（公共）指的是对所有人一切都可见的方法。`protected`（保护）用于访问权限限制在类及其派生类的方法。

**Return Value Type（返回值类型）**：方法可以返回一个值。你使用数据类型来指示方法应该返回的值。例如，`int` 表示方法将返回一个整数，而 `void` 意味着它不返回任何内容。

**Method Name（方法名）**：这就是一个标识符。你必须遵循创建标识符时的规则。

**Parameter List（参数列表）**：它位于一对括号中。如果你有多个参数，用逗号分隔它们。参数向方法传递和接收数据。如果你有空括号，意味着没有参数。

**Statements（语句）**：这是要执行的代码，包含在大括号内。

这是一个关于此的示例：

```
public void sampleMethod()
{
    Console.WriteLine("My sample method has been called.");
}
```

## 调用方法

上面的方法（`sampleMethod()`）可以从另一个方法调用。这是一个示例：

```csharp
using System;

class Program {
    static void Main() {
        Console.WriteLine("This is the main method.");
        sampleMethod();
        Console.ReadLine();
    }

    public static void sampleMethod() {
        Console.WriteLine("My sample method has been called.");
    }
}
```

当程序执行 `Main` 方法时，它会先显示“This is the main method.”。然而，一行告诉它执行 `sampleMethod()`。因此，程序将离开 `Main()` 并进入 `sampleMethod()`。在完成后，它将返回 `Main` 执行 `Console.ReadLine()`。

你可能注意到我在 `sampleMethod` 中添加了 `static`。这是因为我不能在静态方法中调用非静态方法。

## 常用语句

### Return 语句

方法可以编写为将值返回到其他方法。考虑下面的示例：

```csharp
namespace ConsoleApplication {
class Addition {
    static void Main() {
        addInt(10, 30);
    }

    static void addInt(int a, int b) {
        int c = a + b;
        Console.WriteLine("Adding {0} and {1} brings {2} as the answer.", a, b, c);
    }
}
```

在上面的示例中，`addInt` 在 `Main` 中被调用。我们可以重写这段代码，仅在调用 `addInt` 时返回结果。我们的代码看起来像这样：

```csharp
namespace ConsoleApplication1
{
    class Addition
    {
        static void Main()
        {
            int result = addInt(10, 30);
            Console.WriteLine("The answer is {0}", result);
            Console.ReadLine();
        }

        static int addInt(int a, int b)
        {
            int c = a + b;
            return c;
        }
    }
}
```

`addInt` 方法必须将其值从 `void` 更改为 `int`，这阻止了它返回空。语句中还必须添加 `return c`，替换了原来在屏幕上打印答案的代码。现在我们让 `addInt` 向调用它的方法返回值，我们需要在 `Main` 方法中捕获该返回值，那里是 `addInt` 被调的地方。`int result = addInt(10, 30)` 这一行就完成了此操作。

### break 语句

这是 C# 中的另一个重要语句。当特定代码块中使用 `break` 时，程序将终止该代码并移动到下一个代码块。这是一个示例：

```csharp
namespace breakExample
{
    class Program
    {
        static void Main(string[] args)
        {
            int a = 5;
            while (a < 15)
            {
              Console.WriteLine(a);
              if (a == 9)
              {
                Console.WriteLine("Break statement encountered.");
                break;
              }
              a++;
            }
            Console.ReadLine();
        }
    }
}
```

在上面的示例中，程序无法显示任何大于 9 的数字，因为它被指令在 `a` 变为 9 时 `break`。

# 第 8 章：使用数组



# 数组

数组是相同类型数据的集合。在本章中，我们将学习如何使用数组来存储和处理数据。当你有多个相同类型的值时（例如整数列表或字符串集合），数组非常有用。我们将探索如何声明、初始化和访问数组，以及如何使用循环遍历它们。

## 数组的声明和初始化

声明数组时，你指定它包含的元素类型和数组名称，后跟方括号。

```csharp
int[] numbers = new int[5];
```

你也可以在声明时初始化数组：

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
```

### 访问和修改数组

要访问数组中的元素，使用它的索引，索引从 0 开始。

```csharp
Console.WriteLine(numbers[0]); // 输出 1
numbers[0] = 10; // 修改第一个元素
```

### 遍历数组

遍历数组的常用方法是使用 `for` 循环或 `foreach` 循环。

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}

foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

# 第 9 章：异常处理

异常是发生在运行时的错误。这里有一个常见的例子：假设你创建了一个程序，它在对用户输入的两个数字进行除法后返回结果。现在想象一种情况，用户在另一个数字输入了 0。这将导致错误导致程序崩溃。异常处理的作用就是防止这种情况的发生。如果你使用了它，程序将显示有关错误的消息并继续运行。

要使用异常处理，你需要三个重要的代码块：`try`、`catch` 和 `finally`。但你也可以添加第四个名为 `throw` 的块：

- `try`：这是一个关键字。它用于标识一个可能引发异常的代码块。
- `catch`：这是另一个关键字。它在 `try` 抛出异常后处理该异常。
- `finally`：无论是否发生异常，此代码块都会执行。
- `throw`：另一个关键字，用于添加用户定义的异常消息。

让我们来看一个例子：

```csharp
static void Main(string[] args)
{
    int num1, num2;
    decimal result;

    Console.WriteLine("This program divides two numbers");
    Console.WriteLine("Enter the first Number: ");
    num1 = Convert.ToInt32(Console.ReadLine());
    Console.WriteLine("Enter the second Number: ");
    num2 = Convert.ToInt32(Console.ReadLine());
}
```

```csharp
result = (decimal)num1 / (decimal)num2;
Console.WriteLine("The answer is " + result.ToString());
Console.ReadLine();
```

将这段代码复制到编辑器中运行程序。第一次运行时，输入 4 作为第一个数字，输入 2 作为第二个数字。正如你所看到的，你应该没有遇到问题。关闭控制台再次运行程序。这次，输入任意数字和 0。

程序将会崩溃，在用户眼中损害了我们的编码能力。坦率地说，我们有异常处理。这里有一段可以让我们免于尴尬的代码：

```csharp
static void Main(string[] args)
{
MainBlock:
//This is the try block
try
{
    int num1, num2;
    decimal result;

    Console.WriteLine("This program divides two numbers");
    Console.WriteLine("Enter the first Number: ");
    num1 = Convert.ToInt32(Console.ReadLine());
    Console.WriteLine("Enter the second Number: ");
    num2 = Convert.ToInt32(Console.ReadLine());

    result = (decimal)num1 / (decimal)num2;
    Console.WriteLine("The answer is " + result.ToString());
}
```

```csharp
//This is the catch block to handle exception
catch (DivideByZeroException dex)
{
    Console.WriteLine("Entering 0 raises an exception!");
    Console.WriteLine("Details about Error: " + dex.ToString());
    goto MainBlock;
}
```

```csharp
//This is the finally block
finally
{
    Console.ReadLine();
    Console.WriteLine("Press Enter to close or reload the program");
    Console.ReadLine();
}
```

运行程序后，输入任意数字和 0。这个程序不会崩溃。相反，它会显示一个错误并允许你通过按回车重新运行它。

要知道 `goto` 是一个关键字，它指示程序跳转到代码中的某个标签。在上面的示例中，标签是 `MainBlock`。

## 用户定义异常

在 C# 中，你可以创建自己的异常。这些被称为用户生成的异常或自定义异常。它们使用了我们已经讨论过的 `throw` 关键字。学习这个例子：

```csharp
namespace userDefinedException
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

```csharp
int maxR;
Console.WriteLine("Please rate the last movie you just watched. The rating goes from 1 (very bad) to 5 (very exciting).\n");
maxR = Convert.ToInt32(Console.ReadLine());
try
{
    if (maxR <= 5)
    {
        Console.WriteLine("You have given a rating of {0}. Thank you for your input!", maxR);
        Console.ReadLine();
    }
    else
    {
        throw (new wrongR("Wrong Rating Exception: This rating is not valid."));
    }
}
catch (wrongR oex)
{
    Console.WriteLine(oex.Message.ToString());
    Console.ReadLine();
}

//This code creates a custom exception called wrongR
public class wrongR : Exception
{
    public wrongR(string message)
        : base(message)
    {
    }
}
```

如果你按照建议运行程序后输入 1 到 5，自定义异常将不会执行。然而，如果你输入的评分高于 5，程序将带入一个错误。

# 第 10 章：继承

这是 C# 中最重要的概念之一。你可以打赌你将经常使用它。通过它，你可以让一个类继承另一个类的属性。这将节省你编写已有的函数所需花费的时间。你的代码将是可重用的，程序运行将更加简单且高效。

基类（你可以将其视为父类）定义属性。派生类（也称为子类）借用这些属性。

以下是语法：

```csharp
accessSpecifier class baseClass
{
    Statements
}
```

```csharp
class derivedClass : baseClass
{
    Statements
}
```

在派生类中，以关键字 `class` 开始。然后写类名，后面跟着冒号，然后是基类的名称。冒号告诉程序从基类继承属性。让我们来看一个例子：

```csharp
namespace Inheritance_Example
{
    class Program
    {
        static void Main(string[] args)
        {
            Eagle b1 = new Eagle();
            b1.EagleInfo();

            Owl b2 = new Owl();
            b2.OwlInfo();

            Chicken b3 = new Chicken();
            b3.ChickenInfo();

            Console.ReadKey();
        }
    }
}
//This is the base class

class Bird
{
    protected void BirdInfo()
    {
        Console.WriteLine("It has a pair of wings and a pair of feet.");
        Console.ReadLine();
    }
}
```

```csharp
//This is the first derived class
class Eagle : Bird
{
    public void EagleInfo()
    {
        Console.WriteLine("This is an Eagle, a bird.");
        BirdInfo();
    }
}
```

```csharp
//This is the second derived class
class Owl : Bird
{
    public void OwlInfo()
    {
        Console.WriteLine("This is an Owl, a bird.");
        BirdInfo();
    }
}
```

```csharp
//This is the third derived class
class Chicken : Bird
{
    public void ChickenInfo()
    {
        Console.WriteLine("This is a chicken, a bird.");
        BirdInfo();
    }
}
```

鸡、猫头鹰和鹰都是鸟。我们知道它们都有翅膀和脚。因此，与其在每个派生类中都写这些鸟都有翅膀和脚，我们可以创建一个包含这些共同特征的基类。每个派生类将继承这些共同特征，并添加自己的特征，在这种情况下是告诉我们正在看的是哪种鸟。

要知道任何类都可以成为基类：例如我想让鸡成为基类，猫头鹰成为派生类，我可以这样写代码：

```csharp
class Owl : Chicken
```

感谢阅读本书，希望它帮助你学会了如何开始 C# 编程。现在，我相信你已经可以创建简单的控制台程序了。

然而，这还没有结束：你应该继续练习。构思你可以编写的程序。此外，花时间研究其他人编写的代码。思考你已经熟悉的复杂程序并尝试构建它们也有帮助。实验是提高编程能力的方法之一。

如果你遇到困难（这在你刚开始时会经常发生），请让互联网成为你最好的朋友。有很多论坛可以提供编程建议。

精通编程需要时间和努力。祝你在通往程序员的道路上一切顺利。
