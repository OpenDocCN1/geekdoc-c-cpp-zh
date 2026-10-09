

在此处，`Show<>` 的实现本身并未直接使用 `IComparable<>` 接口的任何成员，因此你可能会疑惑为何需要该约束。然而请记住，`BinaryTree<>` 类确实需要此约束（参见列表 12.39）。

### 列表 12.39：要求 IComparable<> 类型参数的 BinaryTree<>

```csharp
public class BinaryTree<>
where T: System.IComparable<>
{
...
}
```

由于 `BinaryTree<>` 类要求其类型参数 T 具有此约束，且 `Show<>` 使用其类型参数 T 作为对应于受约束类型参数的类型实参，因此 `Show<>` 需要确保类类型参数上的约束在其方法类型实参上得到满足。

## 高级主题

## 泛型方法内的类型转换

在某些情况下，使用泛型时需要谨慎——例如，当专门使用泛型来掩盖类型转换操作时。考虑以下方法，它将流转换为指定类型的对象：

```csharp
public static T Deserialize<>(
    Stream stream, IFormatter formatter)
{
    return (T)formatter.Deserialize(stream);
}
```

格式化程序负责从流中移除数据并将其转换为对象。格式化程序上的 `Deserialize()` 调用返回类型为 `object` 的数据。使用 `Deserialize()` 的泛型版本的调用看起来如下所示：

```csharp
string greeting =
    Deserialization.Deserialize<>(stream, formatter);
```

这段代码的问题在于，对于方法的调用者来说，`Deserialize<>()` 看起来是类型安全的。然而，实际上在调用者背后仍然执行了类型转换操作，这与此处所示的非泛型等价情况类似：

```csharp
string greeting =
    (string)Deserialization.Deserialize(stream, formatter);
```

该转换可能在运行时失败；该方法可能并不像表面看起来那样类型安全。`Deserialize<T>` 方法之所以是泛型的，仅仅是为了向调用者隐藏转换操作的存在，这似乎具有危险性的欺骗性。最好让该方法是非泛型的并返回 `object`，从而使调用者意识到它不是类型安全的。如果没有任何约束来验证转换的有效性，开发人员在泛型方法中进行类型转换时应格外小心。

## 准则

避免使用那些看似类型安全但实际上并非如此泛型方法误导调用者。

## 协变与逆变

泛型类型的新用户经常问的一个问题是，为什么类型为 `List<string>` 的表达式不能赋值给类型为 `List<object>` 的变量——既然 `string` 可以转换为 `object` 类型，那么字符串列表应该也与对象列表兼容，对吗？但就一般情况而言，这既不是类型安全的，也不合法。如果你使用相同的泛型类声明两个具有不同类型参数的变量，即使是从更具体的类型赋值给更通用的类型，这些变量在类型上也不兼容——换句话说，它们不是协变的。

协变是范畴论中的一个技术术语，但其基本概念很简单：假设两个类型 X 和 Y 具有特殊关系——即类型 X 的每个值都可以转换为类型 Y。如果类型 `I<X>` 和 `I<Y>` 总是也保持这种相同的特殊关系，我们就说“`I<T>` 在 T 上是协变的”。在处理仅有一个类型参数的简单泛型类型时，可以理解类型参数，我们简单地称“`I<T>` 是协变的”。从 `I<X>` 到 `I<Y>` 的转换称为协变转换。

例如，泛型类 `Pair<Contact>` 和 `Pair<PdaItem>` 的实例即使在类型实参本身兼容的情况下，在类型上也不兼容。换句话说，编译器阻止将 `Pair<Contact>` 转换为 `Pair<PdaItem>`（无论是隐式还是显式），即使 `Contact` 继承自 `PdaItem`。类似地，将 `Pair<Contact>` 转换为接口类型 `IPair<PdaItem>` 也会失败。参见列表 12.40 中的示例。

### 列表 12.40：具有不同类型参数的泛型之间的转换

```csharp
// ...
// 错误：无法转换类型 ...
Pair<PdaItem> pair = (Pair<PdaItem>) new Pair<Contact>();
IPair<PdaItem> duple = (IPair<PdaItem>) new Pair<Contact>();
```

但这为什么是不合法的？为什么 `List<T>` 和 `Pair<T>` 不是协变的？列表 12.41 展示了如果 C# 语言允许不受限制的泛型协变会发生什么。

