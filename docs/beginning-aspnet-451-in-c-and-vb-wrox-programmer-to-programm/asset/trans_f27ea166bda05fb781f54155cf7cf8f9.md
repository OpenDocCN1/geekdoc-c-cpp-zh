

# 组织代码

```
Public Sub SubByValDemo(someValue As Integer)  ' No ByVal needed as it's the default
someValue = someValue + 20
End Sub
```

```
Public Sub ByRefDemo(ByRef someValue As Integer)
someValue = someValue + 20
End Sub
```

```
Dim x As Integer = 0
ByValDemo(x)
```

```
Label1.Text = x.ToString()  ' Prints out 0; A copy of x is sent to ByValDemo,
  ' leaving the original value of x unmodified.
```

```
Dim y As Integer = 0
ByRefDemo(y)
```

```
Label1.Text = y.ToString()  ' Prints out 20; A reference to y is sent
  ' to ByRefDemo so when that method modified
  ' someValue, it also changed the variable y.
```

C# 有一个类似的构造，使用 ref 关键字。与 VB.NET 最大的不同是你需要在调用方法时指定 ref 关键字，如：

```
public void ByRefDemo(ref int someValue)
{
    someValue = someValue + 20;
}
```

```
int y = 0;  // Just as in the VB example, y contains 20
ByRefDemo(ref y);  // after the call to ByRefDemo
```

在使用此类引用参数时要小心；在你意识到之前它可能会改变调用代码中的重要变量。这会导致难以追踪的错误。

要使你的站点范围方法可供网站中的页面访问，你应该将它们放在集中位置。App_Code 文件夹是存放代码的完美位置。

## App_Code 文件夹

App_Code 文件夹是一个特殊的 ASP.NET 文件夹。它专门设计用于存放代码文件、你在整个站点中使用的类。仅适用于单个页面 的代码（如 Button 控件的 click 事件处理程序）应保留在页面的 Code Behind 中，如你迄今所见。

> 注意 App_Code 文件夹特定于 Web Site Projects，即用于 Planet Wix 网站的项目类型。另一方面，Web Application Projects 不使用也不支持 App_Code 文件夹。然而，该项目使你能够在几乎任何其他位置创建代码文件。请按照本章及后续章节中的示例进行操作，使用 Web Site Project 很重要，如第 2 章所述。

## 第 5 章 编程你的 ASP.NET 网页

将 App_Code 文件夹添加到你的站点，在 Solution Explorer 中右键单击站点的名称并选择 Add ASP.NET Folder App_Code。图 5-4 显示了新的文件夹。

有了 App_Code 文件夹后，你就可以开始向其中添加类文件。类文件具有与你为站点选择的编程语言相匹配的扩展名：C# 为 .cs，包含 VB.NET 代码的文件为 .vb。在这些类文件中，你可以创建包含方法（函数和子程序）的类，这些方法将在本章最后一节中更详细地讨论；现在，重点关注代码中的方法以及如何调用它们，而不是为什么首先需要将代码添加到类中。

下一个练习展示了如何使用 App_Code 文件夹来优化你在之前的 Try It Out 中创建的计算器。

![](img/9e033e3b9560597824f8b22941d6d8bb_207_0.png)

图 5-4

## 试一试 优化计算器

在此练习中，你创建一个类，该类公开四个方法：Add、Subtract、Multiply 和 Divide。当类设置好并能够执行必要的计算操作后，你修改 CalculatorDemo.aspx 文件，使其使用你的新 Calculator 类。虽然这是一个微不足道的例子，但它展示了你需要编写的代码量以及通过将代码从 ASPX 页面移动到 App_Code 文件夹以供其他应用程序重用而获得的额外灵活性，它足够全面，可以向你展示概念，又足够简短，可以让你理解代码。现在，只需关注计算器的工作原理以及如何调用其方法。在本章后面关于面向对象的部分，你将确切地了解类是什么。

- 1. 如果尚未执行，请通过右键单击站点并选择 Add ASP.NET Folder App_Code 来添加 App_Code 文件夹。
- 2. 右键单击此新创建的文件夹并选择 Add New Item。在随后出现的对话框中，选择适当的编程语言，然后单击 Class。代替 Add New Item，你也可以选择 Add Class，这可作为添加类文件的快捷方式。此快捷方式还意味着你最近添加到列表中的项目。
- 3. 输入 Calculator 作为文件的名称，然后单击 Add（如果使用快捷方式则单击 OK）。这会创建一个包含名为 Calculator 的类的类文件。请注意，使用 Pascal 命名法命名类是很常见的惯例，其中每个单词都以大写字母开头。
- 4. 在定义 Calculator 类的代码行之后立即添加以下方法，替换类中已有的任何代码：

VB.NET

Public Class Calculator

```
Public Function Add(a As Double, b As Double) As Double
Return a + b
End Function
```

```
Public Function Subtract(a As Double, b As Double) As Double
Return a - b
End Function
```

