
```csharp
public interface IStrategy
{
    void Execute();
}
//...
public class ConcreteStrategyA : IStrategy
{
    public void Execute()
    {
        Console.WriteLine("ConcreteStrategyA.Execute()");
    }
}
//...
public class ConcreteStrategyB : IStrategy
{
    public void Execute()
    {
        Console.WriteLine("ConcreteStrategyB.Execute()");
    }
}
//...
public class Context
{
    public Context()
    {
        currentStrategy = strategyA;
    }

    public void DoSomething()
    {
        currentStrategy.Execute();

        // swap strategy with each call
        currentStrategy = (currentStrategy == strategyA) ? strategyB : strategyA;
    }

    private readonly IStrategy strategyA = new ConcreteStrategyA();
    private readonly IStrategy strategyB = new ConcreteStrategyB();

    private IStrategy currentStrategy;
}
```

每次调用 `Context.DoSomething()` 时，该方法首先委托给当前策略，然后在策略 A 和策略 B 之间切换。 下一次调用将在再次切换回原始策略之前委托给新选择的策略。

策略的选择方式是一个实现细节——它不会改变模式的净效果：类的行为隐藏在接口之后，该接口的实现用于执行实际工作。

## 更进一步的灵活性

接口的实用性不仅限于设计模式。 接口还有一些其他更专业的用途值得研究。 虽然这些特性通常不适用，但在某些情况下它们是完成工作的正确工具。

与设计模式一样，过度使用会损害代码的可读性和可维护性。 找到解决问题的优雅方案所需的协作模式和技术的正确数量是一项艰难的平衡，因此在使用接口进行以下方式时请谨慎行事。

### 鸭子类型

C# 是一种静态类型语言，而鸭子类型更常见于动态类型语言。 鸭子类型使用鸭子测试：

> 当我看到一只鸟走路像鸭子、游泳像鸭子、叫声像鸭子时，我称那只鸟为鸭子。

> —James Whitcomb Riley

应用于编程语言中的类型，鸭子测试表明，只要一个对象表现出某个接口的 *行为*，就应将其视为该接口。不幸的是，在 C# 中默认情况下并非如此。 请观察列表 3-21 中的示例。

**列表 3-21** 尽管对象 `Swan` 实现了 `IDuck` 的所有方法，但它实际上 *不是* `IDuck`。

Click here to view code image

```csharp
public interface IDuck
{
    void Walk();

    void Swim();

    void Quack();
}
//...
public class Swan
{
    public void Walk()
    {
        Console.WriteLine("The swan is walking.");
    }

    public void Swim()
    {
        Console.WriteLine("The swan can swim like a duck.");
    }

    public void Quack()
    {
        Console.WriteLine("The swan is quacking.");
    }
}
//...
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();

        var swanAsDuck = swan as IDuck;

        if(swan is IDuck || swanAsDuck != null)
        {
            swanAsDuck.Walk();
            swanAsDuck.Swim();
            swanAsDuck.Quack();
        }
    }
}
```

`is` 断言和 `as` 转换分别返回 false 和 null。 公共语言运行时 `CLR` 不认为 `Swan` 是 `IDuck`，即使它实际上满足该接口。 类型必须通过接口继承 *实现* 接口。

你可以使用一些技巧使 `Swan` 类可以在 *不* 实现它的情况下作为 `IDuck` 接口的实例使用。 你可以利用 CLR 新版本中的动态类型扩展，或者使用一个名为 `Impromptu Interface` 的第三方库。

### 使用动态语言运行时

从版本 4 开始，`.NET Framework` 不再严格是静态类型的。 随着 `dynamic` 关键字的引入以及一些支持类型，你可以避免 CLR 的静态类型并切换到动态语言运行时 `DLR` 的动态类型。 C# 中动态类型的示例显示在列表 3-22 中。

**列表 3-22** `DLR` 可用于鸭子类型。

Click here to view code image

```csharp
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();

        DoDuckLikeThings(swan);

        Console.ReadKey();
    }

    static void DoDuckLikeThings(dynamic duckish)
    {
        if(duckish != null)
        {
            duckish.Walk();
            duckish.Swim();
            duckish.Quack();
        }
    }
}
```

请注意，`method` 参数的类型为 `dynamic`。不仅需要针对 `.NET Framework 4`，还需要在客户端中专门设计动态类型。在这两方面，有时是不可行的。例如，你不能简单地在所有地方都创建接受 `dynamic` 参数的方法，否则你最好使用动态类型的 `.NET Framework` 语言，例如 `IronPython`³。

> ³ http://ironpython.net/

### 使用 Impromptu Interface

`Impromptu Interface` 是一个可通过 `NuGet` 安装的 `.NET Framework` 库。安装后，你可以使用 `ActLike<T>()` 方法传入你的 `Swan` 并接收一个委托给你的实例的 `IDuck` 实例。清单 3-23 展示了其工作原理。

#### LISTING 3-23 Impromptu Interface allows duck-typing in C#.

Click here to view code image

```csharp
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();

        var swanAsDuck = Impromptu.ActLike<IDuck>(swan);

        if(swanAsDuck != null)
        {
            swanAsDuck.Walk();
            swanAsDuck.Swim();
            swanAsDuck.Quack();
        }

        Console.ReadKey();
    }
}
```

