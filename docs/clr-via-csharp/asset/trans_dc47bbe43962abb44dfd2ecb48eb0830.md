
现在可以使用任何表达式来调用上面的扩展方法，只要该表达式的结果类型实现了 IEnumerable<T> 接口：

```csharp
public static void Main() {
    // Shows each Char on a separate line in the console
    "Grant".ShowItems();

    // Shows each String on a separate line in the console
    new[] { "Jeff", "Kristin" }.ShowItems();

    // Shows each Int32 value on a separate line in the console
    new List<Int32>() { 1, 2, 3 }.ShowItems();
}
```

> **重要** 扩展方法是 Microsoft 语言集成查询（LINQ）技术的基石。要查看提供大量扩展方法的类的绝佳示例，请参阅 Microsoft .NET Framework SDK 文档中的静态 **System.Linq.Enumerable** 类及其所有静态扩展方法。此类中的每个扩展方法都扩展了 **IEnumerable** 或 **IEnumerable<T>** 接口。

你也可以为委托类型定义扩展方法。有关示例，请翻到第 11 章“事件”的第 278 页。你还可以向枚举类型添加扩展方法。我在第 15 章“枚举类型和位标志”的“向枚举类型添加方法”一节中展示了相关示例。

最后但同样重要的是，我想指出 C# 编译器允许你创建一个委托（更多信息请参见第 17 章“委托”），该委托引用针对某个对象的扩展方法：

```csharp
public static void Main () {
    // Create an Action delegate that refers to the static ShowItems extension method
    // and has the first argument initialized to reference the “Jeff” string.
    Action a = "Jeff".ShowItems;
    .
    .
    .
    // Invoke the delegate which calls ShowItems passing it a reference to the “Jeff” string.
    a();
}
```

在上面的代码中，C# 编译器生成 IL 代码来构造一个 **Action** 委托。创建委托时，构造函数会接收应调用的方法，还会接收一个对象引用，该引用应传递给方法隐藏的 **this** 参数。通常，当你创建引用静态方法的委托时，对象引用为 **null**，因为静态方法没有 **this** 参数。然而，在此示例中，C# 编译器生成了一些特殊代码，创建一个引用静态方法（**ShowItems**）的委托，并且该静态方法的目标对象是对“Jeff”字符串的引用。稍后，当调用委托时，CLR 将调用该静态方法，并向其传递对“Jeff”字符串的引用。这有点取巧，但效果很好，而且只要你不去想内部发生了什么，就会感觉很自然。

### 扩展特性

如果扩展方法的这一概念不是 C# 特有的，那将是最好的。具体来说，我们希望程序员能在某种编程语言中定义一组扩展方法，并让使用其他编程语言的人也能利用它们。为此，所选的编译器必须支持在静态类型和方法中搜索可能匹配的扩展方法。而且编译器需要快速完成这项工作，以便将编译时间保持在最低限度。

在 C# 中，当你用 **this** 关键字标记静态方法的第一个参数时，编译器会在内部对该方法应用一个自定义特性，并且该特性会持久化到生成文件的元数据中。该特性定义在 System.Core.dll 程序集中，如下所示：

```csharp
// Defined in the System.Runtime.CompilerServices namespace
[AttributeUsage(AttributeTargets.Method | AttributeTargets.Class | AttributeTargets.Assembly)]
public sealed class ExtensionAttribute : Attribute {
}
```

此外，该特性还会应用于任何包含至少一个扩展方法的静态类的元数据。并且，该特性还会应用于任何包含至少一个含有扩展方法的静态类的程序集的元数据。因此现在，在编译调用不存在的实例方法的代码时，编译器可以快速扫描所有被引用的程序集，以了解哪些程序集包含扩展方法。然后，它只需扫描这些程序集中的静态类来查找包含扩展方法的类，并且只需扫描扩展方法来寻找潜在匹配项，从而尽可能快地编译代码。

![](img/3c46ff5b170881db4209d365b1f7a808_230_0.png)

> **注意** **ExtensionAttribute** 类定义在 System.Core.dll 程序集中。这意味着，即使我在编译代码时不使用 System.Core.dll 中的任何类型，甚至不引用 System.Core.dll，编译器生成的结果程序集也会在其中嵌入对 System.Core.dll 的引用。不过，这并不是太大的问题，因为 **ExtensionAttribute** 仅在编译时使用；在运行时，除非应用程序使用该程序集中的其他内容，否则不必加载 System.Core.dll。

### 分部方法

设想你使用一个工具生成包含类型定义的 C# 源代码文件。该工具知道，在它生成的代码中可能存在你希望自定义类型行为的位置。通常，自定义会通过让工具生成的代码调用虚方法来完成。工具生成的代码还必须包含这些虚方法的定义，而这些方法的实现方式是不做任何事，只是返回。现在，如果你想自定义类的行为，你会定义自己的类，从基类派生它，然后重写实现该行为的任何虚方法，使其具有你想要的行为。下面是一个示例：

```csharp
// Tool-produced code in some source code file:
internal class Base {
    private String m_name;

    // Called before changing the m_name field
    protected virtual void OnNameChanging(String value) {
    }

    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper());  // Inform class of potential change
            m_name = value;                   // Change the field
        }
    }
}
```

```csharp
// Developer-produced code in some other source code file:
internal class Derived : Base {
    protected override void OnNameChanging(String value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

不幸的是，上面的代码存在两个问题：

- 该类型必须是非密封类。你不能对密封类或值类型使用此技术（因为值类型是隐式密封的）。此外，你不能对静态方法使用此技术，因为静态方法不能被重写。
- 这里存在效率问题。仅仅为了重写一个方法而定义类型，这会浪费少量系统资源。而且，即使你不想重写 **OnNameChanging** 的行为，基类代码仍然会调用一个虚方法，而该方法除了返回之外什么也不做。另外，无论 **OnNameChanging** 是否访问传递给它的参数，都会调用 **ToUpper**。

C# 的分部方法功能允许你在修复上述问题的同时选择重写类型的行为。下面的代码使用分部方法来实现与前面代码相同的语义：

分部方法不能有 **out** 参数，因为该方法必须初始化该参数，而该方法可能不存在。分部方法可以有 **ref** 参数，可以是泛型的，可以是实例方法或静态方法，并且可以标记为 **unsafe**。

- 当然，定义分部方法的声明和实现分部方法的声明必须具有相同的签名。如果两者都应用了自定义特性，则编译器会将两个方法的特性合并在一起。应用于参数的任何特性也会合并。
- 如果没有实现分部方法的声明，那么你不能有任何试图创建引用该分部方法的委托的代码。原因同样是该方法在运行时不存在。编译器会产生以下消息：**"error CS0762: Cannot create delegate from method 'Base.OnNameChanging(string)' because it is a partial method without an implementing declaration"**。
- 分部方法始终被视为私有方法。但是，C# 编译器禁止你在分部方法声明前放置 **private** 关键字。

