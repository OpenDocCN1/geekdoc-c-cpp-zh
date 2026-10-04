
```csharp
public class MockDependency : IDependency
{
    private int _callMeTwiceCalled;
    private bool _callMeLastCalled;
    private bool _callMeFirstCalled;

    public int GetValue(string s)
    {
        if (s == "abc")
            return 1;
        if (s == "xyz")
            return 2;
        return 0;
    }

    public void CallMeFirst()
    {
        if (_callMeTwiceCalled > 0) || _callMeLastCalled)
            throw new AssertionException("CallMeFirst not first method called");
        _callMeFirstCalled = true;
    }

    public void CallMeTwice(string s)
    {
        if (!_callMeFirstCalled)
            throw new AssertionException("CallMeTwice called before CallMeFirst");
        if (_callMeLastCalled)
            throw new AssertionException("CallMeTwice called after CallMeLast");
        if (_callMeTwiceCalled >= 2)
            throw new AssertionException("CallMeTwice called more than twice");
        _callMeTwiceCalled++;
        return GetValue(s);
    }

    public void CallMeLast()
    {
        if (!_callMeFirstCalled)
            throw new AssertionException("CallMeLast called before CallMeFirst");
        if (_callMeTwiceCalled != 2)
            throw new AssertionException(
                string.Format("CallMeTwice not called {0} times",
                _callMeTwiceCalled));
        _callMeLastCalled = true;
    }
}
```

# 第 2 章 单元测试简介

- **依赖注入** — 模拟是使 TDD 成为一种可行的软件编写方式的关键概念。当使用模拟时，你的应用程序应该使用依赖注入。

- **面向接口编程，而非面向实现编程** — 当另一个资源作为依赖时，你的关注点不应在于它如何执行任务，而只在于接口是什么。同样，你在设计和构建类时应该使用接口来抽象功能。这种设计使你的代码更不易碎，更易于扩展。

- **尽量限制依赖** — 大多数代码都需要依赖某些东西。可能是用于存储和检索数据的数据库，用于验证用户的 Web 服务，或者是应用程序中的另一个领域。考虑到这一点，你应该限制代码所依赖的事物。大量的依赖不仅标志着一个易碎的系统，而且这种系统也更难以有效地模拟和测试。

- **不要模拟私有方法** — 当你编写测试且代码依赖于另一个类时，你应该只模拟公共方法。并且只模拟你直接使用的那些；不要过度模拟。模拟私有方法需要了解你所模拟服务的内部功能——根据封装规则，你不应该拥有这种知识。作为服务的消费者，你应该只关注公共接口上的方法；受保护和私有方法对你应该是不可见的。

`StubDependency` 具有根据不同输入参数返回不同值的逻辑。该存根能够对不同的刺激做出不同的特定响应。这提供了一种比使用空对象进行模拟更健壮的方法。

`Mock` 是框架和存根设置。`Mock` 提供了与存根相同的功能，但更为复杂。它们有定义的规则，规定了其 API 中方法的被调用顺序、方法被调用的次数，并可以根据这些信息做出反应。`Mock` 通常知道每次调用的上下文，并能够在不同情况下做出不同的反应。因此，`Mock` 需要对它们所模拟的类有一定了解。

以 `Mock` 为例，我向 `IDependency` 接口和 `DependentClass` 类中添加了几个成员：

```csharp
internal interface IDependency
{
    int GetValue(string s);
    void CallMeFirst();
    void CallMeTwice(string s);
    void CallMeLast();
}
```

```csharp
internal class DependentClass
{
    private readonly IDependency _dependency;

    public DependentClass(IDependency dependency)
    {
        _dependency = dependency;
    }

    public int GetValue(string s)
    {
        return _dependency.GetValue(s);
    }

    public void CallMeFirst()
    {
        _dependency.CallMeFirst();
    }

    public int CallMeTwice(string s)
    {
        return _dependency.CallMeTwice(s);
    }

    public void CallMeLast()
    {
        _dependency.CallMeLast();
    }
}
```

## MOQ 简览

.NET 有许多 Mock 框架。多年来，`Rhino Mocks` 一直是 .NET 的 Mock 框架，许多应用程序在测试套件中广泛使用它。除了 `Rhino Mocks` 之外，`NUnit`、`TypeMock` 和 `Easy Mock` 等 Mock 框架也变得流行。它们都是很好的框架，并提供了各种特性，使其对不同的开发者和开发团队具有不同程度的吸引力。一些开发者仍然倾向于自己编写 Mock，但随着 Mock 框架变得普及、功能完备且易于使用，这种做法变得越来越少。使用 Mock 框架绝对比自己编写 Mock 要好得多，它能让你的 TDD 体验更加高效且充实。`Moq` 迅速成为 .NET 最流行的 Mock 框架之一。它拥有坚实的功能列表，易于使用，并且拥有庞大的社区支持，这确保了 `Moq` 功能的不断改进和开发。