```
Public Function Multiply(a As Double, b As Double) As Double
Return a * b
End Function
```

```
Public Function Divide(a As Double, b As Double) As Double
Return a / b
End Function
```

End Class

# C#

```
public class Calculator
{
    public double Add(double a, double b)
    {
        return a * b;
    }

    public double Subtract(double a, double b)
    {
        return a - b;
    }

    public double Multiply(double a, double b)
    {
        return a * b;
    }

    public double Divide(double a, double b)
    {
        return a / b;
    }
}
```

- 5. 接下来，修改 CalculatorDemo.aspx 页面的 Code Behind，以便使用你刚刚创建的类。你需要进行两个更改：首先你需要添加一行代码来创建 Calculator 类的实例，然后你需要修改每个 Case 块以使用计算器中的相关计算器方法：

```
VB.NET
Dim myCalculator As New Calculator()
Select Case OperatorList.SelectedIndex
Case "+"
    result = myCalculator.Add(value1, value2)
Case "-"
    result = myCalculator.Subtract(value1, value2)
Case "*"
    result = myCalculator.Multiply(value1, value2)
```

```
Case "/"
result = myCalculator.Divide(value1, value2)
End Select
```

- 6. 保存所有更改并在浏览器中打开页面。计算器仍然像以前一样工作；只是这次计算不是在代码的 Code Behind 中进行，而是由 App_Code 文件夹中的 Calculator 类完成。

## 它是如何工作的

你在 App_Code 文件夹中创建的文件包含一个名为 Calculator 的类。你将在本章最后一节了解有关类的更多信息，但现在重要的是要知道类是对象的定义，该对象可以在运行时公开可调用的方法。在这种情况下，Calculator 类的定义包含四个执行算术运算的方法。这些方法接受计算左右两侧的参数。每个方法只是执行请求的计算（Add、Subtract 等）并将结果返回给调用代码。

CalculatorDemo.aspx 页面中的代码创建了 Calculator 类的一个实例。也就是说，它基于类定义在计算机内存中创建了一个对象。为此，它使用 New（在 C# 中）关键字创建 Calculator 的一个实例，然后将其存储在变量 myCalculator 中。你将在本章后面讨论对象时了解有关 New 关键字的更多信息。请注意此变量的数据类型是 Calculator，即类的名称。

```
VB.NET
Dim myCalculator As New Calculator()
```

```
C#
Calculator myCalculator = new Calculator();
```

一旦创建了 Calculator 实例，你就可以调用其方法。就像你之前看到的其他方法一样，Calculator 的方法接受由调用代码传入的类参数：

```
VB.NET
```

```
Case "*"
```

```
result = myCalculator.Add(value1, value2)

#
case "*":
    result = myCalculator.Add(value1, value2);
    break;
```

该方法然后将两个值相加并将结果作为 Double 返回，该结果存储在变量 result 中。由于在计算器的第一个版本中，最后结果会使用 Label 控件显示在页面上。

函数和子程序是组织 Web 应用程序的好方法。它们使你能够创建可重用的代码块，可以从其他位置轻松调用。因为只需要定义一次需要多次使用的代码，所以维护或扩展代码变得容易得多。如果你在一个函数中发现了错误，只需在 App_Code 文件夹中修复其定义，所有使用该函数的页面都会自动受益于更改。除了可维护性更高之外，函数和子程序还使你的代码更易于阅读：与其在页面中浏览冗长的代码列表，你只需调用一个函数并使用返回值（如果有）。这对大脑更友好，减少了应用程序中出现错误的可能性。

函数和子程序并不是在 .NET 项目中组织代码的唯一方法。另一种方法是使用命名空间。

## 使用命名空间组织代码

命名空间似乎给新开发者带来了很多困惑。他们认为它们很可怕，认为存在太多，或者看不到使用它们的必要性。所有这些都是错误的，通过对它们的简短解释，你将理解并甚至喜欢命名空间。

命名空间旨在解决两个主要问题：组织 .NET Framework 中的庞大功能量以及避免冲突，即不同类型共享相同名称时的问题。关于命名空间的一个常见误解是 .NET 程序集（具有 .dll 扩展名，由 .NET Framework 加载和使用的文件）之间存在直接关系，但事实并非如此。虽然你通常会在名为 System.Web.dll 的 DLL 中找到像 System.Web.UI 这样的命名空间，但可以在单个 DLL 中定义多个命名空间，或将命名空间分布在多个程序集中也是可能且常见的。请记住在添加程序集引用时这一点，如解释所述。

要查看命名空间的样子，请打开迄今为止创建的 ASPX 页面的 Code Behind 文件之一。你会看到类似以下内容的一切：

# VB.NET

```
Partial Class Demos_CalculatorDemo
    Inherits System.Web.UI.Page
```

# C#

```
public partial class Demos_CalculatorDemo : System.Web.UI.Page
{
```

