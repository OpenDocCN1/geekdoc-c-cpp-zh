
这要视具体情况而定。在大多数情况下，我会将此类异常的出现视为我代码中的 bug。

请注意，当你输入成员名称时，IntelliSense 中会立即显示已记录的异常列表。图 23.20 展示了 File.OpenRead 方法的这种情况。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1235_0.png)

图 23.20 File.OpenRead 的已记录异常。

ArgumentException 最常用的构造函数重载如下：

```csharp
public ArgumentException(string message, string paramName);
```

对于第二个参数，请指定收到无效值的参数名称。该数据可以通过 ParamName 属性再次检索。

## ArgumentNullException

ArgumentNullException 是 ArgumentException 那个更专门的“小兄弟”，用于表示参数收到了意外的 null 引用。同样，它指出了代码中缺少 null 检查，应严肃对待。请问问自己，这个 null 引用最初是如何到达代码中的那个位置的。

尽可能在接近根源的地方消灭这个邪恶的 null 引用（例如，在你正在开发的组件的入口处）。而实现这一目标的方法正是抛出这个异常。常用于此目的的构造函数包括：

```csharp
public ArgumentNullException(string paramName);
public ArgumentNullException(string paramName, string message);
```

第一个构造函数通常就足够了，因为 null 参数的含义除了其参数名之外，不需要太多解释。

### API 耻辱堂与 FxCop

如果你选择使用第二个重载，请注意 .NET 早期框架设计者所犯的一个小错误：这里的 paramName 和 message 参数与 ArgumentException 上的顺序相反。作为权宜之计，引入了 FxCop 规则“Microsoft.Usage CA2208”，用于检测这些异常类型构造函数上参数颠倒的情况。它的检测方法是，将传递给 paramName 参数的字符串与该方法存在的所有参数名进行比对。

### 扩展方法

有时会出现的一个问题是：当扩展方法的 this 参数收到 null 引用时，应该使用哪种异常类型。在调用处，这看起来像一次实例方法调用，因此 NullReferenceException 可能是最自然预期的东西：

```csharp
var res = source.Where(n => n > 0); // LINQ's Where operator
```

然而，NullReferenceException 确实应该保留给运行时检测到的真实取消引用 null 引用的尝试。当扩展方法被写成普通静态方法调用时，这一点尤其明显：

```csharp
var res = Enumerable.Where(source, n => n > 0);
```

在这里，你根本不会期望出现 NullReferenceException。

## ArgumentOutOfRangeException

与针对数组的 IndexOutOfRangeException 类似，这种异常类型用于表示提供的参数超出了某个范围。同样，它通常表明调用方的输入验证不够严谨，而这种问题通常是可以避免的。

使用这种异常类型的示例包括 System.Collections 及其子命名空间中的各种集合数据类型：

```csharp
var lst = new List<int> { 1, 2, 3 };
int thereIsNoThirdElement = lst[3];
```

在你自己的 API 中使用这种异常类型很简单，只需使用与 ArgumentException 类似的构造函数（paramName 放在第一位）。提醒一下，参数和索引是两个不同的概念。使用这种异常类型并不意味着必须使用特定的成员类型（如索引器）或特定的数据类型（如数值）。一个方法同样可以抛出这种类型的异常，以表示其字符串参数超出了可接受值的范围。

## InvalidOperationException

当对一个不具备有效状态的对象执行操作时，就会引发这种异常。有时这是因为没有遵循某种“协议”，这种协议可能非正式地记录在该类型的文档中。例如，一个对象可能需要在调用任何其他成员之前先进行某种 Initialize 调用。一个具体的例子是 System.Data.SqlClient 中的 SqlConnection 类：

```csharp
using (SqlConnection conn = new SqlConnection(connString)) {
    Console.WriteLine(conn.ServerVersion);
}
```

在这里，ServerVersion 属性 getter 会抛出上述讨论的异常，因为尚未通过调用 conn.Open() 打开连接。

这种异常也常在遍历集合的同时修改集合时抛出。这会使正在使用的枚举器对象失效，因为底层集合可能发生各种变化。尽管你可能会认为所有集合更改操作都可以在枚举器内部得到处理，但还是会出现不少有趣的情况。例如，MoveNext 可能已经表示后面还有一个元素，但紧接着发生的更改可能会移除该元素。这将破坏“MoveNext 调用返回 true 确保后续对 Current 方法的调用会成功”的约定。基于这些原因，在集合被修改后，枚举器的任何进一步使用都是被禁止的：

```csharp
var lst = new List<int> { 1, 2, 3 };
foreach (var n in lst)
    lst.Add(n);
```

## NotImplementedException

顾名思义，只要某个方法或成员尚未实现，就会产生这种异常。这可能表示你正在处理一个尚未实现的功能的存根（stub）。Visual Studio 代码编辑器的“实现接口”功能会为其生成的方法存根使用这种异常类型，如图 23.21 所示。

```csharp
class MyCollection<T> : IEnumerable<T>
{
    public IEnumerator<T> GetEnumerator()
    {
        throw new NotImplementedException();
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        throw new NotImplementedException();
    }
}
```

图 23.21 由 Visual Studio 的“实现接口”功能生成的代码。

从代码生成的角度来看，这样做非常有益，因为抛出异常也能让编译器的流分析满意：如果一个方法必须返回一个对象，那么改为抛出异常是让生成的代码能够编译的最简单方法。

NotImplementedException 应保留用于表示功能缺失，而不是表示不支持某操作。前者更常用于存根，而 NotSupportedException 则表示在实现它的类型的上下文中，某个接口成员实现没有意义。我们稍后会回到这一点。

## NotSupportedException

NotSupportedException 并不表示某操作没有实现；而是表示实现该操作没有意义。你可能会想，在这种情况下为什么不直接省略该操作，但通常当实现接口或必须使用基类时，你别无选择，只能提供它。

使用这种异常类型的示例可以在 System.IO 命名空间中看到，当处理不支持某些操作（如 Seek）的 Stream 对象时。自定义派生的流对象通常只支持基类功能的一小部分，因此有必要使用 NotSupportedException 来表示缺失的功能。

NotSupportedException 出现的另一个地方是 C# 编译器为迭代器实现所生成的代码中。你可能还记得我们在讨论 LINQ 时提到过，迭代器实现了 IEnumerator<T> 接口，该接口有一个 Reset 方法。然而，这个方法会得到一个抛出此异常的默认实现：

```csharp
static IEnumerator<int> GetNumbers() {
    int i = 0;
    while (true)
        yield return i++;
}

static void Main() {
    var nums = GetNumbers();
    if (nums.MoveNext())
        Console.WriteLine(nums.Current);

    // Oops, we advanced the enumerator too far. Let's try to reset it...
    nums.Reset();            // Throws a NotSupportedException.

    if (nums.MoveNext())
        Console.WriteLine(nums.Current);
}
```

Reset 方法在 .NET 1.0 时代有点过度设计，主要是为了 COM 互操作而存在（可对比 IEnumVARIANT COM 接口）。因为接口规定此方法可能抛出 NotSupportedException，所以作为一个我们可以普遍依赖的抽象，其价值不大。此外，为 foreach 循环生成的代码也从不调用它。

由于所有这些原因，Reset 大多未被使用，C# 迭代器功能也不愿支持它。在代码生成方面，迭代器是最复杂的语言特性之一，因此为了避免为一个额外但用处不大的 Reset 方法增加更多复杂性，这种简化是受欢迎的。如果你真的想重置迭代器，只需请求一个新的迭代器（反正这是一个廉价的操作）：
