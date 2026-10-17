
输出：

Area of rectangle is 40
Area of triangle is 20

通用委托通过创建名为 `r` 和 `t` 的两个对象实例化两次，其中实例 `r` 被设置为引用 `Rect` 方法（该方法返回 `int` 并接收单个 `int` 类型参数）。实例 `t` 设置为引用 `Triangle` 方法，该方法返回 `float` 类型并接收该类型的单个参数。两个实例 `r` 和 `t` 分别被调用以执行 `Rect` 和 `Triangle` 方法。

如果你想对前面的程序做一些微小的改动呢？你想让 `Triangle` 方法接收 `int` 参数，但返回 `float` 类型的结果。（你想让 `Triangle` 方法的返回类型和参数类型不同）。

## 第11章 委托与事件

要创建更改，请修改之前的 `GenericDelegate.cs` 程序（参见列表 11.9），使其显示如列表 11.10 所示。只有**粗体**语句被修改了。其余部分与列表 11.9 相同。

### 列表 11.10 GenericDelegate.cs 文件中的程序代码

```c
using System;

public delegate T2 Calculate<T1, T2>(T1 arg1, T1 arg2);

class GenericDelegate
{
    static void Main(string[] args)
    {
        Calculate<int, int> r=new Calculate<int, int>(Rect);
        Console.WriteLine("Area of rectangle is " +r(5,8));
        Calculate<int, float> t=new Calculate<int, float>(Triangle);
        Console.WriteLine("Area of triangle is " +t(5,8));
    }
    static float Triangle(int x, int y)
    {
        return (float)1/2*x*y;
    }
    static int Rect(int x, int y)
    {
        return x *y;
    }
}
```

输出：
Area of rectangle is 40
Area of triangle is 20

你可以看到 `Triangle` 方法被修改为接受 `int` 类型的参数并返回 `float` 类型的结果。此外，在代码中，你看到声明 `Calculate` 委托时指定了两个类型 `T1` 和 `T2`。当你创建委托实例 `r` 来引用 `Rect` 方法时，返回类型和参数类型都作为 `int` 提供。显然，由于 `Rect` 方法中的返回类型和参数类型都是 `int` 类型。

在定义委托实例 `t` 时，提供的类型是 `int` 和 `float`，因为 `Triangle` 方法接收 `int` 类型的参数并返回 `float` 类型的结果。委托实例 `r` 和 `t` 都被用来调用它们各自的方法 `Rect` 和 `Triangle`。

## 匿名方法

除了使用命名方法外，C# 还允许你使用匿名方法来处理委托。匿名方法允许声明内联方法，内联方法使用 `delegate` 关键字而不是方法名后跟括号包裹的方法体。如果委托带有参数，你将它们传递给匿名方法，并将它们放在 `delegate` 关键字后的括号中。如果委托没有参数，使用 `delegate` 关键字后跟空括号或完全没有括号。

列表 11.11 所示的 `Anonymous1.cs` 程序演示了匿名方法的调用。

### 列表 11.11 Anonymous1.cs 文件中的程序代码

```c
using System;

public delegate void AddVal(int x, int y);

class Anonymous1 {
  static void Main() {
    AddVal addvalues = delegate(int a, int b) {
      Console.Write("Addition is {0}", a+b);
    };
    addvalues(10,20);
  }
}
```

输出：

Addition is 30

你可以在前面的程序中看到声明了一个返回 `void`（无）的委托 `AddVal`。在 `Main()` 函数中，创建了 `AddVal` 委托的实例 `addvalues`，并通过匿名方法通过委托关键字和包含的参数传递代码块给它。传递给 `addvalues` 委托的代码块是匿名方法，当调用 `addvalues()` 方法时将会被调用。匿名方法的定义以分号（`;`）结束。匿名方法通过 `addvalues()` 方法调用。在调用 `addvalues()` 方法时使用了参数 10 和 20，然后将其赋值给匿名方法的参数 `a` 和 `b`。随后在屏幕上显示参数的相加结果。

列表 11.12 所示的 `Anonymous2.cs` 程序演示了返回值的匿名方法。如预期的，你只需要确保匿名方法返回的值的类型与委托指定的返回类型兼容即可。

