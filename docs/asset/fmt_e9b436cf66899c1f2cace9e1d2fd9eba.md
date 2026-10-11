
| | |
|---|---|
| int number1 | 42 |
| char letter | 'A' |
| float pi | 3.14F |
| int number2 | 42 |

![](img/ffe0f34eac7523830420733690014d17_523_0.png)

图 9.1：值类型直接包含数据

值类型变量就像一张写有数字的纸。如果你想更改该数字，可以擦掉它并替换为另一个数字。如果你有第二张纸，你可以从第一张纸上复制该数字，但这两张纸随后就是相互独立的；在其中一张纸上擦除并替换数字不会影响另一张。

同样，将值类型的实例传递给如 `Console.WriteLine()` 等方法也会导致从与参数关联的存储位置进行内存复制，方法内部对参数变量的任何更改都不会影响调用者中的原始值。由于值类型需要复制，它们通常应该定义为消耗少量的内存（通常为 16 字节或少）。

> 指南
> 避免创建消耗超过 16 字节内存的值类型。

值类型的值通常是短命的；在许多情况下，一个值只需要表达式的一部分或用于方法的激活。在这些情况下，值类型的变量和临时值通常可以存储在称为“栈（`stack`）”的临时存储池中。（这个术语实际上是一个误称：它并不要求临时池在栈之外分配其存储空间。事实上上，作为一种实现细节，它经常选择从可用寄存器中分配存储空间。）

临时池的清理成本比垃圾回收堆（`heap`）低。然而，值类型的复制频率通常比引用类型高，这种复制可能会产生自身的性能开销。不要掉入“由于值类型可以分配在栈上，因此速度更快”的陷阱。

## 引用类型

相比之下，引用类型变量的值是指向对象实例的引用（见图 9.2）。引用类型变量存储的是对象实例数据所在位置引用（通常实现为内存地址），而不是直接存储数据（像值类型变量那样）。因此，为了访问数据，运行时从变量中读取引用，然后对其进行解引用（dereference），以到达实际包含实例数据的内存位置。

## 第9 章：介绍结构体和记录

```
int number1 = 42;

char letter = 'A';

float pi = 3.14F;

int number2 = number1;
```

值类型变量就像一张写有数字的纸。如果你想更改该数字，可以擦掉它并替换为另一个数字。如果你有第二张纸，你可以从第一张纸上复制该数字，但这两张纸随后就是相互独立的；在其中一张纸上擦除并替换数字不会影响另一张。

同样，将值类型的实例传递给如 `Console.WriteLine()` 等方法也会导致从与参数关联的存储位置进行内存复制，方法内部对参数变量的任何更改都不会影响调用者中的原始值。由于值类型需要复制，它们通常应该定义为消耗少量的内存（通常为 16 字节或少）。

> 指南
> 避免创建消耗超过 16 字节内存的值类型。

值类型的值通常是短命的；在许多情况下，一个值只需要表达式的一部分或用于方法的激活。在这些情况下，值类型的变量和临时值通常可以存储在称为“栈（`stack`）”的临时存储池中。（这个术语实际上是一个误称：它并不要求临时池在栈之外分配其存储空间。事实上，作为一种实现细节，它经常选择从可用寄存器中分配存储空间。）

临时池的清理成本比垃圾回收堆（`heap`）低。然而，值类型的复制频率通常比引用类型高，这种复制可能会产生自身的性能开销。不要掉入“由于值类型可以分配在栈上，因此速度更快”的陷阱。

相比之下，引用类型变量的值是指向对象实例的引用（见图 9.2）。引用类型变量存储的是对象实例数据所在位置引用（通常实现为内存地址），而不是直接存储数据（像值类型变量那样）。因此，为了访问数据，运行时从变量中读取引用，然后对其进行解引用，以到达实际包含实例数据的内存位置。

引用类型变量就像一张写有地址的纸。如果你想更改地址，可以擦掉它并替换为另一个地址。如果你有第二张纸，你可以从第一张纸上复制该地址，但这两张纸随后就是相互独立的；在其中一张纸上擦除并替换地址不会影响另一张。

同样，将引用类型的实例传递给如 `Console.WriteLine()` 等方法也会导致从与参数关联的存储位置进行内存复制，方法内部对参数变量的任何更改都不会影响调用者中的值。然而，如果方法更改了引用指向的对象，这种更改将被调用者观察到。由于引用类型只复制引用，它们通常应该定义为消耗少量的内存（通常为 16 字节或少）。

引用类型的值通常是短命的；在许多情况下，一个值只需要表达式的一部分或用于方法的激活。在这些情况下，引用类型的变量和临时值通常可以存储在称为“栈（`stack`）”的临时存储池中。（这个术语实际上是一个误称：它并不要求临时池在栈之外分配其存储空间。事实上，作为一种实现细节，它经常选择从可用寄存器中分配存储空间。）

临时池的清理成本比垃圾回收堆（`heap`）低。然而，引用类型的复制频率通常比值类型高，这种复制可能会产生自身的性能开销。不要掉入“由于引用类型可以分配在栈上，因此速度更快”的陷阱。

图 9.2：引用类型指向堆

引用类型变量就像一张写有地址的纸。如果你想更改地址，可以擦掉它并替换为另一个地址。如果你有第二张纸，你可以从第一张纸上复制该地址，但这两张纸随后就是相互独立的；在其中一张纸上擦除并替换地址不会影响另一张。

由于引用类型只复制指向数据的引用，两个不同的变量可以引用相同的数据。在这种情况下，通过一个变量更改数据将被观察到也更改另一个变量的数据。这在赋值和方法调用中都会发生。

继续我们之前的类比，如果你将建筑的地址传递给一个方法，你复制包含引用的纸并将副本交给该方法。方法无法更改原始纸的内容以指向另一个建筑。假设方法漆了所引用的建筑。那么，当方法返回时，调用者可以观察到调用者仍然引用的建筑现在变了颜色。

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

# 列表 9.3：使用记录结构体

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

# 列表 9.4：等效记录结构体 C# 代码

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

# 498 第 9 章：结构体（Structs）与记录（Records）

```csharp
private bool PrintMembers(StringBuilder builder)
{
    builder.Append("Degrees = ");
    builder.Append(Degrees);
    builder.Append(", Minutes = ");
    builder.Append(Minutes);
    builder.Append(", Seconds = ");
    builder.Append(Seconds);
    builder.Append(", Name = ");
    builder.Append(Name);
    return true;
}
```

```csharp
public static bool operator !==(Angle left, Angle right) =>
    !(left == right);
```

```csharp
public static bool operator ==(Angle left, Angle right) =>
    left.Equals(right);
```

```csharp
public override int GetHashCode()
{
    static int GetHashCode(int integer) =>
        Equality<int>.Default.GetHashCode(integer);
    return GetHashCode(Degrees) * -1521134295
        + GetHashCode(Minutes) * -1521134295
        + GetHashCode(Seconds) * -1521134295
```