`ActLike` 方法所做的是通过使用 `Reflection Emit` 在运行时创建一个新类型。这是 `.NET Framework Reflection API` 的一个强大部分，允许在运行时创建新类型。此新类型实现了 `IDuck` 接口，但它也将 `Swan` 实例作为封装字段包含在内。每当调用其中一个 `IDuck` 接口方法时，新类型会简单地委托给 `Swan` 实例。它本质上是适配器模式的运行时版本。`Impromptu Interface` 是自动应用对象适配器模式的一种方式。

### CLR duck-typing support

有趣的是，`CLR` 已经支持 duck-typing。不幸的是，这仅适用于一种不常见的情況：实现可枚举对象。`foreach` 循环的目标类型必须符合某个接口，但该接口并未形式化，可以在目标类上临时实现。在清单 3-24 的示例中，`Duck` 类是 `foreach` 循环的目标。

#### LISTING 3-24 The CLR implicitly supports duck-typing for enumerable types.

Click here to view code image

```csharp
class Program
{
    static void Main(string[] args)
    {
        var duck = new Duck();

        foreach (var duckling in duck)
        {
            Console.WriteLine("Quack {0}", duckling);
        }

        Console.ReadKey();
    }
}
```

`Duck` 并未实现任何接口，但 `foreach` 循环要求 `GetEnumerator()` 方法，如编译器所指示的那样，如图 3-8 所示。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_137_0.png)

#### FIGURE 3-8 Without requiring a specific interface, the compiler complains that a public method is missing from the class.

当你使用 `void` 返回类型实现此方法时，你会收到一个新错误，指出此类型不支持其他必需的方法和属性，如图 3-9 所示。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_137_1.png)

#### FIGURE 3-9 The return type of the GetEnumerator method must also match an implicit contract.

这些属性随后可以按清单 3-25 所示实现。

#### LISTING 3-25 Completing the implied interface of the DuckEnumerator class.

Click here to view code image

```csharp
public class DuckEnumerator
{
    int i = 0;

    public bool MoveNext()
    {
        return i++ < 10;
    }

    public int Current
    {
        get
        {
            return i;
        }
    }
}
```

此时，你已成功实现了 `foreach` 所需的隐式接口——duck-typing 发挥作用！

### Mixins

duck-typing 的扩展概念是 `mixin`。`mixin` 是一个包含多个其他类的实现而无需使用实现继承的类。正如你已经学到的，C# 不支持多重实现继承，因此你必须寻找其他实现 `mixin` 的解决方案。

一种简单但有限的实现 `mixin` 的方法是使用扩展方法。这允许你向已定义的类型的添加方法，这可能非常有用。另一种选择是使用 `Re-motion Re-mix` 等第三方库，它的工作方式与 `Impromptu Interface` 类似，即在运行时生成一个新类型，该类型包含你指定的所有接口并充当多面适配器。

### 使用扩展方法

自 `.NET Framework 3.5` 以来，扩展方法允许向已存在的类型添加新功能。无需访问类型的源代码，也无需类型为部分定义，你就可以扩展一个类型。清单 3-26 显示了本节将增强的接口，以及一对简单的扩展方法。

#### LISTING 3-26 Extension methods can enhance an existing interface.

Click here to view code image

```csharp
public interface ITargetInterface
{
    void DoSomething();
}
//...
public static class MixinExtensions
{
    public static void FirstExtensionMethod(this ITargetInterface target)
    {
        Console.WriteLine("The first extension method was called.");
    }

    public static void SecondExtensionMethod(this ITargetInterface target)
    {
        Console.WriteLine("The second extension method was called.");
    }
}
```

现在，只要客户端可以访问 `ITargetInterface` 实例，并且它还引用了 `MixinExtensions` 类，这两个扩展方法就会可用。可以创建任意数量的扩展方法，分散在多个静态类中。清单 3-27 显示了另一对扩展方法；这次它们接受额外参数。

#### LISTING 3-27 Extension methods can take parameters.

Click here to view code image

```csharp
public static class MoreMixinExtensions
{
    public static void FurtherExtensionMethodA(this ITargetInterface target, int extraParameter)
    {
        Console.WriteLine("Further extension method A was called with argument {0}", extraParameter);
    }

    public static void FurtherExtensionMethodB(this ITargetInterface target, string stringParameter)
    {
        Console.WriteLine("Further extension method B was called with argument {0}", stringParameter);
    }
}
```

这些扩展方法可以像任何其他方法一样被任何客户端调用，如清单 3-28 所示。

#### LISTING 3-28 Clients have access to extension methods as if they were declared directly on the target interface.

Click here to view code image

```csharp
public class MixinClient
{
    public MixinClient(ITargetInterface target)
    {
        this.target = target;
    }

    public void Run()
    {
        target.DoSomething();
        target.FirstExtensionMethod();
        target.SecondExtensionMethod();
        target.FurtherExtensionMethodA(30);
        target.FurtherExtensionMethodB("Hello!");
    }

    private readonly ITargetInterface target;
}
```

这种 `mixin` 方法有几个值得注意的限制。首先是客户端的可测试性。正如第 4 章“单元测试和重构”将展示的那样，静态类不利于轻松模拟。这使得这些扩展方法的所有客户端更难以进行适当的单元测试。

更糟糕的是，由于扩展方法为静态类，它们无法保存与对象相关的任何额外每个实例状态。当然，有变通方法，例如存储一个将实例映射到某些额外值的静态字典，但这并不理想。

还请注意，所有扩展方法都针对同一个接口，并且所有要增强的实例都必须实现此接口。真正的 `mixin` 另一方面，实现多个不同的接口并充当聚合适配器。

### 使用 Re-motion Re-mix
