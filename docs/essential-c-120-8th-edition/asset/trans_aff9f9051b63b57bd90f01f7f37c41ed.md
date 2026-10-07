

# 引用相等与值相等

在考虑示例之前，让我们先考虑为什么我们最初需要实现基于值的相等性（简称为“值相等”）。如果两个引用指向同一个对象实例，则它们是相同的（**引用相等**）。另一方面，具有相同值的对象是**值相等**的。而且，为了支持值相等，一个类型需要实现基于值的相等性。两个引用相等的对象也是值相等的——这种比较是针对同一个对象的两个引用进行的。然而，如果两个对象之间的（相关）数据也相等，那么这两个对象就可以值相等。只有引用类型可以是引用相等的，从而支持了“身份”的概念——即两个引用指向同一个实例。

相比之下，值类型永远不会引用相等。如果你比较 42 是否等于 42，答案始终是 `false`。每个值类型都存储在内存中不同的位置（引用）上，即使是将值类型传递给方法进行比较的简单操作，也会创建值类型的额外副本。

```
在值类型上调用 ReferenceEquals() 将始终返回 false。
```

虽然值类型永远不会引用相等，但引用类型可以支持值相等。`object` 包含一个名为 `ReferenceEquals()` 的静态方法，用于检查两个参数是否相同——引用相等。此外，`object` 定义了一个虚拟的 `Equals()` 方法，默认情况下，它对引用类型依赖于 `ReferenceEquals()`。然而，此 `Equals()` 方法可以被自定义（在引用类型和值类型上都是如此），以便它们实现值相等而不是引用相等。

事实上，你应该始终在值类型上重写 `Equals()`，否则你将只剩下默认实现，该实现只比较第一个字段来判断值相等。然而，这是不够的。例如，如果一个值类型有三个属性，那么通过只比较第一个属性来检查值相等可能是不充分的。例如，给定一个 `Angle` 对象，比较第一个属性（Degrees）是不充分的。

# 第 9 章：引入结构体（Structs）和记录（Records）

只有当度、分和秒都相等（以及 Angle 包含的任何其他属性相等）时，两个 Angles 才相等。因此，在值类型上提供值相等的自定义实现几乎总是必要的。

然而，值相等并不限于值类型。在引用类型上，值类型相等也可能有意义。`string` 是一个很好的例子。虽然 `string` 是引用类型，但如果字符串中的所有字母都相同，那么两个字符串的比较应该是相等的，即使这两个字符串是不同的实例。

