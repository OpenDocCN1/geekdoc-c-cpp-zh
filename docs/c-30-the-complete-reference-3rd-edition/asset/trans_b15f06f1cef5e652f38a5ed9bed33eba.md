

```csharp
// A C# program begins with a call to Main().
static void Main() {

    // Here, Console.WriteLine is fully qualified.
    System.Console.WriteLine("A simple C# program.");
}
```

由于在使用该命名空间的成员时总是需要指定 System 命名空间相当繁琐，大多数 C# 程序员会在程序顶部包含 `using System`，本书中的所有程序也都将如此。然而，重要的是要理解，如果需要，你可以显式地用命名空间来限定名称。

## 第二个简单程序

也许没有哪种结构对编程语言来说比 *变量* 更重要。*变量* 是一个命名的内存位置，可以为其赋值。它之所以被称为变量，是因为它的值在程序执行过程中可以被改变。换句话说，变量的内容是可变的，而非固定的。

```csharp
// This program demonstrates variables.

using System;

class Example2 {
    static void Main() {
        int x; // this declares a variable
        int y; // this declares another variable

        x = 100; // this assigns 100 to x

        Console.WriteLine("x contains " + x);

        y = x / 2;

        Console.Write("y contains x / 2: ");
        Console.WriteLine(y);
    }
}
```

运行该程序时，你将看到以下输出：

```text
x contains 100
y contains x / 2: 50
```

该程序引入了几个新概念。首先，语句

```csharp
int x; // this declares a variable
```

声明了一个名为 x、类型为整数的变量。在 C# 中，所有变量在使用前都必须声明。此外，还必须指定变量能够保存的值的种类。这称为变量的类型。在本例中，x 可以保存整数值，即整数。在 C# 中，要声明一个整数类型的变量，需要在其名称前加上关键字 `int`。因此，前面的语句声明了一个名为 x、类型为 `int` 的变量。

下一行声明了第二个变量 y。

```csharp
int y; // this declares another variable
```

请注意，它使用的格式与第一个相同，只是变量名不同。

一般来说，要声明一个变量，你会使用这样的语句：

```csharp
type var-name;
```

在这里，`type` 指定了所声明变量的类型，`var-name` 是变量的名称。除了 `int` 之外，C# 还支持其他几种数据类型。

下一行代码将 x 的值赋为 100：

```csharp
x = 100; // this assigns 100 to x
```

在 C# 中，赋值运算符是单个等号。它将右侧的值复制到左侧的变量中。

下一行代码输出 x 的值，并在前面加上字符串“x contains ”。

```csharp
Console.WriteLine("x contains " + x);
```

在此语句中，加号使得 x 的值显示在前面的字符串之后。这种方法可以推广。使用 `+` 运算符，可以在单个 `WriteLine()` 语句中连接任意多个项。

下一行代码将 y 的值赋为 x 除以 2 的结果：

```csharp
y = x / 2;
```

这行将 x 中的值除以 2，然后将结果存储在 y 中。因此，该行执行后，y 将包含值 50，而 x 的值不变。与大多数其他计算机语言一样，C# 支持全套算术运算符，如下所示：

|  |  |
| + | 加法 |
| - | 减法 |
| * | 乘法 |
| / | 除法 |

以下是程序中的接下来两行：

```csharp
Console.Write("y contains x / 2: ");
Console.WriteLine(y);
```

这里出现了两个新事物。首先，内置方法 `Write()` 用于显示字符串“y contains x / 2: ”。该字符串后面没有换行。这意味着当下一个输出生成时，它将在同一行开始。`Write()` 方法与 `WriteLine()` 非常相似，只是它不会在每次调用后输出换行。其次，在调用

```csharp
Console.WriteLine("ivar after division: " + ivar);
Console.WriteLine("dvar after division: " + dvar);
}
```

该程序的输出如下所示：

```
Original value of ivar: 100
Original value of dvar: 100

ivar after division: 33
dvar after division: 33.3333333333333
```

正如你所看到的，当 `ivar`（一个 `int` 变量）除以 3 时，执行的是整数除法，结果是 33——小数部分丢失了。然而，当 `dvar`（一个 `double` 变量）除以 3 时，小数部分被保留了下来。

