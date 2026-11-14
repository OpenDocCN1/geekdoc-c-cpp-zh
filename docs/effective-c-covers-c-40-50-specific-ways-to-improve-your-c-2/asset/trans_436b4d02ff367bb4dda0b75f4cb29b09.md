

泛型接口，使其可以被当作协变或逆变来处理。先讨论泛型协变，然后再讨论逆变。

This method can be called with a List<Planet>:

```
public static void CovariantGeneric(
    IEnumerable<CelestialBody> baseItems)
{
    foreach (var thing in baseItems)
        Console.WriteLine("{0} has a mass of {1} Kg",
            thing.Name, thing.Mass);
}
```

这是因为 IEnumerable<T> 已经被增强，将 T 限制在其接口中仅出现在输出位置：

```
public interface IEnumerable<out T> : IEnumerable
{
    IEnumerator<T> GetEnumerator();
}
```

```
public interface IEnumerator<out T> :
    IDisposable, IEnumerator
{
    T Current { get; }
    // MoveNext(), Reset() inherited from IEnumerator
}
```

我在此同时包含了 IEnumerable<T> 和 IEnumerator<T> 的定义，因为 IEnumerable<T> 有重要的限制。请注意，IEnumerable<T> 现在使用 out 修饰符修饰类型参数 T。这迫使编译器将 T 限制在输出位置。输出位置仅限于函数返回值、属性 get 访问器以及某些委托位置。

因此，使用 IEnumerable<out T>，编译器知道你会查看序列中的每个 T，但永远不会修改源序列的内容。在这种情况下，将每个 Planet 视为 CelestialBody 是可行的。

IEnumerable<T> 能够协变，仅仅是因为 IEnumerator<T> 也是协变的。如果 IEnumerable<T> 返回一个未声明为协变的接口，编译器会生成错误。协变类型必须返回类型参数本身，或返回基于该类型参数且也是协变的接口。

但是，使用泛型时，替换列表中第一个项目的方法将是不变的：

```csharp
public static void InvariantGeneric(
    IList<CelestialBody> baseItems)
{
    baseItems[0] = new Asteroid
    { Name = "Hygiea", Mass = 8.85e19 };
}
```

因为 IList<T> 的 T 既没有装饰 in 修饰符也没有装饰 out 修饰符，你必须使用精确的类型匹配。

当然，你也可以创建逆变的泛型接口和委托。将 in 修饰符替换为 out 修饰符。这指示编译器，类型参数只能出现在输入位置。.NET Framework 已将 in 修饰符添加到 IComparable<T> 接口：

```csharp
public interface IComparable<in T>
{
    int CompareTo(T other);
}
```

这意味着你可以让 CelestialBody 实现 IComparable<T>，使用对象的质量。它可以比较两个 Planet、一个 Planet 和一个 Moon、一个 Moon 和一个 Asteroid，或任何其他组合。通过比较对象的质量，这是一个有效的比较。

你会注意到 IEquatable<T> 是不变的。按定义，一个 Planet 不能等于一个 Moon。它们是不同的类型，所以这样做没有意义。如果两个对象相等，它们必须是相同的类型（这是必要条件，但不是充分条件，参见第 6 项）。

逆变的类型参数只能出现作为方法参数，以及委托参数中的某些位置。

到现在，你可能已经注意到我两次使用了“委托参数中的某些位置”这个短语。委托定义也可以是协变或逆变的。通常很简单：方法参数是逆变的（in），方法返回类型是协变的（out）。BCL 更新了许多委托定义以包含变性：

```
public delegate TResult Func<out TResult>();
public delegate TResult Func<in T, out TResult>(T arg);
public delegate TResult Func<in T1, T2, out TResult>(T1 arg1,
    T2 arg2);
public delegate void Action<in T>(T arg);
public delegate void Action<in T1, in T2>(T1 arg1, T2 arg2);
public delegate void Action<in T1, in T2, T3>(T1 arg1,
    T2 arg2, T3 arg3);
```

