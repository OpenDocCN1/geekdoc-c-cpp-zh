
该类的主要问题（除了无限循环之外）是，它每次都返回自己作为 `IEnumerator` 实现。枚举器预计应该对集合中的位置有一个概念，即在调用 `Current` 时返回的值。假设同时有多个迭代过程在运行，它必须能够区分这些过程当前所处的位置。你不需要为此考虑多线程；只需启动一次迭代并运行一会儿，然后启动另一个，依此类推 —— 只要实现在需要第二次迭代时能阻止前一个迭代即可。

以下 `EndlessList` 类的实现使用了单独的类来处理 `IEnumerator` 和 `IEnumerable`。这些类是嵌套的，虽然它们并不这样做。但实际上，将枚举器实现嵌套在可枚举器内部是一种常见模式。为了让它更实际一些，此实现使用了整数值而不是一直返回字符串。

与大多数真实世界的实现相比，仍然存在一个主要区别：在外层列表实现中没有封装数据。你可能会奇怪为什么这个示例没有以更灵活的方式构建。答案是，这意味着需要编写一些相当复杂的数据结构代码，或者使用数据结构，这会使示例变得不实际，因为所有标准数据结构已经有了自己的 `IEnumerable` 实现。

```csharp
public class EndlessList : IEnumerable {
    public class Enumerator : IEnumerator {
        int val = -1;
        public object Current {
            get { return val; }
        }
        public bool MoveNext() {
            val++;
            return true;
        }
        public void Reset() {
            val = -1;
        }
        public IEnumerator GetEnumerator() {
            return new Enumerator();
        }
    }
}
```

这种实现值序列的模式非常灵活且强大。在某些情况下，它的实现可能非常困难——例如，如果列表中的数据并不易于进行顺序和/或随机访问。但最重要的是，创建此类实现并不快速快捷。某些算法问题有基于序列的简单解决方案，或者基于显式接口实现的解决方案，而 .NET 迭代器并不擅长创建此类临时的迭代器来解决此类问题。

### 实现迭代器函数

C# 的迭代器特性在 C# 2.0 版本中引入，允许你创建 `IEnumerable`/`Enumerator` 组合的实现，而无需手动实现其中任何一个接口。它更进一步，除了支持非泛型接口外还支持泛型接口，使得实现 `Enumerator` 成为可能。

通常，只需要实现具有特定返回类型的函数即可使用此功能。编译器在应用其转换时查找的第二个标准是函数内部使用了至少一个特殊关键字之一。最常见的是 `yield return` 语句。例如，`EndlessList` 示例可以这样实现为 C# 迭代器：

```csharp
public static IEnumerable<int> EndlessListFunction() {
    int val = 0;
    while (true)
        yield return val++;
}
```

要理解如何处理它，最简单的方法是字面理解它。函数的返回类型是 `IEnumerable<int>`，因此你在可能使用实现此接口的类的地方使用它。这里是遍历 `EndlessListFunction` 的代码：

```csharp
var list = EndlessListFunction();
foreach (var item in list)
    Console.WriteLine(item);
```

C# 编译器自动创建一个实现 `IEnumerable<int>` 接口的类。该类的逻辑和相应的 `Enumerator` 经过精心结构，以返回由函数实现中的逻辑所生成的值序列。

这是一个简单的迭代器：

```csharp
public static IEnumerable<int> ThreeNumbers() {
    yield return 3;
    yield return 11;
    yield return 27;
}
```

编译器使用 `yield return` 语句生成的 `ThreeNumbers` 类如下：

```csharp
class ThreeNumbers : IEnumerable<int> {
    int state;
    int current;
    public Enumerator(int state) {
        state = state;
    }
    bool MoveNext() {
        switch (state++) {
            case 0:
                current = 3;
                return true;
            case 1:
                current = 11;
                return true;
            case 2:
                current = 27;
                return true;
            default:
                return false;
        }
    }
    IEnumerator GetEnumerator() {
        throw
    }
    IEnumerator<int> GetEnumerator() {
        return new Enumerator(0);
    }
    public int Current {
        get {
            return current;
        }
    }
}
```

迭代器函数的主体，它从上次停止的地方继续。再次，当消费者停止检索值时，不会产生任何开销。该模式仅在需要时执行大量工作。

下面的代码段展示了一个从 Web 服务检索数据的迭代器的实用示例。数据是从 Web 服务中懒性加载的，因为它是自动分页的。迭代器会检索新页面，并向调用者返回一个长度未知的字符串序列。调用者可以按任何喜欢的方式处理它——在本例中，通过链式调用 `Take`：

```csharp
private static void TwitterSearchIterator() {
    foreach (var tweet in GetTweets("#msdn").Take(10))
        Console.WriteLine(tweet);
}
```

```csharp
private static IEnumerator<string> GetTweets(string searchString) {
    var url = "http://twitter.com/search/search.atom?q=";
    int page = 1;
    var escapedSearchString = searchString.Replace("*", "%40").Replace("#", "%23");
    XmlNamespace ns = "http://www.w3.org/2005/Atom";
    while (true) {
        var doc = XDocument.Load(String.Format(
            "{0}(1)&page={2}", url, escapedSearchString, page));
        var entries = doc.Root.Elements(ns + "entry");
        if (entries.Count() == 0)
            yield break;
        foreach (var entry in entries)
            yield entry.Element(ns + "author").Element(ns + "name").Value + ": " +
                WebUtility.HtmlDecode(entry.Element(ns + "title").Value);
    }
}
```

### 使用 .NET 枚举项

这实际上是 `IEnumerable` 和 `IEnumerator` 声明的迭代模式的最简单实现：

```csharp
public class EndlessListWithoutInterfaces {
    public EndlessListWithoutInterfaces GetEnumerator() { 
        return this;
    }
    public bool MoveNext() { 
        return true;
    }
    public object Current {
        get { return "something"; }
    }
}
```

在 `EndlessListWithoutInterfaces` 类上可以使用 C# 的 `foreach` 结构：

```csharp
var list = new EndlessListWithoutInterfaces();
foreach (var item in list) {
    Console.WriteLine(item);
}
```

该实现非常基础，因此会导致无限循环。需要指出的是，尽管 `IEnumerable` 和 `IEnumerator` 接口没有被“官方”实现，但 `foreach` 很好地完成了它的工作。它完全缺少 `Reset` 方法。可以说，`foreach` 的这种“宽容”行为并不是一件理想的事，但自 .NET 和 C# 1.0 以来一直如此。建议你不要依赖这种行为，仅仅因为其他 .NET 语言并不一定以与 C 相同的方式实现它。

一个完整的列表实现看起来如下：

```csharp
public class EndlessListWithInterfaces: IEnumerable, IEnumerator {
    public EndlessListWithInterfaces() { }
    public IEnumerator GetEnumerator() { 
        return this;
    }
    public object Current {
        get { return "something"; }
    }
    public bool MoveNext() { 
        return true;
    }
    public void Reset() { }
}
```