### 列表 11.12 Anonymous2.cs 文件中的程序代码

```c
using System;

public delegate int AddVal(int x, int y);

class Anonymous2 {
    static void Main() {
        int k;
        AddVal addvalues = delegate(int a, int b) {
            return a+b;
        };
        k=addvalues(10,20);
        Console.Write("Addition of 10 and 20 is {0}", k);
    }
}
```

输出：

Addition of 10 and 20 is 30

在使用完前面的委托示例后，你可能会认为委托和接口是相同的。它们实际上非常不同。请继续阅读。

## 委托与接口之间的区别

用委托完成的任务也可以用接口完成。例如，列表 11.1 所示的 `Delegate1.cs` 程序可以用接口编写，如列表 11.13 所示。

### 列表 11.13 InterfaceApp.cs 文件中的程序代码

```c
interface Calculate
{
    int Rect();
}

class InterfaceApp : Calculate {
    int l,b;
    public InterfaceApp(int x, int y) {
        l=x;
        b=y;
    }
    public int Rect()
    {
        return 1*b;
    }
    public static void Main()
    {
        InterfaceApp r = new InterfaceApp(5,8);
        System.Console.WriteLine("Area of rectangle is {0}", r.Rect());
    }
}
```

## 输出：

Area of rectangle is 40

虽然委托和接口都包含声明，但它们之间存在显著差异。委托和接口的特征清楚地区分了两者。

以下是委托的特征：

-   委托只有声明。委托不提供任何实现。它们只是安全的回调或函数指针。
-   委托可以引用类中的任何方法，只要参数和返回类型与其自身的类型匹配。因此，委托有助于“匿名”调用。
-   当一个类可能需要一个方法的多个实现时，优选使用委托。

以下是接口的特征：

-   接口只包含方法的声明，不包含定义或实现代码。方法的实现在类中完成。
-   接口允许你扩展某些对象的功能或行为。
-   接口可以被继承。事实上，接口在 C# 中用于模拟多重继承。
-   接口调用比委托调用快。
-   可以创建接口的实例。
-   通过委托调用方法是间接的。
-   首先访问方法指针，然后调用相关的方法。接口引用是对实现接口的对象的实例的引用。通过接口引用调用方法更快。
-   当一个类只需要方法的某一种实现时，优选接口。

## 事件处理

事件是任务的启动器。按下回车键或点击鼠标是在处理任何应用程序或程序时创建或发生的常见事件。C# 事件是类的成员，当发生特定的指定事件（动作）时，会被触发。如果你想在事件发生时收到通知，你需要对它进行注册。当事件发生时，注册的方法会自动调用。方法的注册是通过指定注册方法签名的委托完成的。事件发生时调用的方法被称为事件处理器。事件发生时运行的代码封装在事件处理器中。一个事件可以有多个处理器，因此定义事件是一个两步过程。首先，你需要定义一个指定事件触发时调用的委托类型。其次，你需要使用 C# 关键字声明事件以标识相关的委托类型。

## 声明事件

要声明事件，必须为它应该关联的事件声明委托。例如，以下语句声明了一个名为 `Calculate` 的委托，它可以引用接受两个 `int` 类型参数且不返回任何内容的方法：

```c
delegate void Calculate(int x, int y);
```

声明委托后，使用以下语法声明事件：

`public event delegate_name event_name`

例如，以下语句定义了一个名为 `Calculate` 的委托和一个名为 `EventToCalculate` 的事件，后者在事件触发时会调用该委托：

```c
public static event Calculate EventToCalculate;
```

换句话说，事件可以持有委托，并且可以被用来调用与关联委托签名匹配的方法。而不是直接调用方法

# 事件处理 355

直接使用委托时，事件被调用或触发，然后它会调用委托，由委托调用引用的方法。

你可以使用 `+=` 运算符向事件添加委托。将委托实例添加到事件的语法如下：

`event_name+= delegate_instance;`

要调用事件和事件处理程序（由委托引用的方法），你需要指定事件名称以及任何所需的参数（由关联的委托定义）。