再次，这可能不算太难。但是，当你混合使用它们时，事情就开始变得令人困惑了。你已经看到，不能从协变接口返回不变接口。你也不能使用委托来绕过协变和逆变限制。

如果不小心，委托倾向于“翻转”接口中的协变和逆变。这里有几个例子：

```
public interface ICovariantDelegates<out T>
{
    T GetAnItem();
    Func<T> GetAnItemLater();
    void GiveAnItemLater(Action<T> whatToDo);
}
```

```
public interface IContravariantDelegates<in T>
{
    void ActOnAnItem(T item);
    void GetAnItemLater(Func<T> item);
    Action<T> ActOnAnItemLater();
}
```

我特意命名了这些接口中的方法，以展示它为什么这样工作。仔细查看 ICovariantDelegates 接口定义。GetAnItemLater() 只是一种延迟检索项目的方式。调用者可以稍后调用该方法返回的 Func<T> 来检索值。T 仍然存在于输出位置。这可能仍然说得通。GetAnItemLater() 方法可能有点令人困惑。在这里，你的方法接受一个委托，该委托在每次调用时都会接受一个 T 对象。因此，尽管 Action<in T> 是协变的，但它在 ICovariantDelegates 接口中的位置意味着它实际上是从实现 ICovariantDelegates<T> 的对象返回 T 对象的一种方式。它看起来应该是逆变的，但相对于接口来说它是协变的。

IContravariantDelegates<T> 类似，但展示了如何在逆变接口中使用委托。同样，ActOnAnItem 方法应该很明显。ActOnAnItemLater() 方法稍微复杂一点。你返回一个方法，该方法将在稍后接受一个 T 对象。最后那个方法，再次，可能会造成一些混淆。它与另一个接口的概念相同。GetAnItemLater() 方法接受一个将在稍后返回 T 对象的方法。尽管 Func<out T> 被声明为协变，但它的用途是将输入带到实现 IContravariantDelegates 的对象。它相对于 IContravariantDelegates 是逆变的。

描述协变和逆变究竟如何工作当然可能会变得复杂。幸运的是，现在语言支持使用 `in`（逆变）和 `out`（协变）修饰符来装饰泛型接口和委托。你应该尽可能为定义的任何接口和委托添加 `in` 或 `out` 修饰符。然后，编译器可以纠正你定义的变性可能被滥用的情况。编译器会在你的接口和委托定义中捕获它，并检测你创建的类型的任何滥用。

此页故意留空

## 4 | 使用框架

我的朋友兼同事 Martin Shoemaker 在 .NET 于 2002 年首次发布后不久，创建了一个名为“Do I Have to Write That .NET Code？”的圆桌会议。当时这是一个很棒的圆桌会议，而现在它更加相关。.NET Framework 已经发展壮大，现在包含的新类和新功能比当时多得多。重要的是，你不要创建已经存在的功能。

.NET Framework 是一个丰富的类库。你对框架了解得越多，就需要自己编写的代码就越少。框架库将为你完成更多工作。遗憾的是，基类库现在必须应对与版本 4 相关的问题。比版本 1 存在时更好的解决问题的方法已经出现。但框架团队不能简单地删除那些旧的 API 和类。将那些旧 API 标记为弃用可能也没有意义。它们仍然可以工作，重写可用的代码并不符合你的最佳利益。但是，在编写新代码时，你应该使用当前存在的最佳工具。本章展示了如何在当前版本 4.0 中充分利用 .NET Framework 的技术。其他条目帮助你在框架中有多种选择时选择最佳选项。还有其他条目解释了一些技术，如果你希望你的类与框架设计者创建的类协同工作，你应该使用这些技术。

### 第 30 条：优先使用重写而非事件处理程序

许多 .NET 类提供两种不同的方式来处理系统事件。你可以附加一个事件处理程序，也可以重写基类中的虚函数。为什么要提供两种做同一件事的方式？因为不同的情况需要不同的方法。在派生类中，你应该始终重写虚函数。将事件处理程序的使用限制在响应不相关对象中的事件。

