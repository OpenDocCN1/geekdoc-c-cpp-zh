
`string s1 = "Aidan", s2 = "Grant";`

`Console.WriteLine("s1={0}, s2={1}", s1, s2);`

`Swap(ref s1, ref s2);`

`Console.WriteLine("s1={0}, s2={1}", s1, s2);`

```
}
```

使用带有 **out** 和 **ref** 参数的泛型方法可能特别有趣，因为你作为参数传递变量是为了避免潜在的类型安全漏洞。与 **out/ref** 参数相关的问题在第 9 章“参数”的“通过引用传递参数给方法”节的末尾进行了讨论。事实上，`Interlocked` 类以及 **Exchange** 和 **Compare** 方法也因为这个原因提供了泛型重载：

```csharp
public static class Interlocked {
    public static T Exchange<T>(ref T location1, T value) where T : class;
    public static T CompareExchange<T>(ref T location, T value, T comparand) where T : class;
}
```

# 泛型方法与类型推断

对于许多开发者来说，C# 的泛型语法由于存在所有的小于和大于号而可能令人困惑。为了帮助提高代码创建、可读性和可维护性，C# 编译器在调用泛型方法时提供了类型推断。类型推断意味着编译器在调用泛型方法时尝试自动确定（或推断）要使用的类型。以下是演示类型推断的代码：

```csharp
private static void CallingSwapUsingInference() {
    Int32 n1 = 1, n2 = 2;
    Swap(ref n1, ref n2); // 调用 Swap<Int32>
}
string s1 = "Aidan";
Object s2 = "Grant";
Swap(ref s1, ref s2); // 错误，无法推断类型
}
```

> `where` 子句将在本章节后面的“可验证性与约束”部分进行解释。

在这段代码中，注意对 `Swap` 的调用没有在小于/大于符号指定类型参数。在第一次调用 `Swap` 时，C# 编译器能够推断出 `n1` 和 `n2` 是 `Int32`，因此，它将使用 `Int32` 类型参数调用 `Swap`。

在执行推断时

一个类型可以定义多个方法。以下是调用 `Display` 的几种方式：

```csharp
private static void Display<T>(T o) {
    Console.WriteLine(o);
}
```

```csharp
private static void Display(object o) {
    Console.WriteLine(o);
}
```

```csharp
private static void Display<T>(object o) {
    Console.WriteLine(o);
}
```

在第一次调用时，C# 编译器倾向于更精确的匹配。对于第二次调用，它会使用泛型方法。对于第三次调用，它必须调用泛型方法。

```csharp
Display(5); // 第一次调用
Display("hello"); // 第二次调用
Display<int>(5); // 第三次调用
```

在第一次调用时，C# 编译器倾向于更精确的匹配。对于第二次调用，它使用泛型方法。

# 313 泛型与其他成员

C# 属性、索引器、事件、运算符方法、构造函数和析构函数不能拥有自己的类型参数。然而，它们可以定义在泛型类型内部，且这些成员的代码可以使用类型参数。C# 不允许这些成员指定它们自己的类型参数，因为微软 C# 团队认为很少需要让这些成员成为泛型，而且在语言设计方面的成本是巨大的。例如，当你在代码中使用 `+` 运算符时，编译器可以调用运算符重载。这里没有方法可以指示任何类型参数。

# 可验证性与约束

在编译代码时，C# 编译器会分析并确保代码对于今天或未来定义的任何类型都有效。让我们来看这个方法：

```csharp
private static Boolean MethodTakingAnyType<T>(T o) {
    T temp = default;
    Console.WriteLine(o.ToString());
    Boolean b = temp.Equals(o);
    return b;
}
```

该方法声明了一个类型为 `T` 的临时变量 `temp`，然后方法执行了一些变量赋值和方法调用。该方法适用于任何类型。如果 `T` 是引用类型，它是有效的；如果 `T` 是值类型或枚举，它是有效的；如果 `T` 是接口或委托类型，它是有效的。该方法适用于今天或明天定义的所有类型，因为支持 `Object` 定义的赋值和方法调用（如 `ToString` 和 `Equals`）。

现在来看这个方法：

