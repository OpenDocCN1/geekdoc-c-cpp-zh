

好的——所以这解释了编译器如何解决我之前提到的与代码可维护性相关的最后两个问题。我还没有处理第一个问题：一个甚至不知道 `IndexOf` 是否存在的程序员，如何知道有一个对 `StringBuilder` 进行操作的方法呢？这个问题的答案在 Microsoft Visual Studio 的 IntelliSense 功能中。在编辑器中，当你输入一个点号时，Visual Studio 的 IntelliSense 窗口会打开，向你显示可用方法的列表。此外，IntelliSense 还会显示你在点号左侧表达式类型对应的任何扩展方法。图 8-1 显示，Visual Studio 扩展方法的 IntelliSense 图标旁边有一个向下箭头，方法旁边的工具提示指示该方法是一个扩展方法。这真的太棒，因为你可以在各种类型的对象上轻松定义自己的方法，而且其他程序员可以通过使用这些类型对象来自然地发现这些方法。

![](img/0ce3b788d061e3d3095fa554b1a34adf_225_0.png)

图 8-1 Visual Studio 的 IntelliSense 窗口，扩展方法。

## 规则与指南

关于扩展方法，你还需要了解一些额外的规则和指南：

- C# 支持扩展方法；但它不提供扩展属性、扩展事件、扩展运算符等。

- 扩展方法（其第一个参数前带有 `this` 关键字的方法）必须声明在非泛型的静态类中。然而，对类的名称没有限制；你可以使用任何你喜欢的名称。当然，一个扩展方法必须至少有一个参数，且只有第一个参数可以标记为 `this` 关键字。

## 第二部分 设计类型

- C# 编译器会寻找定义在文件作用范围（file scope）内的静态类中的定义的扩展方法。换句话说，如果你将静态类嵌套在另一个类内部，C# 编译器将发出以下信息：`error CS1109: Extension method must be defined in a top-level static class; StringBuilderExtensions is in a nested class.`。

- 由于静态类可以是任何名称，C# 编译器寻找扩展方法需要时间，因为它必须查看所有文件作用范围内的静态类，并扫描它们的静态方法以进行匹配。为了提高性能并避免考虑你未使用的扩展方法，C# 编译器要求你“导入”扩展方法。例如，如果有人在 `Win` 命名空间中定义了 `StringBuilderExtensions` 类，那么想要访问该类扩展方法的程序员必须在其源代码文件顶部使用 `using` 指令。

- 多个静态类可能会定义相同的扩展方法。如果编译器检测到存在两个或多个扩展方法，编译器会发出以下信息：`error CS0121: The call is ambiguous between the following methods or properties: 'StringBuilderExtensions.IndexOf(string, char)' and 'OtherStringBuilderExtensions.IndexOf(string, char)'.` 要修复此问题，你必须修改源代码。具体来说，你不能再使用静态方法调用语法；相反，你现在需要使用静态方法语法来显式指定静态类的名称，以明确告诉编译器你想要调用哪个方法。

- 你应该谨慎使用此功能，因为并不是所有程序员都熟悉它。例如，当你用扩展方法扩展一个类型时，你实际上也通过该方法扩展了所有类型。因此，你不应该定义一个第一个参数为 `System.Object` 的扩展方法，因为该方法对所有表达式类型都是可调用的，这会严重污染 Visual Studio 的 IntelliSense 窗口。

- 扩展方法存在潜在的版本控制问题。如果未来 Microsoft 在其 `StringBuilder` 类中添加了与我的代码尝试调用的原型相同的 `IndexOf` 方法，当当我重新编译代码时，编译器将绑定到 Microsoft 的 `IndexOf` 方法而不是我的方法。由于这种情况，我的程序将产生不同的行为。这个版本控制问题是该功能应该被谨慎使用的另一个原因。

## 使用扩展方法扩展各种类型

在本章中，我演示了如何为 `StringBuilder` 类定义扩展方法。我想指出的是，由于扩展方法实际上是静态方法，CLR 不会生成代码来确保调用该方法的表达式值不为 null。

```csharp
// sb 为 null
StringBuilder sb = null;
```

// 调用扩展方法：调用 IndexOf 时**不会**抛出 NullReferenceException
// 在 IndexOf 的 for 循环内部会抛出 NullReferenceException
sb.IndexOf('X');

// 调用实例方法：调用 Replace 时**会**抛出 NullReferenceException
sb.Replace('.', '!');
```

我想指出，如如下代码所示，你可以为接口类型定义扩展方法。

```csharp
public static void ShowItems<T>(this IEnumerable<T> collection) {
    foreach (var item in collection)
        Console.WriteLine(item);
}
```

上述扩展方法可以使用任何结果为实现了 `IEnumerable<T>` 接口类型的表达式来调用。

```csharp
public static void Main() {
    // 在控制台中单独行显示 Char
    "Grant".ShowItems();

    // 在控制台中单独行显示 String
    new[] { "Jeff", "Kristin" }.ShowItems();

    // 在控制台中单独行显示 Int32 值
    new List<Int32>{ 1, 2, 3 }.ShowItems();
}
```

> 重要的扩展方法是 Microsoft 语言集成查询 (LINQ) 技术的基石。

