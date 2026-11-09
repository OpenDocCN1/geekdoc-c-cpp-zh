
名为 `IndexOf` 的方法接受单个 `Char` 参数。如果存在匹配的实例方法，那么编译器会生成 IL 代码来调用它。如果不存在匹配的实例方法，那么编译器会查看所有静态类，这些静态类定义了名为 `IndexOf` 的静态方法，并且该静态方法的第一个参数类型与用于调用该方法的表达式类型匹配。该类型还必须用 `this` 关键字标记。在此示例中，表达式是 `sb`，其类型为 `StringBuilder`。在这种情况下，编译器专门查找接受两个参数的 `IndexOf` 方法：一个 `StringBuilder`（用 `this` 关键字标记）和一个 `Char`。编译器会找到我们的 `IndexOf` 方法，并生成调用我们静态方法的 IL 代码。

好——那么现在解释了编译器如何改善我前面提到的与代码可理解性相关的最后两个问题。然而，我还没有解决第一个问题：程序员如何知道存在一个可以操作 `StringBuilder` 对象的 `IndexOf` 方法？这个问题的答案在 Microsoft Visual Studio 的 IntelliSense 功能中。在编辑器中，当你键入一个句点时，Visual Studio 的 IntelliSense 窗口会打开，向你显示可用的实例方法列表。其实，该 IntelliSense 窗口还会显示句点左侧表达式类型所存在的任何扩展方法。图 8-1 显示了 Visual Studio 的 IntelliSense 窗口；扩展方法的图标旁边有一个向下箭头，方法旁边的工具提示表明该方法实际上是一个扩展方法。这真是太棒了，因为现在可以轻松定义自己的方法来操作各种类型的对象，并让其他程序员在使用这些类型的对象时自然地发现你的方法。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_202_0.png)

**图 8-1** Visual Studio 的 IntelliSense 窗口，显示扩展方法。

## 规则和指南

关于扩展方法，还有一些你应该了解的附加规则和指南：

- C# 仅支持扩展方法；它不提供扩展属性、扩展事件、扩展运算符等。
- 扩展方法（第一个参数前带 this 的方法）必须在非泛型静态类中声明。不过，类的名称没有限制；你可以随意命名。当然，扩展方法必须至少有一个参数，并且只有第一个参数可以用 this 关键字标记。
- C# 编译器只查找那些自身定义在文件作用域的静态类中定义的扩展方法。换言之，如果你将静态类嵌套定义在另一个类中，C# 编译器将发出以下消息："error CS1109: 扩展方法必须定义在顶级静态类中；StringBuilderExtensions 是嵌套类。"
- 由于静态类可以是你想要的任何名称，C# 编译器在查找扩展方法时需要时间，因为它必须查看所有文件作用域的静态类，并扫描它们的静态方法以寻找匹配项。为了提高性能，同时避免考虑你可能不想要的扩展方法，C# 编译器要求你“导入”扩展方法。例如，如果某人在 Wintellect 命名空间中定义了 StringBuilderExtensions 类，那么想要访问该类扩展方法的程序员必须在其源代码文件顶部放置 using Wintellect; 指令。
- 多个静态类有可能定义相同的扩展方法。如果编译器检测到存在两个或更多扩展方法，那么编译器会发出以下消息："error CS0121: 以下方法或属性之间的调用不明确：'StringBuilderExtensions.IndexOf(string, char)' 和 'AnotherStringBuilderExtensions.IndexOf(string, char)'。" 要修复此错误，必须修改源代码。具体来说，你不能再使用实例方法语法来调用这个静态方法；相反，现在必须使用静态方法语法，在其中显式指出静态类的名称，以明确告诉编译器你想调用哪个方法。
- 你应谨慎使用此功能，因为并非所有程序员都熟悉它。例如，当你用扩展方法扩展某个类型时，实际上也在用该方法扩展派生类型。因此，你不应定义第一个参数为 System.Object 的扩展方法，因为该方法将可被所有表达式类型调用，并且这确实会污染 Visual Studio 的 IntelliSense 窗口。
- 扩展方法存在潜在的版本化问题。如果将来 Microsoft 向其 StringBuilder 类添加一个与我代码尝试调用的方法具有相同原型的 IndexOf 实例方法，那么当我重新编译代码时，编译器将绑定到 Microsoft 的 IndexOf 实例方法，而不是我的静态 IndexOf 方法。因此，我的程序将表现出不同的行为。这个版本化问题是应谨慎使用此功能的另一个原因。