列表 11.14所示的 `EventDemo.cs` 程序演示了事件是如何触发的，以及与事件关联的事件处理程序是如何调用的。程序声明了一个名为 `Calculate` 的委托，该委托可以引用接受两个 `int` 类型参数且没有返回值的方法。声明了一个名为 `EventCalculate` 的事件，当事件发生或触发时，会调用 `Calculate` 委托。

### 列表 11.14 EventDemo.cs 文件中的代码

```csharp
using System;

delegate void Calculate(int x, int y);

class EventDemo
{
    public static event Calculate EventToCalculate;
    static void Rect(int x, int y)
    {
        Console.WriteLine("Area of rectangle is {0}", x*y);
    }
    static void Main()
    {
        EventToCalculate+=new Calculate(Rect);
        EventToCalculate(5,8);
    }
}
```

## 输出：

Area of rectangle is 40

你可以看到定义了一个静态方法 `Rect`，它接受两个 `int` 参数来计算矩形的面积。`Rect` 方法只是简单地显示计算出的矩形面积，而不返回任何内容。创建了一个引用 `Rect` 方法的委托实例。使用 `+=` 运算符将该委托实例添加到事件 `EventToCalculate` 中。`EventToCalculate` 传递了两个 `int` 参数：5 和 8。`EventToCalculate` 调用了 `Calculate` 委托，委托转调用引用的方法。值 5 和 8 被赋予 `Rect` 方法，从而显示了矩形的面积。

## 注意

在前面的程序中调用的 `Rect` 方法被称为事件处理程序。

一个事件可以关联多个事件处理程序。列表 11.15 所示的 `EventProg.cs` 程序演示了当单个事件发生时如何调用多个事件处理程序。程序声明了一个名为 `EventHandler` 的委托，它可以引用一个没有参数且没有返回值的方法。声明了一个名为 `dispMessage` 的事件，当事件发生时调用 `EventHandler` 委托。

### 列表 11.15 EventProg.cs 文件中的代码

```csharp
using System;

delegate void EventHandler();

class EventProg
{
    public static event EventHandler dispMessage;
    static void Main()
    {
        dispMessage += new EventHandler(handler1);
        dispMessage += new EventHandler(handler2);
        dispMessage += new EventHandler(handler3);
    }
    static void handler1()
    {
        Console.WriteLine("This is event handler 1");
    }
    static void handler2()
    {
        Console.WriteLine("This is event handler 2");
    }
    static void handler3()
    {
        Console.WriteLine("This is event handler 3");
    }
}
```

## 输出：

This is event handler 1
This is event handler 2
This is event handler 3

你可以看到定义了三个静态方法：`handler1`、`handler2` 和 `handler3`，它们不接受参数并简单的显示消息。使用 `+=` 运算符将三个处理程序方法添加到事件（其调用列表）中。也就是说，创建了三个 `EventHandler` 委托实例，它们被添加到 `dispMessage` 事件。在实例 `p` 上调用的 `Invoke` 方法触发了 `dispMessage` 事件。如预期所示，`dispMessage` 调用了 `EventHandler` 委托，委托转调用 `p` 实例的方法。

在之前的两个程序中，你学习了在事件发生时调用静态方法。列表 11.16 所示的 `EventDelg.cs` 程序演示了在事件发生时调用类方法。程序声明了一个名为 `ProductDelegate` 的委托，它可以引用一个没有参数且没有返回值的方法。定义了一个名为 `Product` 的类，包含一个名为 `qty` 的数据成员。该类还包含一个初始化数据成员 `qty` 的构造函数。类定义了两个成员方法：`RaiseEvent` 和 `Display`。声明了一个名为 `ProductEvent` 的事件，当事件发生时调用 `ProductDelegate` 委托。

### 列表 11.16 EventDelg.cs 文件中的代码

```csharp
using System;

public delegate void ProductDelegate();

public class Product
{
    event ProductDelegate ProductEvent;
    int qty;
    public Product(int v)
    {
        qty=v;
    }
    public void RaiseEvent()
    {
        ProductEvent();
    }
    public void Display()
    {
        Console.WriteLine("Product quantity is {0}", qty);
    }
}

class EventDelg
{
    static void Main()
    {
        Product p = new Product(10);
        p.ProductEvent += new ProductDelegate(p.Display);
        p.RaiseEvent();
    }
}
```
