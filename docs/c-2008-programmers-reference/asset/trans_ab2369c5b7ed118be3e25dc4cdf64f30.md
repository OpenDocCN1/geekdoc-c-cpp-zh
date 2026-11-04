
使用异步回调时，可以通过在不同线程中执行程序的不同部分，使程序更具响应性。

*第10章更详细地讨论了线程。*

## 匿名方法和 Lambda 表达式

从 C# 2.0 开始，您可以使用称为匿名方法的特性来定义委托。
匿名方法是一个“内联”的语句或表达式，可用作委托参数。
要了解其工作原理，请看以下示例：

```csharp
class Program
{
    delegate void MethodsDelegate(string Message);

    static void Main(string[] args)
    {
        MethodsDelegate method = Method1;

        //---call the delegated method---
        method("Using delegate.");
        Console.ReadLine();
    }

    static private void Method1(string Message)
    {
        Console.WriteLine(Message);
    }
}
```

而不是定义一个单独的方法然后使用委托变量指向它，您可以使用匿名方法来缩短代码：

```csharp
class Program
{
    delegate void MethodsDelegate(string Message);

    static void Main(string[] args)
    {
        MethodsDelegate method = delegate(string Message)
        {
            Console.WriteLine(Message);
        };

        //---call the delegated method---
        method("Using anonymous method.");
        Console.ReadLine();
    }
}
```

## 第一部分：C# 基础

在此表达式中，方法委托是一个匿名方法：

```csharp
MethodsDelegate method = delegate(string Message)
{
    Console.WriteLine(Message);
};
```

匿名方法在使用委托时消除了定义单独方法的需要。如果委托方法只包含几条简单语句并且不被其他代码使用，这很有用，因为您无需创建单独的方法，从而减少了实例化委托的编码开销。

在 C# 3.0 中，匿名方法可使用称为 lambda 表达式的新特性进一步缩短。Lambda 表达式是 .NET 3.5 中的新特性，它为编写匿名方法提供了更简洁、函数式的语法。

上述使用匿名方法的代码可使用 lambda 表达式重写：

```csharp
class Program
{
    delegate void MethodsDelegate(string Message);

    static void Main(string[] args)
    {
        MethodsDelegate method = (Message) => { Console.WriteLine(Message); };

        //--call the delegated method--
        method("Using Lambda Expression.");

        Console.ReadLine();
    }
}
```

Lambda 表达式将在第 14 章中更详细地讨论。

## 事件

计算机科学中最重要的技术之一，它使得当今的图形用户界面操作系统（如 Windows、Mac OS X、Linux 等）成为可能，就是事件驱动编程。事件驱动编程让操作系统能够对用户做出的不同点击做出适当反应。典型的 Windows 应用程序具有各种小部件，如按钮、单选按钮和复选框，当用户点击它们时可以引发事件。程序员只需编写代码来处理特定事件。事件的好处在于，您无需知道这些事件何时会被引发——您只需为将处理事件的事件处理程序提供实现，操作系统就会负责适当地调用必要的事件处理程序。

在 .NET 中，事件使用委托实现。具有事件的对象称为发布者。订阅事件（换句话说，处理事件）的对象称为订阅者。当对象公开事件时，它会定义一个委托，以便任何想要处理此事件的对象都必须

为此委托提供一个函数。此委托称为事件，而处理此委托的函数称为事件处理程序。事件是每个 Windows 应用程序不可或缺的一部分。例如，使用 Visual Studio 2008 您可以创建一个包含 Button 控件的 Windows 应用程序（见图 7-4）。

![](img/a977a875c7c627b45d939729705a252e_250_0.png)

当您双击 Button 控件时，会自动为您添加一个事件处理程序：

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
    }

    private void button1_Click(object sender, EventArgs e)
    {
    }
}
```

但您的应用程序如何知道哪个事件处理程序对应哪个事件？事实证明，Visual Studio 2008 会在窗体的代码隐藏文件（FormName.Designer.cs；见图 7-5）中自动连接事件处理程序，该文件位于名为 InitializeComponent() 的函数中：

```csharp
this.button1.Location = new System.Drawing.Point(12, 12);
this.button1.Name = "button1";
this.button1.Size = new System.Drawing.Size(75, 23);
this.button1.TabIndex = 0;
this.button1.Text = "button1";
this.button1.UseVisualStyleBackColor = true;
this.button1.Click += new System.EventHandler(this.button1_Click);
```

![](img/a977a875c7c627b45d939729705a252e_250_1.png)

## 第一部分：C# 基础

请注意，将事件处理程序连接到处理 Click 事件的方式与将方法名分配给委托的方式类似。

或者，您可以手动创建 Button 控件的 Click 事件的事件处理程序。在 Form() 构造函数中，在 Click 事件后输入 += 并按 Tab 键。Visual Studio 2008 会自动完成该语句（见图 7-6）。

![](img/a977a875c7c627b45d939729705a252e_251_0.png)

图 7-6

再按一次 Tab 键，Visual Studio 2008 会为您插入事件处理程序的存根（见图 7-7）。

![](img/a977a875c7c627b45d939729705a252e_251_1.png)

图 7-7

完成的代码如下所示：

```csharp
public Form1()
{
    InitializeComponent();
    this.button1.Click += new EventHandler(button1_Click);
}

void button1_Click(object sender, EventArgs e)
{
}
```

请注意，Click 是事件，事件处理程序必须与事件所需的签名匹配（在这种情况下，Click 事件的事件处理程序必须有两个参数——object 和 EventArgs）。按照惯例，.NET Framework 中的事件处理程序返回 void 并有两个参数。第一个是事件的来源（即引发此事件的对象），第二个是从 EventArgs 派生的对象。EventArgs 参数允许数据从事件传递到事件处理程序。EventArgs 类将在本章后面进一步讨论。

使用 C# 3.0 中的新 lambda 表达式，前面的事件处理程序也可以这样写：

```csharp
public Form1()
{
    InitializeComponent();
    this.button1.Click += (object sender, EventArgs e) =>
    {
        MessageBox.Show("Button clicked!");
    };
}
```

## 处理事件

让我们通过几个简单示例来看看如何处理事件。Timer 类（位于 System.Timers 命名空间中）是一个在固定间隔生成一系列重复事件的类。您通常使用 Timer 类执行一些后台任务，例如在从服务器下载文件时更新 ProgressBar 控件，或显示当前时间。

Timer 类有一个您需要处理的重要事件——Elapsed。每次设定的时间间隔过去时，Elapsed 事件就会被触发。

以下程序展示了如何使用 Timer 类在控制台窗口中显示当前时间：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Runtime.Remoting.Messaging;
using System.Timers;
namespace Events
{
    class Program
    {
        static void Main(string[] args)
        {
            Timer t = new Timer(1000);
            t.Elapsed += new ElapsedEventHandler(t_Elapsed);
            t.Start();
            Console.ReadLine();
        }

        static void t_Elapsed(object sender, ElapsedEventArgs e)
        {
            Console.SetCursorPosition(0, 0);
            Console.WriteLine(DateTime.Now);
        }
    }
}
```