## Mock 框架是做什么的？

Mock 框架为你提供了创建和使用存根（`stubs`）和模拟（`mocks`）的设施。使用 Mock 框架 API，你可以在运行时创建 Mock 并注入你的测试功能。Mock 框架还提供了一个领域特定语言（`DSL`），用于为你的模拟资源定义执行规则。

## 关于 Moq

`Moq` 是一个基于 BSD 许可证发布的开源 .NET Mock 框架。`Moq` 的构建是为了利用 .NET 3.5 和 C# 3.0 中的新语言特性——特别是 `lambda` 表达式。`Moq` 放弃了许多 Mock 框架使用的记录/回放（`record/playback`）功能，而采用更具声明性的语法。`Moq` 的设计非常轻量且易于使用。`Moq` 拥有非常活跃的用户和支持社区，更新和错误修复几乎每天提交到代码库。

## Moq 基础

`Moq` 易于使用。以下示例展示了如何基于此类和接口为测试创建 Mock 和存根：

```csharp
public interface ILongRunningLibrary
{
    string RunForAlongTime(int interval);
}

public class LongRunningLibrary : ILongRunningLibrary
{
    public string RunForAlongTime(int interval)
    {
        var timeToWait = interval * 1000;
        Thread.Sleep(timeToWait);
        return string.Format("Waited {0} seconds", interval);
    }
}
```

该方法的目的是模拟一个长时间运行的过程，例如数据库查询。这个示例开始向你展示长时间运行的过程如何让测试过程变得非常缓慢，因为测试必须等待长时间运行的测试执行。在这个示例中，我用一个 Mock 代替了模拟数据库访问的长运行过程，该 Mock 无需实际访问数据库。此示例展示了不使用存根的情况下运行它：

```csharp
[TestFixture]
public class MoqExamples
{
    private ILongRunningLibrary _longRunningLibrary;

    [SetUp]
    public void SetupTest()
    {
        _longRunningLibrary = new LongRunningLibrary();
    }

    [Test]
    public void TestLongRunningLibrary()
    {
        const int interval = 30;
        var result = _longRunningLibrary.RunForLongTime(interval);
        Debug.WriteLine("Return from method {0}", result);
    }
}
```

你可以看到，这个测试简单地实例化了 `LongRunningLibrary` 并调用了 `RunForLongTime` 方法。然后测试将该方法的结果写入调试控制台。如果你在测试运行器中运行此测试，测试会在方法执行时等待，并将输出写入调试控制台，如图 2-3 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_43_0.png)

图 2-3

测试通过了，但等待 30 秒是一个很长的时间。想象一下如果你正在运行 10 个这样的测试。甚至 100 个！你还很大程度上取决于 `RunForLongTime` 方法以及 `LongRunningLibrary` 类的其余部分的实现。如果它们发生变化或存在缺陷，你可能无法获得有意义的通过或失败结果。

你必须做的第一件事是为变量 `_longRunningLibrary` 声明一个新类型。不再创建具体实例，而是让 Mock 根据 `ILongRunningLibrary` 接口创建一个模拟的实例：

```csharp
private Mock<ILongRunningLibrary> _longRunningLibrary;

[SetUp]
public void SetupForTest()
{
    _longRunningLibrary = new Mock<ILongRunningLibrary>();
}
```

由于 `_longRunningLibrary` 现在是一个 `Mock`，你必须在测试方法中以稍不同的方式处理它。要访问模拟实例上的方法，你需要使用 `Mock` 对象的 `Object` 属性：

```csharp
[Test]
public void TestLongRunningLibrary()
{
    const int interval = 30;
    var result = _longRunningLibrary.Object.RunForAll(interval);
    Debug.WriteLine("Return from method was '{0}'", result);
}
```

如果你现在运行，你将得到预期的结果，如图 2-4 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_44_0.png)

图 2-4

测试失败是因为提供了一个 `LongRunningLibrary` 的模拟实例，但没有为模拟方法提供实现。这很容易修正：

```csharp
_longRunningLibrary
    .Setup(l1rl => l1rl.RunForAllTime(30))
    .Returns("This method has been mocked!");
```

在这个示例中，你是在告诉 `Mock` 在参数为 30 的 `LongRunningLibrary` 模拟实例上调用 `RunForAllTime` 方法，你只是想要返回字符串 "This method has been mocked!"。如果你现在运行测试运行器，测试通过了，如图 2-3 所示。

> Passed: 1 Failed: 0 Errors: 0 Inclusive: 0 Ignored: 0 Skipped: 0 Time: 0.543011
>
> **** Unit.MoqExamples.TestLongRunningLibrary
>
> Return from method was "This method has been mocked!"