正如程序所示，当你想在程序中指定一个浮点值时，必须包含小数点。如果不这样，它将被解释为整数。例如，在 C# 中，值 100 是整数，而值 100.0 是浮点值。

程序中还有另一个值得注意的新内容。要打印空行，只需调用不带任何参数的 `WriteLine()`。

浮点数据类型通常用于处理现实世界中常常需要小数部分的量。例如，下面的程序计算圆的面积，它使用 3.1416 作为 π 的值。

```
// Compute the area of a circle.
```

```csharp
using System;

class Circle {
    static void Main() {
        double radius;
        double area;

        radius = 10.0;
        area = radius * radius * 3.1416;

        Console.WriteLine("Area is " + area);
    }
}
```

该程序的输出如下所示：

```
Area is 314.16
```

显然，如果没有浮点数据，就无法令人满意地完成圆面积的计算。

## 两个控制语句

在方法内部，执行从上到下按语句顺序进行。通过使用 C# 支持的各种程序控制语句，可以改变这种流程。虽然我们稍后会仔细研究控制语句，但这里先简要介绍两种，因为我们将用它们来编写示例程序。

### if 语句

你可以通过使用 C# 的条件语句 `if` 来选择性地执行程序的一部分。`if` 语句在 C# 中的工作方式与其他语言中的 IF 语句非常相似。例如，它在语法上与 C、C++ 和 Java 中的 `if` 语句完全相同。其最简单的形式如下所示：

```csharp
if(condition) statement;
```

这里，`condition` 是一个布尔（即 true 或 false）表达式。如果 `condition` 为 true，则执行该语句。如果 `condition` 为 false，则跳过该语句。下面是一个示例：

```csharp
if(10 < 11) Console.WriteLine("10 is less than 11");
```

在本例中，由于 10 小于 11，条件表达式为 true，因此 `WriteLine()` 将执行。然而，请考虑下面这种情况：

```csharp
if(10 < 9) Console.WriteLine("this won't be displayed");
```

在本例中，10 不小于 9。因此，对 `WriteLine()` 的调用不会发生。

C# 定义了一整套可用于条件表达式的关系运算符。如下所示：

| 运算符 | 含义 |
| < | 小于 |
| <= | 小于或等于 |
| > | 大于 |
| >= | 大于或等于 |
| == | 等于 |
| != | 不等于 |

下面是一个演示 `if` 语句的程序：

```csharp
// Demonstrate the if.
using System;
class IfDemo {
    static void Main() {
        int a, b, c;
        a = 2;
        b = 3;
        if(a < b) Console.WriteLine("a is less than b");
        // This won't display anything.
        if(a == b) Console.WriteLine("you won't see this");
        Console.WriteLine();
    }
}
```

```csharp
c = a - b; // c contains -1
Console.WriteLine("c contains -1");
if(c >= 0) Console.WriteLine("c is non-negative");
if(c < 0) Console.WriteLine("c is negative");

Console.WriteLine();

c = b - a; // c now contains 1
Console.WriteLine("c contains 1");
if(c >= 0) Console.WriteLine("c is non-negative");
if(c < 0) Console.WriteLine("c is negative");
}
```

该程序生成的输出如下所示：

```
a is less than b

c contains -1
c is negative

c contains 1
c is non-negative
```

请注意该程序中的另一件事。这一行

```
int a, b, c;
```

使用逗号分隔的列表声明了三个变量 a、b 和 c。如前所述，当你需要两个或更多相同类型的变量时，可以在一条语句中声明，只需用逗号分隔变量名即可。

### for 循环

你可以通过创建循环来重复执行一段代码。C# 提供了多种强大的循环结构。我们这里要看的是 `for` 循环。与 `if` 语句一样，C# 的 `for` 循环与 C、C++ 和 Java 中的 `for` 循环类似。`for` 循环最简单的形式如下所示：

```csharp
for(initialization; condition; iteration) statement;
```

在最常见的形式中，循环的初始化部分将循环控制变量设置为初始值。`condition` 是一个测试循环控制变量的布尔表达式。如果测试结果为 true，`for` 循环将继续迭代；如果为 false，循环终止。迭代表达式决定了每次循环迭代时循环控制变量的改变方式。下面是一个演示 `for` 循环的简短程序：

```
// Demonstrate the for loop.

using System;

class ForDemo {
    static void Main() {
        int count;
```

