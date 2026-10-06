
# 第 11 章 异常处理

在 C# 中，所有异常都是 `Exception` 类或其某个派生类的实例。异常条件会生成一个封装错误信息的对象。与 C# 编程语言中的所有其他类一样，`Exception` 类是 `Object` 类的后代。`Exception` 类本身还有几个派生类，其中许多具有不寻常的名字，例如 `SerializationException`、`ParserException`、`SoapException`、`IOException`（用于输入输出错误）、`InvalidPrinterException`（用户请求无效打印机时）以及 `PathLongException`（当文件路径字符超过系统允许范围时使用）。C# 有超过 100 多个 `Exception` 子类；表 11-1 仅列出部分内容，让你了解可能看到的各种情况。

## 理解异常

| 类 | 描述 |
| --- | --- |
| `System.ArgumentException` | 当提供给方法的某个参数无效时抛出 |
| `System.ArithmeticException` | 当算术、强制转换或转换操作出现错误时抛出 |
| `System.ArrayTypeMismatchException` | 当尝试在数组中存储错误类型的元素时抛出 |
| `System.Data.OperationAbortedException` | 当正在进行的操作被用户中止时抛出 |
| `System.Drawing.InvalidPrinterException` | 当尝试访问无效的打印机设置时抛出 |
| `System.FormatException` | 当参数格式不符合调用方法的参数规范时抛出 |
| `System.IndexOutOfRangeException` | 当尝试访问数组边界之外的索引时抛出；此类无法继承 |
| `System.InvalidCastException` | 当发生无效的强制转换或显式转换时抛出 |
| `System.InvalidOperationException` | 当针对对象的当前状态调用方法时抛出 |
| `System.IO.InvalidDataException` | 当数据流格式无效时抛出 |
| `System.IO.IOException` | 当发生 I/O 错误时抛出 |
| `System.MemberAccessException` | 当尝试访问类成员失败时抛出 |
| `System.NotImplementedException` | 当请求的方法或操作未实现时抛出 |
| `System.NullReferenceException` | 当尝试对空对象解除引用时抛出 |
| `System.OperationCanceledException` | 在线程取消其正在执行的操作时在线程中抛出 |
| `System.OutOfMemoryException` | 当没有足够的内存继续执行程序时抛出 |
| `System.RankException` | 当向方法传递维度数量错误的数组时抛出 |
| `System.StackOverflowException` | 当执行栈因为包含过多的嵌套方法调用而溢出时抛出；此类无法继承 |

**表 11-1** 选定的 C# 异常子类

表 11-1 使用了“抛出”（thrown）一词，将在本章后面解释。

你将使用的大多数异常派生自三个类：

* 派自 `SystemException` 的内置通用语言运行时（CLR）异常类
* 你派自 `ApplicationException` 的自定义应用程序异常类
* `Exception` 类，它是 `SystemException` 和 `ApplicationException` 的父类

微软以前建议你应该从 `ApplicationException` 类创建你自己的自定义异常。他们现在修改了观点，并建议你在实践中使用 `Exception` 类作为基类，因为他们没有发现之前的方法具有显著价值。如需更新信息，请访问 <http://msdn.microsoft.com>。

## 故意生成 SystemException

你可以通过强制程序包含错误来故意生成 `SystemException`。作为一个例子，在每种编程语言中，整数除以零都是非法的，因为这在数学上是未定义的。考虑图 11-1 中简单的 `MilesPerGallon` 程序，它提示用户输入两个值并将第一个除以第二个。如果用户输入非零整数，程序运行正常没有意外。然而，如果用户在提示输入加仑时输入 0，就会发生除以 0 操作，并产生错误。图 11-2 显示了程序的两次执行。

在 C# 中将浮点数除以 0 时，不会发生异常。相反，C# 会为结果分配特殊值 `Infinity`。因为浮点和双精度浮点数是不精确的，将它们除以 0 在数学上趋于无限。

### MilesPerGallon 程序示例

```csharp
using System;
using static System.Console;

class MilesPerGallon
{
    static void Main()
    {
        int milesDriven;
        int gallonsOfGas;
        int mpg;
        Write("Enter miles driven ");
        milesDriven = Convert.ToInt32(ReadLine());
        Write("Enter gallons of gas purchased ");
        gallonsOfGas = Convert.ToInt32(ReadLine());
        mpg = milesDriven / gallonsOfGas;
        WriteLine("You {0} miles per gallon", mpg);
    }
}
```

图 11-1 MilesPerGallon 程序

![](img/b0a31988f44670d0728c4f372d8dab77_518_0.png)

图 11-2 MilesPerGallon 程序的两次执行

当用户在 `MilesPerGallon` 程序中加仑输入 0 时，对话框报告应用程序停止并需要关闭。此错误是为了演示而故意设计的；用户可以通过点击对话框右下角的“关闭”按钮忽略此消息。

