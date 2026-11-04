
使用方法组创建委托会执行一些重载解析，以检查方法组所表示的重载集合中是否包含与委托签名兼容的方法。例如，我们可以有多个 IsEven 重载，它们接受的输入参数不同。当该组被赋给期望 int 输入参数的 Filter 委托时，确定委托对象应引用的最佳匹配就是编译器的任务。

委托可以像普通方法一样被调用。这样做时，委托实例所捕获的目标方法将被调用。本质上，委托是一种引入一级间接调用方法的方式。有了我们的 Filter 委托，就可以创建一个通用过滤方法：

```csharp
static int[] Where(int[] numbers, Filter predicate)
{
    // In fact, a more general-purpose Where method exists in LINQ.
    // It uses a generic delegate to filter elements of a generic collection.
    // For a thorough explanation, see the chapter on LINQ.

    var results = new List<int>();
    foreach (int n in numbers)
        if (predicate(n))  // delegate invocation
            results.Add(n);

    return results.ToArray();
}
```

我们将在第 17 章更详细地讨论委托，并在第 18 章“事件”中将其付诸实践（事件在幕后使用委托）。

## 重载解析

当存在具有给定名称的方法的多个重载时，编译器的职责之一是根据给定的参数列表确定要调用哪个方法。存在一套完整的规则来确定“最佳目标”。这些规则在很大程度上对应于常识以及开发人员期望的最佳匹配。可以使用 Math.Abs 方法举一个简单的例子，该方法有七个重载：

```csharp
public static decimal Abs(decimal value);
public static double Abs(double value);
public static float Abs(float value);
public static int Abs(int value);
public static long Abs(long value);
public static sbyte Abs(sbyte value);
public static short Abs(short value);
```

大多数，如果不是全部，读者都会同意在以下使用 Math.Abs 的代码片段中必须调用的重载：

```csharp
int x = int.Parse(Console.ReadLine());
Console.WriteLine("Abs({0}) = {1}", x, Math.Abs(x));
```

因为在可用重载集合中存在方法签名的精确匹配，所以 Math.Abs(int) 候选被选中不足为奇。如果找不到精确匹配，其他规则就会启动以找到最佳可能的匹配：

```csharp
uint x = uint.Parse(Console.ReadLine());
Console.WriteLine("Abs({0}) = {1}", x, Math.Abs(x));
```

虽然对正无符号整数取绝对值意义不大，但它很好地说明了重载解析的要点。因为没有接受 uint 作为唯一参数的精确匹配，所以会考虑隐式转换（参见第 13 章“运算符重载和转换”）。在这种情况下，可以隐式地将 uint 参数转换为 long（即无需用户显式指定），则使用该重载，如图 10.13 所示。这种从 uint 到 long 的隐式转换存在的原因是，每个 32 位无符号整数都可以不失精度地放入 64 位（long）有符号整数中。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_549_0.png)

图 10.13 一个隐式转换弥合了实参与形参之间的差距。

C# 语言规范中存在更多规则以更正式的方式定义重载解析。我不会赘述；如果你感兴趣，请参阅规范。实际操作中你需要知道的是，编译器（而不是运行时）负责找到一个合适的重载。如果所选目标不是预期的目标（这种情况不应该经常发生），总是可以通过添加更多强制转换来影响决策。这也是在找不到最佳匹配且调用存在歧义时引导编译器朝某个方向进行的方式：

```csharp
public static void Main(string[] args)
{
    Bar("Which one", "will you pick?");
}
```

```csharp
public static void Bar(object a, string b) { ... }
public static void Bar(string a, object b) { ... }
```

因为 Bar 的两个重载同样适用（因为每个字符串都是对象，可以如此对待），编译器无法做出决定（幸运的是）并引发错误以提示歧义，如图 10.14 所示。解决此问题的一种方法是显式指定预期的参数类型：

```csharp
public static void Main(string[] args)
{
    Bar((object)"Pick the", "first one");
    Bar("Pick the", (object)"second one");
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_550_0.png)

图 10.14 重载解析期间发现的歧义提示手动解决。

### 泛型中的挑战

泛型是第 15 章的主题，在重载解析方面带来了额外的挑战。基本上，泛型使你能够对用作类型或方法参数的类型进行抽象：

```csharp
public static void Main(string[] args)
{
    Bar<int, string>(1, "2"); // This is fine...
    Bar<int, int>(1, 2);      // ...but what's meant here?
}
```

```csharp
public static void Bar<TFirst, TSecond>(TFirst f, TSecond s) { ... }
public static void Bar<TFirst, TSecond>(TSecond s, TFirst f) { ... }
```

当从泛型方法的用法推断类型参数时，存在一些平局决胜规则，它们会优先选择提供良好匹配的非泛型参数，而不是走泛型路线。例如：

```csharp
public static void Main(string[] args)
{
    Foo(1, 2); // second one is used as "int" is better than "TSecond"
}
```

```csharp
public static void Foo<TFirst, TSecond>(TFirst f, TSecond s) { ... }
public static void Foo<TFirst>(TFirst f, int n) { ... }
```

在设计泛型丰富的 API 时，始终是一个好主意要考虑泛型类型参数的替换可能导致此处所示的歧义的情况。尽可能避免将消歧挑战放在 API 用户身上，因为它们可能相当棘手。

了解重载解析的最佳方式是在 .NET Framework API 等上下文中练习它。重载被广泛用于提供开发人员便利，因此你会经常遇到它们。

### 扩展方法

作为 LINQ 启用语言功能集的一部分，扩展方法于 C# 3.0 中引入，提供了一种扩展现有类型（例如类、结构、接口、枚举、委托）的方法，使其具有可像实例方法一样调用的附加方法。本质上，它们为调用辅助方法提供了用户便利。

在 .NET 3.5 之前（它包含 C# 3.0 和 VB 9.0，两者都将扩展方法作为语言特性），如果不拥有该类型，为现有类型定义附加功能相当麻烦。例如，假设你急需一个反转字符串的方法。能够编写以下代码片段来执行此操作不是很好吗？

```csharp
var input = Console.ReadLine();
Console.WriteLine(input.Reverse());
```

不幸的是，框架设计者没有想在 System.String 类型上引入 Reverse 方法，因此上述代码无法编写。扩展字符串类型不是解决此问题的可行选项，因为你希望 Reverse 方法存在于每个字符串对象上，而不仅仅是某些专门的子类型上。（此外，BCL 中的字符串类型是密封的，因此你无法从它派生，正如你在第 14 章中所学。）引入 Reverse 操作的唯一方法就是定义如下的辅助方法：

```csharp
static class StringExtensions
{
    public static string Reverse(string s)
    {
        var chars = s.ToCharArray();
        Array.Reverse(chars);
        return new string(chars);
    }
}
```