此外，正确重写 `Equals()` 需要许多额外的成员存在并可能被重写，这些将在后文的章节“[实现值相等性](https://essentialsharp.com/implementing-value-equality)”中描述。这些成员包括 `GetHashCode()` 以及 `==` 和 `!=` 运算符。在此之前，让我们深入了解什么是值类型。

> 注意：`object.Equals()` 的实现（重写之前所有对象上的默认实现）仅依赖于 `ReferenceEquals()`。所有值类型都重写了默认实现，转而比较值类型内部的一个或多个值。引用类型可以选择地也重写 `Equals()` 以支持值相等。在自定义值类型上实现相等性总是必要的。

# 结构体 (Structs)

C# 的内置类型如 `bool` 和 `int` 都是值类型，`string` 和 `object` 除外，它们是引用类型。框架提供了许多额外的值类型。开发者也可以定义自己的值类型。

要定义自定义值类型，你使用的语法类似于定义类和接口类型时使用的语法。语法上的关键区别是值类型使用 `struct` 关键字（列表 9.1）。

遗憾的是，注释的省略号代表了大量的复杂性，正如我们在本章稍后将看到的 true。

# 列表 9.1：示例结构体

```csharp
public struct Angle
{
    // ...
}
```

# 声明记录结构体 (Record Struct)

幸运的是，从 C# 9.0 开始，创建结构体相关的许多复杂性通过一个新的上下文关键字——`record` 被消除了，该关键字触发编译器生成许多与值类型行为相关的重要且复杂的代码。学习 9.2 节提供了一个示例。通过这种简单的语法，我们有了一个用度、分、秒描述高精度角度的值类型。（一个*分*是1度的六十分分之一，一个*秒*是分钟的六分之一。）这个系统被用于导航，因为它有一个很棒的属性：赤道面上1分钟的弧长恰好是一个**海里。

# 列表 9.2：声明结构体

```csharp
// 使用 record struct 构造函数声明一个值类型
public readonly record struct Angle(
    int Degrees, int Minutes, string? Name = null);
```

这种使用主构造函数的语法是定义整个类型所需的全部。然而，与第 6 节解释的普通主构造函数（且直到 C# 12.0 才能可用）不同，记录的主构造函数还会从属性（可选的¹）位置参数生成一组初始属性。因此，这种简单的代码结构被称为 **record struct**，它具有了构建值类型所需的所有要求，包括值声明、使用属性进行数据存储、不可变性、构造函数初始化、解构、等效性行为，甚至是 `toString()` 诊断功能。

+ 1. 位置参数以及它们周围的括号（当没有位置参数时）都是可选的。虽然只用括号进行声明可能很奇怪，因为这样做等同于声明一个空结构体或类。

# 第 9 章：引入结构体和记录

你会注意到列表 9.2 中，既有基于位置参数生成的构造函数，也有基于位置参数的解构函数（deconstructor）。这在定义的相同的属性（未显示）之外。此外，如果属性等效，则两个 Angle 实例将对评估为相等，这种等效性是根据重写相等运算符的指南实现的。

列表 9.3：使用记录结构体

```csharp
using System;
using System.Diagnostics;

public class Program
{
    public static void Main()
    {
        // 使用位置参数生成构造函数
        (int degrees, minutes, seconds) = (90, 0, 0);
        Angle angle = new(degrees, minutes, seconds);

        // 记录包含了 ToString() 实现
        // 返回："Angle = 90, Minutes = 0, Seconds = 0"
        Console.WriteLine(angle.ToString());

        // 记录拥有一个使用位置参数的解构函数
        if (angle is (int, int, int) angleData)
        {
            Trace.Assert(angle.Degrees == angleData.Degrees);
            Trace.Assert(angle.Minutes == angleData.Minutes);
            Trace.Assert(angle.Seconds == angleData.Seconds);
        }

        Angle copy = new(degrees, minutes, seconds);
        // 记录提供了自定义相等运算符
        Trace.Assert(angle == copy);

        // with 运算符具有对象初始化
        // 用于实例化一个修改后的副本。
        copy = angle with {};
        Trace.Assert(angle == copy);

        Angle modifiedCopy = angle with { Degrees = 180 };
        Trace.Assert(angle != modifiedCopy);
    }
}
```

# 记录结构体代码生成

记录结构体的所有功能由 C# 编译器在编译时生成。C# 等效代码见列表 9.4。

列表 9.4：等效记录结构体 C# 代码

```csharp
using System;
using System.Runtime.CompilerServices;
using System.Text;

[CompilerGenerated]
public readonly struct Angle : IEquatable<Angle>
{
    public int Degrees { get; init; }
    public int Minutes { get; init; }
    public int Seconds { get; init; }
    public string? Name { get; init; }
    public Angle(int Degrees, int Minutes, int Seconds, string? Name)
    {
        this.Degrees = Degrees;
        this.Minutes = Minutes;
        this.Seconds = Seconds;
        this.Name = Name;
    }

    public override string ToString()
    {
        StringBuilder stringBuilder = new();
        stringBuilder.Append("Angle");
        stringBuilder.Append("{ ");
        if (PrintMembers(stringBuilder))
        {
            stringBuilder.Append('\'');
        }
        stringBuilder.Append("}");
        return stringBuilder.ToString();
    }
}
```