在图 11-2 `MilesPerGallon` 程序的第一次执行中，用户输入了两个有效的整数，计算成功。然而，在第二次执行中，用户在加仑处输入 0，错误消息显示创建了一个未处理的 `System.DivideByZeroException` 异常。消息提供了进一步信息（“尝试除以 0。”），并显示了发生异常的方法——在 `MilesPerGallon.Main()` 中。

`DivideByZeroException` 是 C# 自动生成的。它是 `DivideByZeroException` 类的一个实例，该类有四个祖先。它是 `ArithmeticException` 类的子类，而该类继承自 `SystemException` 类。`SystemException` 类派生自 `Exception` 类，而 `Exception` 类又是 `Object` 类的子类。

仅仅发生了异常并创建了 `Exception` 对象，并不意味着你必须处理它。在 `MilesPerGallon` 类中，你只需让出错的程序终止即可；这就是为什么图 11-2 中的错误信息显示异常是“未处理的（Unhandled）”。然而，程序的终止是突然且不留情的。当程序两个数字相除或执行某些尝试性任务（如玩游戏）时，如果程序突然结束，用户可能会感到恼火。对于交通管制或在手术期间监测患者的生命体征来说，突然结束可能是灾难性的。通过异常处理，程序可以在处理问题后继续运行。这在任务关键型应用中尤为重要。“任务关键型”（mission critical）是指对组织至关重要的任何过程。面向对象的错误处理技术比简单的关闭提供了更优雅的解决方案。

能够适当处理异常的程序被认为比那些不能处理的程序更具容错性和健壮性。容错型应用的设计使其在系统某些部分失效时能够继续运行（可能处于较低的水平）。健壮性代表了系统对压力的抵抗程度以及保持正确功能的能力。

观看视频 System Exceptions（系统异常）。

### 两个真理和一个谎言

1. 异常是执行程序中发生的任何错误状况或意外行为。
2. 在 C# 中，所有异常都是 `Exception` 类或其任一派生类的成员。
3. 在 C# 中，当异常发生并创建了 `Exception` 对象时，你必须使用一套特定的异常处理技术来管理问题。

> 虚假的陈述是 #3。你并不一定因为发生了异常并创建了 `Exception` 对象就必须处理它。

## 由来操作

### 故意引发异常

在许多情况下，C# 会自动生成 `SystemException`。在接下来的步骤中，你将通过执行一个提供多个异常机会的程序来故意生成 `SystemException`。

1. 创建一个名为 `ExceptionsOnPurpose` 的新项目，并输入以下程序，该程序允许你生成几种不同的异常。

```csharp
using System;
using static System.Console;

class ExceptionsOnPurpose
{
    static void Main()
    {
        int answer;
        int result = 0;
        Write("Enter an integer >> ");
        answer = Convert.ToInt32(ReadLine());
        result = answer / zero;
        WriteLine("The answer is " + answer);
    }
}
```

2. 你不能除以未定义的常量 0（通过将除法语句改为 `result = answer / 0`），也不能将变量 `zero` 改为命名常量（通过在 `int zero` 声明开头插入 `const`）。如果你进行了其中任何一处，程序将无法编译，因为编译器可以确定会发生除零错误。然而，使用变量 `zero` 而不是未命名或命名的常量，编译器“信任”在除法发生之前会为该变量提供一个合法的值（尽管在这种情况下，这种信任是不必要的）。保存程序并编译。

3. 使用不同的输入值多次执行程序，并观察结果。每次执行会出现两个窗口。Windows 正在收集更多关于问题的特定信息。该窗口很快会被图 11-3 所示的窗口取代，该窗口重复显示 `ExceptionsOnPurpose.exe` 已停止工作。你永远不会编写一个故意除零的程序；你在这里这样做是为了演示 C# 生成异常的能力。如果你正在运行专业应用程序，你可能会收到解决方案。由于你是故意创建此异常的，只需点击“关闭程序”按钮即可。

![](img/b0a31988f44670d0728c4f372d8dab77_521_0.png)

**图 11-3** 由未处理异常生成的错误报告窗口

图 11-4 显示了程序的三次执行，期间用户输入了以下内容：

* `abc`——这产生了一个 `System.FormatException`，当程序尝试将输入值转换为整数时发生该错误，因为不允许字母。
* `12.5`——这同样产生了一个 `System.FormatException`，因为不允许小数点。
* `0`——这产生了一个 `System.DivideByZeroException`：尝试除以 0。

## 比较传统与面向对象的错误处理

另一种使用异常处理代替决策来控制错误的方法是：当程序的主逻辑被一系列可能检测错误的 `if` 语句和决策中断时，程序可能会变得更加复杂且难以理解。面向对象的错误处理方法将程序的主任务与处理稀有错误的代码分离。

C# 的创建者将“不频繁”定义为发生概率小于 30% 的事件。

程序员使用“晴天场景”（sunny day catch）一词来描述一切顺利且没有发生错误的场景。

## 理解面向对象的异常处理方法

面向对象的异常处理涉及三个术语：`try`、`throw` 和 `catch`。

