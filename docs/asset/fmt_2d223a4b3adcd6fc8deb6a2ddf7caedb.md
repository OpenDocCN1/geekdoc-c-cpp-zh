
```
+ EqualityComparer<string>.Default.GetHashCode(Name!);
```
```
```csharp
public override bool Equals(object obj) =>
    obj is Angle angle && Equals(angle);
```
```csharp
public bool Equals(Angle other) =>
    EqualityComparer<int>.Default.Equals(Degrees, other.Degrees)
    && EqualityComparer<int>.Default.Equals(Minutes, other.Minutes)
    && EqualityComparer<int>.Default.Equals(Seconds, other.Seconds)
    && EqualityComparer<string>.Default.Equals(Name, other.Name);
```
```csharp
public void Deconstruct(out int Degrees, out int Minutes,
    out int Seconds, out string Name) =
    => (Degrees, Minutes, Seconds, Name)
    (this.Degrees, this.Minutes, this.Seconds, this.Name);
```

# 结构体 499

从示例 9.1 中的代码行来看，示例 9.3 显示生成了大量的代码。首先，`Angle` 不再是一个类（`class`），而是一个结构体（`struct`），且 `record` 上下文关键字被删除。在 C# 中，要定义自定义值类型必须是结构体。虽然 C# 允许你像示例 9.3 所示从零开始编写整个结构体，但 C# 9.0 的 `record` 关键字启动了许多样板代码（`boilerplate code`），使得我们不再有理由使用 `record` 关键字来开始编写，特别是因为你可以定义所有生成代码的自定义版本，根据需要覆盖默认的生成实现。

注意，在 C# 9.0 中，不带 `struct` 关键字的 `record` 关键字是编译器允许的。然而，在 C# 10.0 中（引入了用于结构体的记录类型），添加了 `record class` 的显式声明。为了清晰起见，我们建议始终使用 `record class`，而不是简化的仅限 `record` 的语法。

![](img/ffe0f34eac7523830420733690014d17_533_0.png)

## 指南

- 在声明结构体时，请使用 `record struct` (C# 10.0)。
- 为了清晰起见，请使用 `record class` (C# 10.0)，而不是简化的仅限 `record` 的语法。

所有值类型都是隐式密封的（你不能从它们派生）。此外，所有非枚举值类型（枚举将在本章稍后讨论）都派自 `System.ValueType`。因此，结构体的 `ValueType` 链始终是从 `object` 到 `System.ValueType` 再到自定义结构体。

`System.ValueType` 通过重写 `object` 的所有虚方法（如 `Equals()`、`ToString()` 和 `GetHashCode()`）引入了值类型的行为。然而，这种实现通常是不够的，需要开发者负责对这些方法中的每一个进行进一步专门化——当然，这直到 C# 10.0 引入 `record` 修饰符为止，现在 C# 编译器会生成更适合生产代码的自定义覆盖。许多相同的功能在类中也同样可用。

# 记录类（Record Classes）

此外，`record` 修饰符不仅限于创建值类型。从 C# 9.0 开始，增加了对记录类的支持，如示例 9.5 所示。

示例 9.5：声明一个记录类

```csharp
// 使用 record class 构造声明一个引用类型
public record class Coordinate(
    Angle Longitude, Angle Latitude)
```

在这个记录类中，我们使用 `Angle` 类型作为位置参数传入 `Coordinate`，以表示经度和纬度。

为了将记录结构体和记录类与它们的非记录版本区分开，我们将在本章将其称为标准结构体和标准类。`record class` 特性引入的最关键问题之一是：何时使用 `record class` 而不是标准类，反之亦然？关键且可能也是定义 `record class` 的唯一原因在于，如果该类型需要具有值相等性（value equality）。事实上，每当自定义类型需要实现值相等性时（对于值类型始终如此），应尽可能使用 `record` 构造。可能无法实现的示例是在是在 C# 9.0 之前的版本中工作（对于值类型）。

另一种无法在类上使用 `record` 构造的情况是基类不是记录类。`record class` 只能继承自另一个 `record class`，而标准类只能继承自另一个标准类。继承链不能在标准类和记录类型之间混合使用。

> 注意
> 引用类型默认应实现为标准类，只有在需要值相等性实现时才实现为记录类。

许多与 `record struct` 相关的特性也用于 `record class`，包括简洁的声明、带属性的数据存储、构造函数初始化、解构、`ToString()` 诊断能力，以及最重要的（由于其复杂性）值相等性，而不仅仅是引用相等性。生成的等效记录类 C# 代码见示例 9.6。

**示例 9.6：** 等效记录类 – 生成的 C# 代码

```csharp
using System.Runtime.CompilerServices;
using System.Text;

