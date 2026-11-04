
显然，我们现在也可以在 Student 类上重写 `ToString` 方法。在这里，调用基类的 `ToString` 方法变得很有用，只需将子类附加信息追加到它后面即可：

```csharp
public override string ToString()
{
    return base.ToString() + " and attends " + College;
}
```

一旦这样做，前述示例代码中对 `ToString` 的调用就会分派到更派生的 Student 类型的 `ToString` 实现上。

## Declaring Virtual Members

为了从不同角度说明虚拟成员的概念，让我们定义另一个类型层次结构，在其中我们自己声明虚拟成员（而不是重写来自 `System.Object` 的成员）。一个很好的例子是 Shape 的概念，它可以被查询其面积和周长。根据 Shape 的子类，这些值的计算方式会有所不同：

```csharp
class Shape
{
    public virtual double Area
    {
        get { return 0.0; }
    }

    public virtual double Circumference
    {
        get { return 0.0; }
    }
}
```

目前，我们为这些虚拟属性 getter 使用默认实现，它们看起来似乎不会产生很有意义的值。稍后，在你学习了抽象类和成员之后，我们将讨论如何完全省略此类实现。

现在让我们定义几个子类 Circle 和 Square，它们对两个指标的计算都相当简单。我们通过重写来定义这些计算：

```csharp
class Circle : Shape
{
    public Circle(double radius)
    {
        Radius = radius;
    }

    public double Radius { get; private set; }

    public override double Area
    {
        get { return Math.PI * Radius * Radius; }
    }

    public override double Circumference
    {
        get { return Math.PI * 2 * Radius; }
    }
}

class Square : Shape
{
    public Square(double side)
    {
        Side = side;
    }

    public double Side { get; private set; }

    public override double Area
    {
        get { return Side * Side; }
    }

    public override double Circumference
    {
        get { return 4 * Side; }
    }
}
```

在输入此代码时，IntelliSense 会通过建议仍可重写的成员来帮助我们。有了这段代码，我们就可以编写多态代码：

```csharp
Shape s1 = new Circle(2.0);
Console.WriteLine(s1.Area);
Shape s2 = new Square(3.0);
Console.WriteLine(s2.Circumference);
```

## Sealing and Hiding: Take Two

如前所述，sealed 关键字会阻止类被进一步派生。我们也可以在更细粒度的成员级别上应用这种特化防止。例如，虽然我们可以让 Square 类型保持未密封（默认值），但我们可以防止人们重写我们已定义的虚拟属性：

```csharp
class Square : Shape
{
    public Square(double side)
    {
        Side = side;
    }

    public double Side { get; private set; }

    public sealed override double Area
    {
        get { return Side * Side; }
    }

    public sealed override double Circumference
    {
        get { return 4 * Side; }
    }
}
```

现在如果有人进来并定义了 Square 的子类，例如 ColoredSquare，就不再可能重写计算属性 Area 或 Circumference。

关于使用 new 修饰符进行隐藏，可以隐藏继承的成员，包括虚拟成员，但 override 和 new 的组合是没有意义的。毕竟，同时声明你隐藏基成员又坚持重写基成员意味着什么？首先你要求完全定义一个不同的成员，接下来你又想重写基成员。这些显然是开发者提出的相互冲突的要求：

```csharp
class Bar
{
    public new string ToString()
    {
        return "Hi there!";
    }
}
```

考虑到前面的代码，尝试预测以下内容的输出：

```csharp
Bar b = new Bar();
Console.WriteLine(b.ToString());
Console.WriteLine(b);
```

在这里，第一次调用 Console.WriteLine 涉及在静态类型为 Bar 的变量上调用 ToString。编译器会在 Bar 类型上找到一个隐藏继承成员的 ToString 方法，因此选择它。因此，第一次调用将打印“Hi there!”

然而，第二次调用使用的是接受 System.Object 作为参数的 WriteLine 重载。在 WriteLine 内部，ToString 将被调用，而编译时除了知道传入的类型是 System.Object 外没有任何其他类型信息。结果是一次虚拟调用。因为我们没有重写 ToString 而是隐藏了它，所以调用的是从 System.Object 继承的默认 ToString 方法，因此打印出 Bar 的类型名称。

如果我们通过将新创建的 Bar 实例赋给 System.Object 类型的变量来进行多态操作，情况也会有所不同：

```csharp
object o = b;
Console.WriteLine(o.ToString());
Console.WriteLine(o);
```

现在，对 ToString 的两次调用，一次是显式调用，一次是通过 Console.WriteLine 的代码，都导致虚拟调用。因为 Bar 没有重写 ToString 方法，所以两次调用都打印 Bar 的类型名称。

## How Virtual Dispatch Works

乍一看，虚拟分派可能看起来有点像魔法。编译器确实知道静态类型，但运行时类型上的虚拟方法重写仍会被考虑执行。这是如何工作的？答案在于为方法调用提供的运行时设施。存在一组不同的指令来调用方法，其中 C# 编译器使用了两种。一种是 call，另一种是 callvirt。从名称上就可以推断出第二个指令的任务（尽管 C# 编译器出于其他目的也会使用它，正如你将看到的）。

考虑到我们之前定义的 Shape 和 Circle 类，请考虑以下代码片段。注意对 Radius 的调用涉及一个非虚拟成员，而对 Area 的调用应使用虚拟分派进行。

```csharp
Circle c = new Circle(3.0);
Console.WriteLine(c.Radius);

Shape s = c;
Console.WriteLine(s.Area);
```

图 14.14 显示了与前述片段对应的 IL 代码。有几件事需要指出。首先，注意所有对静态 WriteLine 方法重载的调用都是使用 call 指令执行的。因为静态方法永远不可能虚拟（毕竟，你通过指定类型名称来调用它们），这是预期的。然而，对 Radius 和 Area 属性 getter 的两次调用都使用 callvirt。当查看 Shape 和 Circle 的代码时，你会期望只有 get_Area 调用使用 callvirt。两者都使用 callvirt 的原因是关于空值检查的行为差异：callvirt 会在发现目标是空引用时立即正确抛出 NullReferenceException。

另一方面，call 指令如果方法不访问目标上的任何实例状态，则可能不会这样做。

除了前面指出的关于 IL 读取的小注意事项外，callvirt 指令会很快判断出该方法实际上是非虚拟的，并像 call 一样工作。现在我们强调了两种不同指令的存在，我们可以仔细查看它们两者以及虚拟分派的工作原理。

首先要指出的是，从 CLR 的角度来看，虚拟分派在方法级别工作。尽管在 C# 等语言中使用 virtual 修饰符修饰其他成员类型是合法的，但它本质上是一个方法级构造。例如，对于属性而言，它是 getter/setter 方法的特性。

现在查看为我们的代码生成的代码，如图 14.14 所示。注意被调用方法是在哪些类型上定义的。对于静态 WriteLine 方法不应有任何意外。对属性 getter 的调用基于编译时关于静态类型的信息。对于 Radius，编译器知道目标类型是 00.Circle。有趣的地方在于针对虚拟方法的情况。在这种情况下，将使用声明虚拟方法的最小派生类型。对于我们的示例，目标是 00.Shape 的 get_Area 方法。但即使我们编写以下代码，也会使用这个特定方法：

```csharp
Circle c = new Circle(3.0);
Console.WriteLine(c.Area);
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_708_0.png)

图 14.14 包含虚拟和非虚拟调用的 IL 代码。

尽管我们调用 Area 的对象在静态上已知是 Circle，但仍会发出对 Shape 的 Area getter 的虚拟调用。从这一点开始，运行时负责将调用分派到它能找到的最具体的实现。