```csharp
private static T Min<T>(T o1, T o2) {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

`Min` 方法尝试使用 `o1` 变量调用 `CompareTo` 方法。但有许多类型并没有提供 `CompareTo` 方法，因此，C# 编译器无法编译此代码并保证该方法适用于所有类型。如果你尝试编译上述代码，编译器会抛出以下消息：“错误 CS0117: 'T' 不包含到 'CompareTo' 的定义。”。

# 第 12 章 泛型 297

看起来在使用泛型时，你只能声明泛型类型的变量、执行一些变量赋值、调用由 Object 定义的方法，而仅此而已！这使得泛型几乎毫无用处。幸运的是，编译器和 CLR 支持一种名为“约束”（constraints）的机制，你可以利用它让泛型再次变得有用。

约束用于限制指定泛型参数时可以指定的类型数量。限制类型数量允许你对这些类型执行更多操作。这里是 Min 方法的新版本，它指定了一个约束（加粗）：

```csharp
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

C# 中的 `where` 告诉编译器，为 T 指定任何类型必须实现相同类型的泛型接口（T）。由于这个约束，编译器现在允许你调用 `CompareTo` 方法，因为该方法是由 `IComparable<T>` 接口定义的。

现在，当代码引用泛型类型或方法时，编译器负责确保指定了约束。例如，以下代码会导致编译器发出以下消息：“error CS0311: 类型 'object' 不能作为泛型类型或方法 'SomeType.Min<T>' 中的类型参数 'T'。从 'object' 到 'System.IComparable<object>' 没有隐式引用转换”。

```csharp
private static void CalMin() {
    Object o1 = "Jeff", o2 = "Richter";
    Object oMin = Min<Object>(o1, o2); // Error CS0311
}
```

编译器发出此错误是因为 `System.Object` 没有实现 `IComparable<Object>` 接口。事实上，`System.Object` 并没有实现任何接口。

现在你已经了解了约束是什么以及它们如何工作，我们将开始更深入地研究它们。约束可以应用于泛型类型的类型参数，也可以应用于泛型方法的类型参数（如 Min 方法所示）。CLR 不允许通过类型参数名称或约束来进行重载；你可以根据参数个数（arity）对类型进行重载。以下示例展示了我的意思：

```csharp
// 定义以下类型是允许的：
internal sealed class AType {}
internal sealed class AType<T> {}
internal sealed class AType<T1, T2> {}
```

```csharp
// 错误：与没有约束的 AType<T> 冲突
internal sealed class AType<T> where T : IComparable<T> {}
```

# 第二部分 设计类型

```csharp
// 错误：与 AType<T1, T2> 冲突
internal sealed class AType<T3, T4> {}
```

```csharp
internal sealed class AnotherType {
    // 定义以下方法是允许的：
    private static void M() {}
    private static void M<T>() {}
    private static void M<T1, T2>() {}
```

```csharp
// 错误：与没有约束的 M<T> 冲突
    private static void M<T>() where T : IComparable<T> {}
```

```csharp
// 错误：与 M<T1, T2> 冲突
    private static void M<T3, T4>() {}
```

在覆盖虚泛型方法时，覆盖方法必须指定相同数量的类型参数，并且这些类型参数将继承基类方法上指定的约束。事实上，覆盖方法完全不允许在其类型参数上指定任何约束。然而，它可以更改类型参数名称。同样，在实现接口方法时，方法必须与接口方法指定相同数量的类型参数，并且这些类型参数将继承接口方法对其指定的约束。这里是一个通过虚方法演示此规则的示例：

```csharp
internal class Base {
    public virtual void M<T1, T2>()
        where T1 : struct
        where T2 : class {}
}
```

```csharp
internal sealed class Derived : Base {
    public override void M<T3, T4>()
        where T3 : EventArgs // 错误
        where T4 : class // 错误
}
```

尝试编译上述代码会导致编译器发出以下消息：“error CS0460: 覆盖和显式接口实现方法的约束从基方法继承，因此不能直接指定。”如果我们移除 Derived 类中 `M<T3, T4>` 方法的 `where` 行，代码将正常运行。注意，你可以更改类型参数名称（如示例所示：从 T1 更改到 T3，从 T2 更改到 T4）；但是你不能更改（甚至无法指定）约束。

现在让我们谈谈编译器/CLR 允许你应用于类型参数的不同类型的约束。类型参数可以使用主约束、次要约束和/或构造函数约束进行约束。我将在接下来的三个章节讨论这三种约束。

# 主约束

类型参数可以指定零个主约束或一个主约束。主约束可以是一个引用类型，用于标识一个非密封的类。你可以指定以下特殊引用类型之一：`System.Object`、`System.Array`、`System.Delegate`、`System.MulticastDelegate`、`System.ValueType`、`System.Enum` 或 `System.Void`。