[CompilerGenerated]
public class Coordinate : IEquatable<Coordinate>
{
    public Angle Longitude { get; init; }
    public Angle Latitude { get; init; }
    public Coordinate(Angle Longitude, Angle Latitude) : base()
    {
        this.Longitude = Longitude;
        this.Latitude = Latitude;
    }
    public override string ToString()
    {
        StringBuilder stringBuilder = new();
        stringBuilder.Append("Coordinate");
        if (PrintMembers(stringBuilder))
        {
            stringBuilder.Append(' ');
        }
        stringBuilder.Append("}");
        return stringBuilder.ToString();
    }
    protected virtual bool PrintMembers(StringBuilder builder)
    {
        RuntimeHelpers.EnsureExecutionStack();
        builder.Append("Longitude = ");
        builder.Append(Longitude.ToString());
        builder.Append(", Latitude = ");
        builder.Append(Latitude.ToString());
        return true;
    }
    public override int GetHashCode()
    {
        static int GetHashCode(Angle angle) =>
            EqualityComparer<Angle>.Default.GetHashCode(angle);
        return (EqualityComparer<Type>.Default.GetHashCode(
            EqualityContract()) * -1521134295
        * GetHashCode(Longitude)) * -1521134295
        * GetHashCode(Latitude);
    }
    public override bool Equals(object obj) =>
        Equals(obj as Coordinate);
    public virtual bool Equals(Coordinate? other) =>
        (object)this == other || (other is not null)
        && EqualityContract() == other!.EqualityContract()
        && EqualityComparer<Angle>.Default.Equals(
            Longitude, other!.Longitude)
        && EqualityComparer<Angle>.Default.Equals(
            Latitude, other!.Latitude);
    }
    public void Deconstruct(
        out Angle Longitude, out Angle Latitude)
    {
        Longitude = this.Longitude;
        Latitude = this.Latitude;
    }
    protected virtual Type EqualityContract() => typeof(Coordinate);
    public Type ExternalEqualityContract => EqualityContract();
    // Actual name in IL is "<Clone>$". However,
    // you can't add a Clone method to a record.
    public Coordinate Clone() => new(this);
    protected Coordinate(Coordinate original)
    {
        Longitude = original.Longitude;
        Latitude = original.Latitude;
    }
}
```

502 第 9 章：结构体（Structs）与记录（Records）

```csharp
public static bool operator !==(Coordinate? left, Coordinate? right) =>
!(left == right);
public static bool operator ==(
    Coordinate left, Coordinate? right) =>
    ReferenceEquals(left, right) ||
    (left?.Equals(right) != false);
```

```c
Latitude = original.Latitude;
}
```

在 `record struct` 与 `record class` 生成的代码之间存在几处预期的差异。

首先，几个成员被标记了 `virtual` 修饰符（`PrintMembers(StringBuilder builder)`、`Equals(Coordinate? Other)` 和 `EqualityContract()`）。`record struct` 永远未使用 `virtual`，因为它们都是密封的（`sealed`），这使得在 record 的情况下使用 `virtual` 没有意义。

其次，`record class` 需要考虑空值的可能。因此，`Equals()`、`==` 运算符以及两个 `Equals()` 方法都需要检查参数值是否为空。

在接下来的章节中，我们将详细探索记录；我们将讨论每个特性、值得注意的实现方式，以及 `record struct` 与 `record class` 实现之间的独特差异。

| 指南 |
| :--- |
| 如果你想根据数据而非标识进行等效性比较，请尽可能使用 records。 |

# 记录类继承 (Record Class Inheritance)

虽然 `record struct` 由于是密封的而不支持继承，但 `record class` 支持继承。主要的限制是 `record class` 只能继承自其他 `record class`，甚至不能继承自标准类。列表 9.7 提供了一个示例。

+ 列表 9.7：记录类继承

```csharp
public record class NamedCoordinate(
    Angle Longitude, Angle Latitude, string Name)
