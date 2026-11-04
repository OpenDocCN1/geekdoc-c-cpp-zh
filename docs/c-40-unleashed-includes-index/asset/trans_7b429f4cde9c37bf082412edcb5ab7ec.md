
由于 .NET 中的字符串是不可变的，因此无法就地修改它们，所以要完成此任务，你需要创建一个包含逆序字符序列的新字符串。利用前面的辅助方法，你现在可以编写如下代码：

```csharp
var input = Console.ReadLine();
Console.WriteLine(StringExtensions.Reverse(input));
```

遗憾的是，这极大地破坏了代码的“流畅性”。尤其是，无法将一组转换字符串的方法调用“链接在一起”。例如：

```csharp
var input = Console.ReadLine();
Console.WriteLine(input.ToUpper().Reverse().ToLower());
```

这种过度的链式调用是否是一件好事，尚可争论。因为每个中间方法调用都可能返回 null 或抛出异常，所以要找出故障点可能变得相当困难。此外，没有局部变量保存中间结果，而中间结果对调试可能很有用。尽管如此，在许多情况下，对辅助方法的需求确实破坏了代码的流畅性和从左到右的阅读体验：

```csharp
var input = Console.ReadLine();
Console.WriteLine(StringExtensions.Reverse(input.ToUpper()).ToLower());
```

LINQ 就是其中一个非常需要流畅模式的具体 API。我们稍后会对此进行更详细的讨论（参见第 19 章“语言集成查询基础”），但现在请从语法角度对比下面两个示例查询。我相信你会同意第一个更易读，并且能更好地传达操作的顺序：

```csharp
var resNew = new[] { 1, 2, 3 }
    .Where(x => x % 2 == 0)
    .Select(x => x.ToString());
```

```csharp
var resOld = Enumerable.Select(
    Enumerable.Where(
        new[] { 1, 2, 3 },
        x => x % 2 == 0
    ),
    x => x.ToString()
);
```

实际上，第一个代码片段在编译时通过扩展方法这一语言特性被转换为第二个代码片段。暂时忽略看起来奇怪的箭头语法；那些是 lambda 表达式，将在第 17 章中讨论。如果你想大声读出代码，可以把粗箭头读作“goes to（指向）”，这样你应该就能体会到那些 lambda 表达式代表了什么。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_554_0.png)

图 10.15 IntelliSense 中显示的扩展方法。

请注意，System.String 上似乎还存在另一个 Reverse 扩展方法。实际上，这是泛型 `IEnumerable<T>` 接口类型上的扩展方法，它被定义为 LINQ 标准查询运算符的一部分。每个字符串都是字符序列，因此 System.String 实现了 `IEnumerable<char>` 接口。LINQ 中的 Reverse 运算符可以作用于任何序列（任意类型 T）并以逆序返回该序列。

## 静态类

请注意，扩展方法定义在静态类中，这是编译器强制执行的要求。静态类是在 C# 2.0 中引入的，以防止因忘记将方法标记为 static 而创建出不可用的类。在 C# 2.0 之前，要声明只包含静态工具方法的类，通常采用以下模式：

```csharp
class Helpers
{
    private Helpers() {}
    public static void Bar() { ... }
    ...
}
```

通过定义私有实例构造函数（参见第 12 章），任何人都无法创建辅助类的实例，这显然是正确的做法，因为类上的所有方法都是静态的，因此不需要实例即可操作。然而，这类类型定义中的错误并未被发现，尤其是当有人添加方法却忘记将其标记为 static 时：

```csharp
class Helpers
{
    private Helpers() {}
    public static void Bar() { ... }
    public void Foo() { ... }    // Oops, forgot to mark as static
    ...
}
```

现在，没有人可以调用此方法（除非使用反射 API 之类的非常手段），因为无法创建实例来调用该方法。通过将类标记为 static，编译器强制规定只能定义静态成员。

## 重载解析

实际上，出现两个 Reverse 扩展方法这一事实说明了重载解析同样适用于扩展方法。当我们编写以下代码时，编译器认为 string 上的扩展方法比 `IEnumerable<T>` 上定义的扩展方法（将 T 替换为 char）更匹配：

```csharp
var input = Console.ReadLine();
Console.WriteLine(input.Reverse());
```

因此，我们的方法将优先于 LINQ API 定义的方法。此外，仅当找不到合适的实例方法时，才会考虑扩展方法。换句话说，在尝试查找实例方法的所有尝试都失败后，它们会作为“最后机会查找”操作来执行：

```csharp
static class StringExtensions
{
    public static string Substring(this string s, int startIndex)
    {
```

尽管像前面那样定义扩展方法是合法的，但你无法通过“实例调用语法”调用它，因为 System.String 已经有一个接受 int 参数的 Substring 方法：

```csharp
var art = "Bart".Substring(1);
```

因为找到了实例方法，编译器就不必再去寻找以 string 为第一个参数、后面接受 int 的扩展方法。如果我们仍然想调用自己的扩展方法，可以使用静态方法调用语法来调用：

```csharp
var art = StringExtensions.Substring("Bart", 1);
```

请注意，由于这种重载解析的顺序，只有在所有实例方法查找都失败后才会尝试使用扩展方法，因此扩展方法不能因为“比实例方法更匹配”而被调用。例如：

```csharp
static class StringExtensions
{
    public static string Substring(this string s, byte startIndex)
    {
```

前面的扩展方法可以被定义为一种高效的 substring，它利用了接收 byte 大小的 startIndex 而不是 32 位整数这一特点。所以，如果我们编写一个索引类型为 byte 的 substring 调用，编译器会首先寻找合适的实例方法。因为 byte 可以隐式转换为 int，所以它会选择 System.String 上定义的 Substring 方法，永远不会考虑我们的“重载”：

```csharp
var art = "Bart".Substring( (byte)1); // Calls System.String.Substring
```

这可能一开始会令人惊讶，但这是为了确保 C# 2.0 代码即使在 C# 3.0 中重新编译后仍能像以前一样工作而采取的措施之一。

## 版本控制的故事

由于前面解释的重载解析规则，扩展方法的版本控制故事并不美好。只要 `this` 参数的类型引入了同名的实例方法，那么在重新编译使用该同名扩展方法的代码时，该实例方法将首先被考虑。例如，如果 .NET 4.x 在 System.String 上引入一个不带任何参数的 Reverse 实例方法，那么当你针对该新平台重新编译代码时，将会选用该方法。如果此方法的行为与我们自己的扩展方法不同，则可能导致意想不到的变化。

尽管如此，一旦发现此类回归，你始终可以通过改用静态方法调用来切换回调用扩展方法。当代码升级到使用较新版本的库或框架（这些库或框架可能带来了新的且冲突的实例方法）时，工具能够帮助检测此类版本问题也并非难以想象。

## 使用扩展方法

你已经看到了如何简单地通过将第一个参数作为左侧来使用扩展方法（模仿实例方法调用语法），但另一个问题是这些扩展方法如何变为可用。答案在于命名空间的使用，这将在第 24 章“命名空间”中介绍。简而言之，命名空间提供了一种以分层方式对类型进行分组的手段。例如，System.Text 命名空间包含 StringBuilder 等类型，而 System.IO 包含处理文件、流等的类型。你不必到处指定完整的类型名，而是可以在 C# 中使用 `using` 关键字导入命名空间：

```csharp
using System;

class Program
{
    static void Main()
    {
        // Same as writing System.Console.WriteLine("Hello");
        Console.WriteLine("Hello");
    }
}
```
