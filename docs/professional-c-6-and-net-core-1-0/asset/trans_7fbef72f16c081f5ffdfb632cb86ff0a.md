
如果基类的方法声明为 `virtual` 并且用途相同，就重写该方法。但是，如果其他方法已经调用了此方法，简单的重命名可能会导致其他代码被破坏。

> **注意** 不应故意使用 `new` 方法修饰符来隐藏基类的成员。该修饰符的主要目的是处理版本冲突，并在派生类完成后应对基类的更改。

## 调用方法的基类版本

C# 有一种特殊的语法可以从派生类调用方法的基类版本：`base.<MethodName>`。例如，你在基类 `Shape` 中声明了 `Move` 方法，并希望在派生类 `Rectangle` 中调用它，以使用基类中的实现。要添加派生类的功能，你可以使用 `base` 调用它（代码文件 `VirtualMethods/Shape.cs`）：

```csharp
public class Shape
{
    public virtual void Move(Position newPosition)
    {
        Position.X = newPosition.X;
        Position.Y = newPosition.Y;
        WriteLine($"moves to {Position}");
    }
    //... other members
}
```

`Move` 方法在 `Rectangle` 类中被重写，以便将 `Rectangle` 字样输出到控制台。在写入此文本后，使用 `base` 关键字调用基类的方法（代码文件 `VirtualMethods/ConcreteShapes.cs`）：

```csharp
public class Rectangle: Shape
{
    public override void Move(Position newPosition)
    {
        Write("Rectangle");
        base.Move(newPosition);
    }
    //... other members
}
```

现在将矩形移动到新位置（代码文件 `VirtualMethods/Program.cs`）：

```csharp
r.Move(new Position { X = 120, Y = 40 });
```

运行应用程序，查看 `Rectangle` 和 `Shape` 类中 `Move` 方法执行后的输出结果：

```
Rectangle moves to X: 120, Y: 40
```

> **注意** *使用* `base` *关键字可以调用基类的任何方法——而不仅仅是已被重写的方法。*

## 抽象类与抽象方法

C# 允许将类和方法声明为抽象。抽象类不能被实例化，而抽象方法没有实现，并且必须在任何非抽象的派生类中重写。显然，抽象方法*自动*是虚拟的（尽管你不需要提供 `virtual` 关键字，这样做反而会导致语法错误）。如果某个类包含任何抽象方法，那么该类也是抽象的，并且也必须声明为抽象。

让我们将 `Shape` 类改为 `abstract`。这样一来，就必须从该类派生。新的 `Resize` 方法被声明为抽象，因此它不能在 `Shape` 类中有任何实现（代码文件 `VirtualMethods/Shape.cs`）：

```csharp
public abstract class Shape
{
    public abstract void Resize(int width, int height);   // abstract method
}
```

从抽象基类派生类型时，必须实现所有抽象成员。否则，编译器会报错：

```csharp
public class Ellipse : Shape
{
    public override void Resize(int width, int height)
    {
        Size.Width = width;
        Size.Height = height;
    }
}
```

当然，实现也可以像下面的示例这样。抛出类型为 `NotImplementedException` 的异常也是一种实现，只是这不是预期中的实现，通常只是开发期间的临时实现：

```csharp
public override void Resize(int width, int height)
{
    throw new NotImplementedException();
}
```

> **注意** *异常将在第14章“错误与异常”中详细说明。*

使用抽象的 `Shape` 类和派生的 `Ellipse` 类，你可以声明一个 `Shape` 类型的变量。你不能实例化它，但可以实例化一个 `Ellipse`，并将其赋值给 `Shape` 变量（代码文件 `VirtualMethods/Program.cs`）：

```csharp
Shape s1 = new Ellipse();
DrawShape(s1);
```

## 密封类与密封方法

如果不允许创建从你的类派生的类，那么你的类应该是 sealed。给类添加 `sealed` 修饰符后，就不允许你创建它的子类。密封一个方法意味着无法重写该方法。

```csharp
sealed class FinalClass
{
    // etc
}

class DerivedClass : FinalClass        // wrong. Cannot derive from sealed class.
{
    // etc
}
```

最有可能将类或方法标记为 sealed 的情况是：该类或方法对你正在编写的库、类或其他类的内部操作至关重要，而任何试图重写其某些功能的尝试都可能导致代码不稳定。例如，也许你尚未对继承进行过测试，也没有为继承的设计决策投入精力。如果是这种情况，最好将你的类标记为 sealed。

密封类还有另一个原因。对于 sealed 类，编译器知道不可能有派生类，因此用于虚拟方法的虚表（virtual table）可以被缩减或消除，从而提高性能。`string` 类就是 sealed 的。由于我还没有见过哪个应用程序不使用字符串，因此最好让这个类型尽可能高效。将类设为 sealed 对编译器来说是一个很好的提示。

将方法声明为 sealed 的目的与类相似。该方法可以是从基类重写而来的方法，但在下面的示例中，编译器知道另一个类不能为此方法扩展虚表；它到此为止。

```csharp
class MyClass : MyBaseClass
{
    public sealed override void FinalMethod()
    {
        // implementation
    }
}

class DerivedClass : MyClass
{
    public override void FinalMethod()  // wrong. Will give compilation error
    {
    }
}
```

要在方法或属性上使用 `sealed` 关键字，它必须首先从基类重写。如果你不希望基类中的方法或属性被重写，那就不要将其标记为 virtual。

## 派生类的构造函数

第3章讨论了构造函数如何应用于各个类。一个有趣的问题出现了：当你开始为层次结构中的类定义自己的构造函数时，会发生什么？这些类继承自其他可能也带有自定义构造函数的类。

假设你没有为任何类定义任何显式构造函数。这意味着编译器会为你的所有类提供默认的零初始化构造函数。实际上，这种情况发生时，底层会有很多事情在运作，但编译器能够进行安排，使整个类层次结构中的一切都能顺利运作，并且每个类中的每个字段都被初始化为其默认值。然而，当你添加自己的构造函数时，实际上就控制了构造过程。这会一直影响到派生类的整个层次结构，因此你必须确保不会无意中做任何阻碍构造过程在层次结构中顺利进行的事情。

你可能会想，为什么派生类会存在什么特殊问题。原因在于，当你创建派生类的实例时，有多个构造函数在起作用。你实例化的类的构造函数本身不足以初始化该类；还必须调用基类的构造函数。这就是我们一直在讨论的通过层次结构进行构造的原因。

在之前的 `Shape` 类型示例中，属性是使用自动属性初始化器初始化的：

```csharp
public class Shape
{
    public Position Position { get; } = new Position();
    public Size Size { get; } = new Size();
}
```

在幕后，编译器会为类创建一个默认构造函数，并将属性初始化器移入该构造函数中：

```csharp
public class Shape
{
    public Shape()
    {
        Position = new Position();
        Size = new Size();
    }
    public Position Position { get; }
    public Size Size { get; }
}
```
