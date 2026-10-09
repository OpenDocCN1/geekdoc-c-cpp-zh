
需要注意，基类 `Employee` 既不包含 `Manage()` 方法，也不包含 `Work()` 方法。只有 `Manager` 类型的对象才能使用 `Manage()` 方法，只有 `Worker` 类型的对象才能使用 `Work()` 方法。也就是说，`managerOrg1[0].Manage()` 或 `managerOrg1[0].Work()` 将在构建时导致编译错误。

这种语法避免了我们在进行 `is` 测试后必须进行显式类型转换的需要。

对于 `as` 表达式，我们可以这样做：

```csharp
Console.WriteLine($"{(managerOrg1[0] as Manager)!.Manage()}");
Console.WriteLine($"{(managerOrg1[0] as Worker)?.Work()}");
```

第一个 `WriteLine()` 方法将输出：

```text
I just manage and I get paid 1000000 dollars.
```

另一方面，第二个 `WriteLine()` 方法除了换行符外什么也不输出（因为参数求值结果为空字符串）。

由于 `as` 表达式的结果可能为 `null`，因此我们需要进行空值检查。在此特定情况下，由于我们知道 `managerOrg1[0]` 的运行时类型是 `Manager`（且该表达式不可能产生 `null` 值），我们采取了一点取巧的做法，使用了 `!` 运算符。

这是向编译器发出的明确提示，表示既然我们知道自己在做什么，你可以忽略该表达式的空值检查。（`!` 被称为“空值容忍运算符”或“空值抑制运算符”。）

另一方面，在第二条语句的情况下，我们使用了“空值条件运算符” `?`。只有当 `as` 表达式（位于 `?` 之前）不为 `null` 时，才会调用 `Work()` 方法。如果 `as` 表达式求值为 `null`（因为 `managerOrg1[0]` 无法转换为 `Worker`），则整个表达式 `(managerOrg1[0] as Worker)?.Work()` 的总体值为 `null`。

有一点需要注意，Management 和 RankAndFile 类使用了“集合初始化语法”。例如：

```csharp
var managerOrg1 = new Management("M1") {
    new Manager("M1a"),
    new Manager("M1b"),
};
```

之所以可能这样写，是因为其基类 Organization 继承自集合类型 `List<Employee>`。因此，这些类实际上是通过继承而来的集合类型。

主程序还使用了一种“高阶”方法 `ForEach()`，它是作为 `List<T>` 上的成员方法定义的。

例如：

```csharp
allEmployees.ForEach(e => total1 += e.Salary);
```

`ForEach()` 参数的类型是一个委托。更具体地说，`e => total1 += e.Salary` 是一个“Lambda 表达式”，它是某种委托类型的字面量。

> 在此特定情况下，`ForEach()` 的参数类型为 `Action<Employee>`。来自 system 命名空间的 `Action<T>` 类型封装了一个只有一个参数且不返回值的​​方法。

Lambda 表达式类似于匿名函数。注意其语法。粗箭头（`=>`）前面的变量是参数。如果有多个参数，我们会将它们放在一对括号中。如果只有一个参数，通常省略括号。

粗箭头后面的表达式是函数体，在这种情况下是表达式 `total += e.Salary`。

`ForEach()` 方法会对列表（在此情况下为 `allEmployees`）中的所有元素评估 Lambda 表达式。

该语句实际上等价于以下代码：

```csharp
foreach (var e in allEmployees) {
    total += e.Salary;
}
```

虽然 `ForEach()` 不是 LINQ 方法，但从技术上讲，它遵循了许多 LINQ 方法所遵循的相同模式。我们将在本书后面的章节中展示一些 LINQ 扩展方法的用法示例。

**小测验。** 😃

> 构造方法不能是 `virtual` 的。你认为这是为什么？同样，构造方法也不能是 `abstract` 的。为一个类型拥有 `abstract` 构造方法有意义吗？

## 摘要

我们学习了 C# 中继承的基础知识。类型的虚方法和 `abstract` 方法与属性可以由其子类型（记录类和类）重写。

特别是，我们使用了关键字 `abstract`、`virtual` 和 `override` 等。引用类型（例如类、结构体和接口）的对象在运行时可以表现出多态行为。

我们还涵盖了用于控制类型成员方法和属性访问级别的六个访问修饰符。即 `public`、`internal`、`protected`、`protected internal`、`private protected` 和 `private`。

C# 提供了许多用于检查类型和在不同类型之间强制转换对象的运算符。我们探索了 `is` 和 `as` 运算符的一些基础知识。虽然本课没有涵盖，但 C# 还有一个运算符 `typeof`，用于获取给定类型名称的 `System.Type` 实例。`object.GetType()` 方法（所有对象均可用）也可以用于获取对象的类型。

我们还学习了函数式风格方法（例如 `List<T>.ForEach()`）和 Lambda 表达式的基本用法。`List<T>.ForEach()` 方法以及许多 LINQ 扩展方法都接受一个委托作为其中一个参数。

# 第 23 课：面积与周长

## 23.1. 引言

在本课中，我们将探讨 C# 中接口多重继承是如何工作的。

这一课将是本书中最枯燥的一课。😞 如果你对 C# 语法的所有细微末节不感兴趣，可以跳过这一课。C# 是一门相当复杂的语言，然而，为了熟练掌握它，你至少需要了解某些概念，即使你不必记住所有细节。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_373_0.png)

## 23.2. 代码审查 - 多种形状的面积和周长计算器

让我们从简单的例子开始。C# 中接口（单一）继承是如何工作的？

“接口继承”在这个语境下不是最常用术语。我们更常说一个类“实现”了一个或多个接口等。但是，只要我们清楚这里讨论的是什么，我们使用哪种术语并不是那么关键。

复杂性来源于 C# 给了我们太多的选项。这些选择既是福也是祸。

当我们定义一个接口时，我们可以选择性地为方法或属性提供默认实现。当我们实现接口方法或属性时，类可以显式或隐式地实现该接口方法或属性。等等。

在这种情况下，我们通常会面对所谓的“组合爆炸”。

让我们看一些具体的例子。这是一个简单的接口：

`area-calculation/si1/Area.cs` (第 4-10 行)

```csharp
public interface IArea {
    /// <summary>
    /// Returns the area.
    /// This method needs to be implemented in the concrete types.
    /// </summary>
    float Size();
}
```

我们稍后会详细讨论“XML 文档注释”。目前，接口 `IArea` 声明了一个方法 `float Size()`。这个接口方法是隐式抽象的，并且需要具体类型提供实现。该方法也是隐式公有的。

我们在 `SI1` 命名空间中创建了三个实现这个 `IArea` 接口的类型（尽管代码片段中未明确显示）。

`SI1.ShapeB` 类“隐式”实现了 `Size()` 方法：

`**area-calculation/si1/Shapes.cs**` (第 4-9 行)

```csharp
public class ShapeB : IArea {
    /// <summary>Implicit/normal implementation of
    /// IArea.Size().</summary>
    public float Size() {
        return 5.0f;
    }
}
```

这是实现接口方法或属性最常见且传统的方式。让我们用一个简单的程序来测试它：

```csharp
ShapeB shape1B = new();
var size1B = shape1B.Size();
Console.WriteLine($"size1B = {size1B}");
```

输出如下所示，符合预期：

```text
size1B = 5
```

没什么意外。现在，让我们尝试“显式实现”：

`**area-calculation/si1/Shapes.cs**` (第 12-17 行)

```csharp
public class ShapeC : IArea {
    /// <summary>Explicit implementation of IArea.Size().</summary>
    float IArea.Size() {
        return 10.0f;
    }
}
```