当指定引用类型约束时，你向编译器承诺指定的类型参数将是指定的类型或其派生类型。主约束可以是一个标识非密封类的引用类型。

`Nullable<T>` 将参数约束为 `struct`。可空类型将在第 19 章“可空类型”中讨论。

# 次要约束

类型参数可以指定零个或多个次要约束，其中次要约束表示接口类型。当指定接口类型约束时，你向编译器承诺指定的类型参数是实现该接口的类型。由于你可以指定多个接口约束，类型参数必须指定一个实现所有接口约束（以及如果指定了所有的主约束）的类型。第 13 章详细讨论了接口约束。

还有另一种次要约束称为类型参数约束（有时称为裸类型约束）。这种约束的使用频率比接口约束低得多。

这里是一个演示使用类型参数约束的泛型方法：

```csharp
private static List<TBase> ConvertList<T, TBase>(List<T> list)
where T : TBase {
    List<TBase> baseList = new List<TBase>(list.Count);
    for (int32 index = 0; index < list.Count; index++) {
        baseList.Add(list[index]);
    }
    return baseList;
}
```

# 第 12 章 泛型 301

```csharp
private static void CallingConvertIList() {
    // 构建并初始化一个 List<String> (实现了 IList<String>)
    List<String> ls = new List<String>();
    ls.Add("A String");
    // 将 List<String> 转换为 IList<Object>
    IList<Object> lo = ConvertList<String, Object>(ls);
    // 将 List<String> 转换为 IComparable<String>
    IComparable<String> lc = ConvertList<String, IComparable>(ls);
    // 将 List<String> 转换为 IComparable<IComparable<String>>
    IComparable<IComparable<String>> lcs = ConvertList<String, IComparable<String>>(ls);
    // 将 List<String> 转换为 IList<String>
    IList<String> ls2 = ConvertList<String, String>(ls);
    // 将 List<String> 转换为 IList<Exception>
    IList<Exception> le = ConvertList<String, Exception>(ls);// Error
}
```

在第一次调用 Convert 时，编译器确保 String 派生自 Object，第一次调用遵循类型参数约束。在第二次调用 Convert 时，编译器确保 String 兼容 IComparable。由于 String 实现了 IComparable 接口，第二次调用遵循类型参数约束。在第三次调用 Convert 时，编译器确保 String 兼容 IComparable<String>。由于 String 实现了 IComparable<String>接口，第三次调用遵循类型参数约束。在第四次调用 Convert 时，编译器知道 String 与其本身兼容。在第五次调用 Convert 时，编译器确保 String 兼容 Exception。由于 String 不兼容 Exception，第五次调用不符合类型参数约束，编译器输出了以下信息：'error CS0311: 无法将类型 'String' 用作泛型类型或方法类型参数 'T' 中的 'Program.ConvertIList<T,TBase>(System.Collections.Generic.IList<T>)'。从 'string' 到 'System.Exception' 没有隐式引用转换'。

# 构造函数约束

一个类型可以指定零个构造函数约束或一个构造函数约束。在指定构造函数约束时，你向编译器承诺指定的类型参数将是一个实现了公共无参数构造函数的非抽象类型。注意，C# 编译器认为对结构体（struct）指定构造函数约束是多余的，因为所有值类型都隐式提供了公共无参数构造函数。这是一个使用构造函数约束限制其类型参数的示例类：

# 第二部分 设计类型

```csharp
internal sealed class ConstructorConstraint<T> where T : new() {
    public static T Factory() {
        // 允许是因为值隐式地
        // 具有公共无参数构造函数，并且
        // 约束要求任何指定的引用
        // 类型也具有公共无参数构造函数
        return new T();
    }
}
```

在这个示例中，new 一个 T 是合法的，因为 T 已知是一个具有公共无参数构造函数的类型。这对于所有值类型都是如此，而构造函数约束要求任何作为类型参数指定的引用类型也必须满足这一点。

有时，开发者希望通过约束来声明类型，其中该约束允许构造函数接收各种参数。目前，CLR（以及 C# 编译器）仅支持无参数构造函数。微软认为这对于几乎所有场景都是足够的，我表示同意。

# 其他可验证性问题

在本节的剩余部分中，我想指出一些在与泛型配合使用时产生意外行为的代码结构，或者如何使用约束使代码再次具有可验证性。

# 泛型类型变量的转换

将泛型类型变量转换为另一种类型是非法的，除非你将其转换为带有约束的类型：

```csharp
private static void CastingGenericVariable1<T>(T obj) {
```