* 你“尝试”（`try`）执行一个可能无法正确完成的过程。
* 检测到错误状况的方法“抛出”（`throw`）异常。
* 处理错误的代码块“捕获”（`catch`）异常。

当你编写一段可能出现问题的代码块时，可以将代码放在 `try` 块中，`try` 块由以下元素组成：

* 关键字 `try`
* 一对包含可能引发异常的语句的大括号

你必须在 `try` 块之后紧跟着编写至少一个 `catch` 块或 `finally` 块。（你将在本章的晚些时候学习 `finally` 块）。每个 `catch` 块可以“捕获”一种类型的异常——即一个 `Exception` 对象或其任一子类对象的对象。程序员有时将 `catch` 块称为 `catch` 子句（catch clause）。

### catch 块的组成

* 包含异常（`Exception`）类型以及可选的、该异常类型实例名称的括号
* 一对大括号包含处理错误状况的语句

你可以通过省略括号和异常类型来创建一个 `catch` 块。如果你这样做，那么当抛出任何类型的异常时，该 `catch` 块都将执行。换句话说，`catch` 和 `catch(Exception)` 都是启动 `catch` 块以捕获异常的正确方法，当你不需要命名异常对象（因为你不关心显示它的详细信息）。

图 11-5 显示了 `try...catch` 组合的通用格式。`catch` 块中的占位符 `XException` 代表异常类或其任何特定的子类。占位符 `XException` 是 `ExceptionInstance` 对象的数据类型。`catch` 块看起来非常像一个命名为 `catch()` 的方法，它接收一个作为 `XException` 实例的参数。然而，它并不是一个方法；你不能直接调用它。方法可以接受多个参数，但 `catch` 块只能捕获一个，而且与方法不同，`catch` 块没有返回值。

正如 `XException` 所示，异常类通常使用 `Exception` 作为名称的后半部分，例如 `SystemException` 和 `ApplicationException`。编译器并不要求这种命名规范，但这种规范使得异常的后代更容易识别。

```cpp
try {
  // 任意数量的语句；
  // 某些语句可能会抛出异常
} catch(XException anExceptionInstance) {
  // 对其进行处理
}
// 无论是否有异常都会执行这里的语句
```

**图 11-5** `try...catch` 组合的通用形式

你可以在 `try` 块中放置任意数量的语句，包括那些已知永远不会抛出异常的语句。然而，如果你放置在 `try` 块中的任何语句确实抛出了异常，那么捕获该异常的 `catch` 块中的语句将执行。如果 `try` 块内没有发生异常，则 `catch` 块不会执行。无论何种情况，`catch` 块之后的语句都会正常执行。

例如，图 11-6 包含一个程序，其中提示、接受和使用 `gallonsOfGas` 的语句被封装在一个 `try` 块中。（按照惯例，这三个变量声明是在 `try` 块之前完成的。在这种情况下，`mpg` 必须在 `try` 块之外声明以便在程序的最终输出语句中识别。）图 11-7 显示了程序的两次执行情况。在第一次执行中，为 `gallonsOfGas` 输入了一个可用的值，程序正常运行，跳过了 `catch` 块。然而，在第二次执行中，用户为 `gallonsOfGas` 输入了 0。当尝试进行除法时，会自动创建并抛出一个异常对象。`catch` 块捕获了该异常，它在这里被称为 `e`。（图 11-6 中的阴影箭头从创建异常的地方延伸到捕获异常的地方。）`catch` 块中的语句将 `mpg` 设置为 0 并显示消息。无论 `catch` 块是否执行，跟在 `catch` 块大括号之后的最后的 `WriteLine()` 语句都会执行。

```csharp
using System;
using static System.Console;

class MilesPerGallon2
{
    static void Main()
    {
        int milesDriven;
        int gallonsOfGas;
        int mpg;
        try
        {
            Write("Enter miles driven ");
            milesDriven = Convert.ToInt32(ReadLine());
            Write("Enter gallons of gas purchased ");
            gallonsOfGas = Convert.ToInt32(ReadLine());
            mpg = milesDriven / gallonsOfGas;
        }
        catch (Exception e)
        {
            mpg = 0;
            WriteLine("You attempted to divide by zero!");
        }
        WriteLine("You got {0} miles per gallon", mpg);
    }
}
```

图 11-6 MilesPerGallon2 程序

![](img/b0a31988f44670d0728c4f372d8dab77_525_0.png)

图 11-7 MilesPerGallon 程序的两次执行

当你编译图 11-6 中的程序时，你会收到一个警告，称 `e` 已声明但从未使用过。你可以声明一个变量来持有抛出的异常对象，但在示例中你不想使用它，所以你可以安全地忽略该警告。如果你不想在 `catch` 块中使用捕获的 `Exception` 对象，那么你就不需要为它提供实例名称。例如，在图 11-6 中，`catch` 子句可以这样开始：

```csharp
catch (Exception)
```

在本章稍后的示例中，`Exception` 对象将被用于提供信息。在这些情况下，要求必须有一个标识符。
