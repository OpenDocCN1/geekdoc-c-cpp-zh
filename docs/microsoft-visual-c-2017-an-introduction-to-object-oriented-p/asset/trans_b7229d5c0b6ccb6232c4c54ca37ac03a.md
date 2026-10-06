

# 第 11 章 异常处理

DivideByZeroException 对象是由 C# 自动生成的。它是 DivideByZeroException 类的实例，该类有四个祖类。它是 ArithmeticException 类的子类，而 ArithmeticException 类派生自 SystemException 类。SystemException 类又派生自 Exception 类，而 Exception 类是是 Object 类的子类。

仅仅因为发生了异常并创建了 Exception 对象，并不意味着你必须去处理它。在 MilesPerGallon 类中，你只管让出错的程序终止即可；这就是为什么图 11-2 中的错误消息显示异常为“已处理（Handled）”。然而，程序的终止是突然且不留情的。当程序对两个数字除法或执行其他任务（如玩游戏）时，如果程序突然结束，用户可能会感到恼。如果程序用于空中交通控制或监测手术期间患者的体征，突然结束可能是灾难性的。通过异常处理，程序在处理问题后可以继续运行。这对于任务关键型应用（mission-critical applications）尤为重要。“任务关键型”一词是指任何对组织至关重要的过程。面向对象的错误处理技术比简单的关闭提供了更优雅的解决方案。

恰当处理异常的程序被认为比不处理的程序更具容错性和健壮性。容错异常的设计使得当系统部分发生故障时，它们能够继续运行（可能处于降低的水平）。健壮性代表了系统抵抗压力并保持正确功能的程度。

观看视频 System Exceptions（系统异常）。

| 两个真理和一个谎言 |
| :--- |
| 理解异常 |
| 1. 异常是执行中程序中的任何错误状况或意外行为。 |
| 2. 在 C# 中，所有异常都是 Exception 类或其某个派生类的成员对象。 |
| 3. 在 C# 中，当发生异常并创建 Exception 对象时，你必须使用一套特定的异常处理技术来管理问题。 |

> 它被创建了，你并不一定必须去处理它。错误的陈述是 #3。仅仅因为发生了异常且一个 Exception 是

# 你来做

## 故意引发异常

在许多情况下，C#会自动生成 SystemExceptions。在接下来的步骤中，你将通过执行一个提供多次异常机会的程序来故意生成一个 SystemException。

-   启动名为 ExceptionsOnPurpose 的新项目，并输入以下程序，它允许你生成几种不同的异常。
```csharp
using System;
using static System.Console;
class ExceptionsOnPurpose
{
    static void Main()
    {
        int answer;
        int result;
        int zero = 0;
        Write("Enter an integer >> ");
        answer = Convert.ToInt32(ReadLine());
        result = answer / zero;
        WriteLine("The answer is " + answer);
    }
}
```

-   你不能除以未命名的 0（通过将除法语句改为 `result = answer / 0`），也不能将变量 `zero` 更改为命名常量（通过在 `int` 声明开头插入 `static`）。如果你对这些任何一项进行更改，程序将无法编译，因为编译器可以确定将发生除以零的操作。然而，使用变量而不是未命名或命名的常量，编译器“信任”在除法发生之前会为该变量提供一个合法的值（尽管在这种情况下，这种信任并非必要的）。保存程序并编译它。

-   使用不同的输入值多次执行程序，并观察结果。第一次报告每次执行时出现 Windows 窗口。三个窗口显示 Windows 正在检查问题的解决方案，第二次报告它正在收集有关问题的更多信息。该窗口很快被图 11-3 所示的第三个窗口取代，反复显示 ExceptionsOnPurpose.exe 已停止。你永远不会编写一个故意除以零的程序；你在这里这样做是为了演示 C# 的异常生成能力。如果你正在运行专业应用程序，你可能会收到解决方案的通知。由于你是故意创建此异常的，只需点击关闭按钮。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_516_0.png)

**图 11-3** 由未处理的异常生成的错误报告窗口

-   **seven**——这会产生 FormatException，因为整数不允许包含字母。
-   **7.7**——这也会产生 FormatException，因为不允许包含小数点。
-   **7**——这会产生 FormatException，因为这是不允许的。
-   **7**——这会产生 DivideByZeroException：尝试除以零（Attempted to divide by zero）。

# 第 11 章 异常处理

## 比较传统方法与面向对象的方法

使用异常处理代替决策来控制错误的另一个优势是：当程序的逻辑逻辑被一组可能检测错误的 `if` 语句和决策中断时，程序可能会变得更加复杂且难以理解。面向对象的错误处理方法将程序的主任务与处理罕见异常的代码分开。

程序员使用“晴天日（sunny day）”一词来描述一切顺利且没有发生错误的情况。

## 理解面向对象的异常处理

面向对象的异常处理三个三个术语：try、throw 和 catch。

-   你“尝试（try）”一个可能无法正确完成的过程。
-   检测到错误状况的方法“抛出（throw）”异常。
-   处理错误的代码块“捕获（catch）”异常。

当你编写可能出现问题的代码块时，可以将代码放在 `try` 块中，它由以下元素组成：

-   关键字 `try`
-   一对大括号，包含可能引发异常的语句

`try` 后面必须至少跟一个 `catch` 块或 `finally` 块。（你将在本章稍些之后学习 `finally` 块）。每个 `catch` 块可以“捕获”一种类型的异常——即一个 Exception 对象或其子类对象的对象。程序员有时将 `catch` 块称为 `catch` 子句。你可以通过输入以下元素创建 `catch` 块：

-   关键字 `catch`
-   括号，包含一个 Exception 类型并（可选地）为该 Exception 类型的实例命名
-   一对大括号，包含处理错误状况的语句

```csharp
if(gallonsDriven == 0)
  mpg = milesDriven;
else
  mpg = 0;
```