```

# 第 9 章：介绍结构体和记录

Coordinate(Longitude, Latitude);

注意，在定义继承关系时，你也可以通过基类名称后的参数来识别如何带参数调用基构造函数。在这种情况下，我们将 `Longitude` 和 `Latitude` 传递给 `Coordinate` 的由位置参数生成的构造函数。

# 记录 (Records)

在本节中，我们将深入研究记录背后的代码细节，突出 `record class` 与 `record struct` 之间的差异，最重要的是，挖掘值等效性的实现细节。我们从记录的数据存储开始讨论。

# 使用属性的数据存储 (Data Storage with Properties)

注意位置参数 `Degree`、`Minutes` 和 `Seconds` 如何映射到 `Angle` 结构体上自动生成的属性。`Coordinate` 上的 `Longitude` 和 `Latitude` 也是如此。一旦初始化完成，属性是只读的（具有 `init-only` 设置器）。属性只读是 `record class` 的默认行为，或者是由 `record struct` 声明上的 `readonly` 修饰符引起的——该修饰符导致值类型在初始化完成之前是不可变的。

记录的一个特殊之处在于，按照惯例，位置参数是 `PascalCase`（帕斯卡命名法），因此它们是构造函数的参数。虽然编译器没有要求，但对位置参数使用 `PascalCase` 可以确保相应的属性也具有 `PascalCase`——后者是类型 API 中更可见的部分。

要自定义默认实现，你可以使用相同的名称为每个属性定义自己的版本——也许可能使用备用字段和自定义验证。你甚至可以将属性替换为同名的字段。此外，如果它们没有作为位置参数包含，你还可以添加额外的属性和字段。唯一的限制是，由于结构体的 `readonly` 修饰符，所有属性和字段也必须是只读的。

注意，生成的属性没有与任何验证逻辑相关。因此，非可空引用类型的位置参数将包含空检查。由于由于原因，请考虑始终将引用类型位置参数定义为可空，除非你提供了检查空值的自定义实现。

# 指南 (Guidelines)

- **对记录的位置参数使用 PascalCase (C# 9.0)。**
- **如果不提供检查空值的自定义属性实现，请将所有引用类型位置参数都定义为可空。**
- **为所有非可空位置参数实现自定义的非可空属性。**

# 不可变值类型 (Immutable Value Types)

一个重要的指南是所有值类型和 `record class` 都应该是不可变的：一旦你实例化了其中任何一个，就不应该能够修改同一个实例。该指南有三个充分的。

首先，对于结构体（structs），值类型应该表示值。人们不会将两个整数相加看作是对其中任何一个的修改；相反，两个加数是不可变的，产生第三个值作为结果。其次，因为值类型是通过值复制而非引用复制的，很容易产生混淆并错误地认为一个值类型变量的变异可以观察到导致另一个变量的变异，就像引用类型那样。

第三，对于结构体和 `record class`，事实是哈希值是根据类型内部存储的数据计算的，且哈希值永远不应该改变。（参见本章节后部分的“高级主题：重写 GetHashCode()”）。如果这些类型内部的数据发生变化并计算出新的哈希值，在存在旧哈希值的集合中搜索新的哈希值可能会导致值永远无法找到，并产生错误的行为。

# 第 9 章：介绍结构体和记录

注意列表 9.3 中的 `Angle` 结构体是不可变的，因为所有属性都是自动实现的、使用 `init-only` 设置器而非 `set` 声明的只读属性。为了验证是否符合不可变指南，你可以在结构体定义中使用 `readonly` 修饰符 `³`（同时适用于 `record struct` 和标准结构体）。请参见列表 9.8。

# 列表 9.8：在结构体上使用只读修饰符

```csharp
readonly struct Angle { }
```