## 使用扩展方法扩展各种类型

在本章中，我演示了如何为 StringBuilder 类定义扩展方法。我想指出，由于扩展方法实际上是对静态方法的调用，CLR 不会生成代码来确保用于调用该方法的表达式的值不为 null：

```csharp
// sb is null
StringBuilder sb = null;

// Calling extension method: NullReferenceException will NOT be thrown when calling IndexOf
// NullReferenceException will be thrown inside IndexOf's for loop
sb.IndexOf('X');

// Calling instance method: NullReferenceException WILL be thrown when calling Replace
sb.Replace('.', '!');
```

我还想指出，你可以为接口类型定义扩展方法，如下代码所示：

```csharp
public static void ShowItems<T>(this IEnumerable<T> collection) {
    foreach (var item in collection)
        Console.WriteLine(item);
}
```

现在可以使用任何结果为实现了 IEnumerable<T> 接口的类型的表达式来调用上述扩展方法：

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

**重要** 扩展方法是 Microsoft 语言集成查询（LINQ）技术的基石。关于提供许多扩展方法的类的一个很好的示例，请参阅 Microsoft .NET Framework SDK 文档中的静态 System.Linq.Enumerable 类及其所有静态扩展方法。该类中的每个扩展方法都扩展 IEnumerable 或 IEnumerable<T> 接口。

你也可以为委托类型定义扩展方法。下面是一个示例：

```csharp
public static void InvokeAndCatch<TException>(this Action<Object> d, Object o)
    where TException : Exception {
    try { d(o); }
    catch (TException) { }
}
```

下面是调用它的示例：

```csharp
Action<Object> action = o => Console.WriteLine(o.GetType()); // throws NullReferenceException
action.InvokeAndCatch<NullReferenceException>(null);          // Swallows NullReferenceException
```

你还可以向枚举类型添加扩展方法。我在第 15 章“枚举类型和位标志”的“向枚举类型添加方法”一节中展示了相关示例。

最后但同样重要的是，我想指出，C# 编译器允许你创建一个委托（更多信息参见第 17 章“委托”），该委托引用某个对象上的扩展方法：

```csharp
public static void Main () {
    // Create an Action delegate that refers to the static ShowItems extension method
    // and has the first argument initialized to reference the "Jeff" string.
    Action a = "Jeff".ShowItems;
    .
    .
    .
    // Invoke the delegate which calls ShowItems passing it a reference to the "Jeff" string.
    a();
}
```

在上面的代码中，C# 编译器生成 IL 代码来构造一个 Action 委托。创建委托时，构造函数会接收应被调用的方法，还会接收一个对象引用，该对象应传递给方法的隐藏 this 参数。通常，当你创建引用静态方法的委托时，对象引用为 null，因为静态方法没有 this 参数。然而，在此示例中，C# 编译器生成了一些特殊代码，创建一个引用静态方法（ShowItems）的委托，并且该静态方法的目标对象是对 "Jeff" 字符串的引用。之后，当调用委托时，CLR 将调用该静态方法，并将对 "Jeff" 字符串的引用传递给它。这有点取巧，但它工作得很好，而且只要不去想内部发生了什么，就会感觉很自然。

## 扩展特性

如果扩展方法这一概念并非 C# 专有，那将是最好的。具体来说，我们希望程序员在某种编程语言中定义一组扩展方法，并让其他编程语言中的人能够利用它们。为此，所选的编译器必须支持搜索静态类型和方法以寻找可能匹配的扩展方法。而且编译器需要快速完成这项工作，以便将编译时间保持在最低限度。

在 C# 中，当你用 this 关键字标记静态方法的第一个参数时，编译器会在内部对该方法应用一个自定义特性，并且该特性会持久化到生成文件的元数据中。该特性定义在 System.Core.dll 程序集中，其形式如下：
