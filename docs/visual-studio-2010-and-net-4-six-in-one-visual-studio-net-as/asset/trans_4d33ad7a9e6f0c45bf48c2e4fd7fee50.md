

```cs
public dynamic MyOperation(int a, dynamic arg)
{
    return a + arg;
}
```

你可以将它们作为成员类型，也可以作为构造函数参数，如下所示：

```
class MyClass
{
    dynamic _Arg;

    public MyClass(dynamic arg)
    {
        _Arg = arg;
    }
}
```

与 C# 4.0 相比，.NET Framework 的通用语言运行时 (CLR) 并没有为 `dynamic` 设置一个独立的内置类型。相反，编译器在任何地方使用 `System.Object`，并在内部将变量标记为 `dynamic` 以在编译期间使用这些信息。这种实现带来了一些后果：

- 使用 `System.Object`，从每个类型（指针类型外）到 `dynamic` 有隐式转换，以及从 `dynamic` 到每种此类类型的显式转换。

- 如果方法的签名仅区别于 `dynamic` 与 `System.Object`，则它们被认为是相同的。

- `typeof(dynamic)` 表达式为 `true`。

尽管 `System.Object` 和 `dynamic` 被视为相同的，但如果两者都是某个表达式的候选类型，类型推断算法会优先选择 `System.Object`。

## 动态语言运行时

动态查找底层实现中的一个重要组件是动态语言运行时 (DLR)，它是 .NET Framework 4.0 的一部分。DLR 是一个运行时环境，为动态语言向通用语言运行时 (CLR) 添加了一组服务，这使得开发在 .NET Framework 上运行的动态语言变得更加容易，同时也便于为静态类型语言添加动态特性。DLR 构建在 CLR 之上，并使用运行时绑定器通过动态表达式访问物理对象模型。

DLR 不仅为 C# 动态查找提供了大部分基础设施，还为 .NET 上的多种动态编程语言提供了实现（如 IronPython 和 IronRuby）。DLR 提供了一种卓越的缓存机制（命名为调用点缓存 Call Site Caching），它极大地提高了运行时分派的效率。对于 C# 动态查找的用户来说，DLR 是不可见的。

虽然说 C# 是最接近 CLR 的 .NET 编程语言，但在使用时存在一些局限：

- DLR 允许从代表类的对象创建对象。然而，C# 的当前实现还没有支持此点的语法。

- Lambda 表达式根据本质是类型推断的，因此编译器使用上下文来推断它们的含义。如果 Lambda 表达式作为动态方法调用的参数出现，编译器无法决定该 Lambda 表达式应转换为什么类型。因此，不允许 Lambda 动态动态方法的参数出现。

- 动态查找将无法找到方法。动态查找发生在运行时，而扩展方法是编译时产物。扩展方法是否生效（如果存在多个扩展方法，则使用哪一个）取决于调用的静态上下文（即源文件中出现了哪些 `using` 子句）。这些上下文信息不会保留在编译后的二进制文件中，DLR 将无法找到扩展方法。

## 命名参数和可选参数

早些，列表 24-1 显示了在某些冗余且难以阅读的方法调用方面的一些“代码表头”，如下所示：

```
chart.ChartWizard(
range.CurrentRegion, // --- Source
Type.Missing, // --- Gallery
Type.Missing, // --- Format
Type.Missing, // --- PlotBy
Type.Missing, // --- CategoryLabels
Type.Missing, // --- SeriesLabels
Type.Missing, // + +"Memory Usage in *" + Environment.MachineName, // --- Title
Type.Missing, // --- CategoryTitle
Type.Missing, // --- ValueTitle
Type.Missing); // --- ObjectTitle
```

末尾注释帮助你猜测传递给 `ChartWizard` 调参数的作用，但如果没有它们，你几乎无法破解 `Type.Missing` 参数代表什么。

某些 API（最尤其是 Microsoft Office 和 Visual Studio 自动化 API 等 COM 接口）是专门针对命名参数和可选参数编写的。直到现在，在 C# 中调用这些 API 一直非常痛苦，有时必须显式传递多达 30 个参数，其中大多数参数都有合理的默认值且可以省略。随着 C# 4.0 引入了可选参数，之前的代码看起来完全符合它应该有的：

```
chart.ChartWizard(
    Source: range.CurrentRegion, // + Environment.MachineName
    Title: "Memory Usage in *" + Environment.MachineName);
```

命名参数和可选参数确实是两个不同的特性，但通常经常一起使用。可选参数允许你省略成员调用的参数，而命名参数提供了一种利用相应参数名称的方法，而不是依赖于它在参数列表中的位置。

当你比较列表 24-1 和列表 24-2 中调用 `ChartWizard` 的两个代码段时，你可以看到这些新特性的组合是多么强大。代码不仅变得简洁，而且开发者的意图从方法调用中变得一目了然。

## 使用可选参数

不要认为 COM 自动化对象模型是这两个语言特性的唯一候选者！即使在 .NET 的 API 中，你有时也会发现被迫为一个方法编写许多具有不同参数组合的重载，以便为调用者提供最大的可用性。在这些情况下，可选参数是一个非常有用的替代方案。

```cs
public class MyClass{
    public void DoTheWork(int taskId, string taskType, int timeout,
        bool useMultipleCores)
    {
        // ...
    }

    public void DoTheWork(int taskId, string taskType, int timeout)
    {
        DoTheWork(taskId, taskType, timeout, false);
    }

    public void DoTheWork(int taskId, string taskType)
    {
        DoTheWork(taskId, taskType, 10000);
    }

    public void DoTheWork(int taskId)
    {
        DoTheWork(taskId, "Cleanup");
    }
}
```

这里有一个示例帮助你理解：

与其为 `DoTheWork` 编写四个重载，你可以创建一个带有可选参数的方法。通过为参数提供默认值，可以将该参数声明为可选的：

```cs
public void DoTheWork(int taskId,
    string taskType = "Cleanup",
    int timeout = 10000,
    bool useMultipleCores = false)
{
    // ...
}
```

在这里，`taskType`、`timeout` 和 `useMultipleCores` 参数都是可选的，可以在方法调用中省略：

```cs
DoTheWork(123, "Processing", 4000, true);
DoTheWork(124, "Removing files", 6000);
DoTheWork(125, "Adding ID");
DoTheWork(126);
```

## 可选参数规则

C# 4.0 不允许在逗号之间省略参数，因此你不能写这样的代码：

```cs
DoTheWork(123, , ,);
```

语言设计者认为这会导致难以阅读的逗号计数代码——他们是正确的。与其写逗号，不如使用命名参数。

使用必需和可选参数有一些规则：

- 带有 `ref` 或 `out` 修饰符的参数不能有默认值。

- 参数（没有默认值表达式）不能出现在可选参数之后。

- 可选参数的默认值必须是常量表达式，或者 `new` 或 `default` 运算符的操作的是值类型。这些可以在编译期间解析，而其他表达式不能。

## 可选参数和索引器

访问器实际上是方法，因此你可以在索引器的 getter 和 setter 方法中使用可选参数。例如，你可以定义这样一个实现稀疏矩阵的类：

```cs
public class SparseMatrix<T>
{
    public struct SparseIndex
    {
        public int Row;
        public int Column;
    }
    Dictionary<SparseIndex, T> _Storage = new Dictionary<SparseIndex,T>();
    public T this[int row = 0, int column = 0]
    {
        get
        {
            T result;
            return _Storage.TryGetValue(new SparseIndex { Row = row, Column = column });
        }
    }
}
```

