

## 本章所学内容

| 主题 | 关键概念 |
|---|---|
| 使用泛型类型 | 泛型类型需要一个或多个类型参数才能工作。你可以通过在声明变量时传入所需的类型参数，将泛型类型用作变量的类型。具体做法是将逗号分隔的类型名称列表放在尖括号中。 |
| 可空类型 | 可空类型是可以接受指定值类型的任何值或 `null` 值的类型。你可以使用 `Nullable<T>` 或 `T?` 语法来声明可空类型变量。 |
| `??` 运算符 | 空合并运算符返回其第一个操作数的值；如果第一个操作数为 `null`，则返回第二个操作数的值。 |
| 泛型集合 | 泛型集合非常有用，因为它们内置了强类型支持。你可以使用 `List<T>`、`Collection<T>` 和 `Dictionary<K, V>` 等其他集合类型。这些集合还公开了泛型接口。要对泛型集合进行排序和搜索，可以使用 `IComparer<T>` 和 `IComparable<T>` 接口。 |
| 定义泛型类 | 定义泛型类型与其他类型非常相似，只需在指定类型名称的位置添加泛型类型参数即可。与使用泛型类型一样，你需要将这些参数指定为尖括号内的逗号分隔列表。你可以在代码中任何需要使用类型名称的地方使用泛型类型参数，例如在方法返回值和参数中。 |
| 泛型类型参数约束 | 为了在泛型类型代码中更有效地使用泛型类型参数，你可以限制使用该类型时可供提供的类型。你可以按基类、支持的接口、必须是值类型还是引用类型、是否支持无参数构造函数来约束类型参数。如果没有这些约束，你必须使用 `default` 关键字来实例化泛型类型的变量。 |
| 其他泛型类型 | 除了类之外，你还可以定义泛型接口、泛型委托和泛型方法。 |
| 变体 | 变体是类似于多态的概念，但应用于类型参数。它允许你在两个仅泛型类型参数不同的泛型类型之间互换使用。协变允许在目标类型的类型参数是源类型类型参数的基类时进行转换。逆变允许在关系相反时进行转换。协变类型参数使用 `out` 关键字定义，并且只能用作返回类型和属性 get 访问器类型。逆变类型参数使用 `in` 关键字定义，并且只能用作方法参数。 |

## 13

## 更多 C# 技术

## 本章你将学习

- 了解 `::` 运算符
- 理解全局命名空间限定符
- 创建自定义异常
- 使用事件
- 使用匿名方法
- 使用 C# 特性
- 使用初始化器
- 使用 `var` 类型和类型推断
- 使用匿名类型
- 使用 `dynamic` 类型
- 使用命名和可选方法参数
- 使用 Lambda 表达式

## WROX.COM 本章代码下载

你可以从 www.wrox.com/go/beginningvisualc#2015programming 的 Download Code 选项卡中找到本章的 wrox.com 代码下载。代码位于 Chapter 13 下载中，并根据本章中的名称单独命名。

在本章中，你将继续探索 C# 语言，了解一些在其他地方尚未完全涉及的零散内容。Anders Hejlsberg（C# 的发明者）和微软的其他人员一直在不断更新和完善这门语言。在撰写本书时，最新的更改是 C# 语言第 6 版的一部分，该版本随 Visual Studio 2015 产品线以及 .NET 4.6 一起发布。在本书的这个阶段，你可能会想还有什么其他需要的；事实上，以前版本的 C# 在功能方面并不缺乏。然而，这并不意味着没有办法让 C# 编程的某些方面更简单，也不意味着 C# 与其他技术之间的关系无法得到简化。

你还会对前几章中一直在构建的 CardLib 代码进行一些最终修改，甚至使用 CardLib 来创建一个纸牌游戏。

## `::` 运算符和全局命名空间限定符

`::` 运算符提供了访问命名空间中类型的另一种方式。如果你想使用命名空间别名，但别名与实际命名空间层次结构之间存在歧义，这可能是必要的。在这种情况下，命名空间层次结构的优先级高于命名空间别名。要了解这意味着什么，请考虑以下代码：

```
using MyNamespaceAlias = MyRootNamespace.MyNestedNamespace;
namespace MyRootNamespace
{
    namespace MyNamespaceAlias
    {
        public class MyClass {}
    }
    namespace MyNestedNamespace
    {
        public class MyClass {}
    }
}
```

MyRootNamespace 中的代码可以使用以下内容来引用类：

```
MyNamespaceAlias.MyClass
```

此代码引用的类是 MyRootNamespace.MyNamespaceAlias.MyClass，而不是 MyRootNamespace.MyNestedNamespace.MyClass。也就是说，命名空间 MyRootNamespace.MyNamespaceAlias 隐藏了 using 语句定义的别名，该别名指向 MyRootNamespace.MyNestedNamespace。你仍然可以访问 MyRootNamespace.MyNestedNamespace 命名空间及其包含的类，但需要不同的语法：

```
MyNestedNamespace.MyClass
```

或者，你可以使用 `::` 运算符：

```
MyNamespaceAlias::MyClass
```

使用此运算符会强制编译器使用 using 语句定义的别名，因此代码引用的是 MyRootNamespace.MyNestedNamespace.MyClass。

你还可以将 `global` 关键字与 `::` 运算符结合使用，这实际上是顶级根命名空间的别名。这有助于更清楚地表明你正在引用哪个命名空间，如下所示：

```
global::System.Collections.Generic.List<int>
```

这是你期望的类，即泛型 `List<T>` 集合类。它肯定不是以下代码定义的类：

```
namespace MyRootNamespace
{
    namespace System
    {
        namespace Collections
        {
            namespace Generic
            {
                class List<T> {}
            }
        }
    }
}
```

当然，你应该避免为命名空间起与现有 .NET 命名空间相同的名称，尽管在大型项目中可能会出现类似的问题，特别是当你作为大型团队的一部分工作时。使用 `::` 运算符和 `global` 关键字可能是访问所需类型的唯一方法。

## 自定义异常

第 7 章介绍了异常，并解释了如何使用 `try...catch...finally` 块来处理异常。你还看到了几个标准的 .NET 异常，包括异常的基类 `System.Exception`。有时，从这个基类派生你自己的异常类以在应用程序中使用，而不是使用标准异常，是很有用的。这使你能够向捕获异常的代码发送更具体的信息，并使捕获代码能够更具体地处理哪些异常。例如，你可以向异常类添加一个新属性，以允许访问某些底层信息，从而使异常接收者能够做出所需的更改，或者只是提供有关异常原因的更多信息。

> 注意 System 命名空间中有两个基本的异常类，它们都派生自 Exception：ApplicationException 和 SystemException。SystemException 用作 .NET Framework 预定义异常的基类。ApplicationException 提供给开发人员派生自己的异常类，但最新的最佳实践表明，你不应该从这个类派生异常；你应该使用 Exception。

### 向 CardLib 添加自定义异常

如何使自定义异常再次最好地通过升级 CardLib 项目来说明。`Deck.GetCard()` 方法当前在尝试时抛出一个标准的 .NET 异常