### 列表 12.41：防止协变保持同质性

```csharp
//...
Contact contact1 = new Contact("Princess Buttercup"),
Contact contact2 = new Contact("Inigo Montoya");
Pair<Contact> contacts = new Pair<Contact>(contact1, contact2);

// 这会给出错误：无法转换类型 ...
// 但假设它没有
// IPair<PdaItem> pdaPair = (IPair<PdaItem>) contacts;
// 这完全合法但不是类型安全的
// pdaPair.First = new Address("123 Sesame Street");
...
```

`IPair<PdaItem>` 可以包含一个地址，但该对象实际上是一个只能包含联系人而不能包含地址的 `Pair<Contact>`。如果允许不受限制的泛型协变，类型安全将被完全破坏。现在也应该很清楚为什么字符串列表不能用作对象列表。你不能将整数插入字符串列表，但你可以将整数插入对象列表；因此，将字符串列表转换为对象列表必须是非法的，这是编译器可以强制执行的一个错误。

## 在 C# 4.0（及更高版本）中通过 out 类型参数修饰符启用协变

你可能已经注意到，之前描述的两个由不受限制的协变引起的问题，是因为泛型对（pair）和泛型列表允许向其内容写入。假设我们通过创建一个只读接口 `IReadOnlyPair<T>` 来消除这种可能性，该接口仅将 T 作为从接口“输出”（即用作方法返回类型或只读属性）而绝不“输入”（即用作形式参数或可写属性类型）。如果我们将自己限制在关于 T 的“仅输出”接口上，那么刚刚描述的协变问题就不会发生（参见列表 12.42）。

### 列表 12.42：可能实现的协变

```csharp
interface IReadOnlyPair<T>
{
  T First { get; }
  T Second { get; }
}

interface IPair<T>
{
  T First { get; set; }
  T Second { get; set; }
}

public struct Pair<T> : IPair<T>, IReadOnlyPair<T>
{
  // ...
}

class Program
{
  static void Main()
  {
    // 错误：在没有 out 类型参数修饰符的情况下，这只是理论上可能
    Pair<Contact> contacts =
      new Pair<Contact>(
        new Contact("Princess Buttercup"),
        new Contact("Inigo Montoya") );
    IReadOnlyPair<PdaItem> pair = contacts;
    PdaItem pdaItem1 = pair.First;
    PdaItem pdaItem2 = pair.Second;
  }
}
```

当我们限制泛型类型声明仅作为数据从接口输出时，编译器没有理由阻止协变。对 `IReadOnlyPair<PdaItem>` 实例的所有操作都会将联系人（来自原始的 `Pair<Contact>` 对象）向上转换为基类 `PdaItem`——这是一个完全有效的转换。没有方法将地址“写入”该对象，因为该对象实际上是一对联系人，而接口未公开任何可写属性。

列表 12.42 中的代码仍然无法编译。然而，C# 4 增加了对安全协变的支持。要指示某个泛型接口旨在其某个类型参数上是协变的，你可以使用 `out` 类型参数修饰符声明该类型参数。列表 12.43 展示了如何修改接口声明以指示应允许协变。

### 列表 12.43：使用 out 类型参数修饰符实现协变

```csharp
  ...
interface IReadOnlyPair<out T>
{
  T First { get; }
  T Second { get; }
}
```

通过 `out` 修改 `IReadOnlyPair<out T>` 接口上的类型参数，将导致编译器验证 T 确实仅用于“输出”——方法返回类型和只读属性返回类型——而绝不用于形式参数或属性设置器。从此以后，编译器将允许涉及该接口的任何协变转换成功。当对列表 12.42 中的代码进行此修改时，它将成功编译并执行。

对协变转换施加了几个重要限制：

-   只有泛型接口和泛型委托（在第 13 章中描述）可以是协变的。泛型类和结构体永远不是协变的。

-   源和目标泛型类型的可变类型实参必须是引用类型，而不是值类型。也就是说，`IReadOnlyPair<string>` 可以协变地转换为 `IReadOnlyPair<object>`，因为 `string` 和 `IReadOnlyPair<object>` 都是引用类型。`IReadOnlyPair<int>` 不能转换为 `IReadOnlyPair<object>`，因为 `int` 不是引用类型。

![](img/ef6a8a417630b222bfb3f3b949facff0_563_0.png)

![](img/ef6a8a417630b222bfb3f3b949facff0_563_1.png)

