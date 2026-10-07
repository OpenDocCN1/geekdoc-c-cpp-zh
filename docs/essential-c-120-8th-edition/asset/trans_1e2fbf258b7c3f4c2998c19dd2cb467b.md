

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
        + EqualityComparer<string>.Default.GetHashCode(Name!);
}
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

从示例 9.1 中的代码行来看，示例 9.3 显示生成了大量的代码。首先，`Angle` 不再是一个类（class），而是一个结构体（struct），且 `record` 上下文关键字被删除。在 C# 中，要定义自定义值类型必须是结构体。虽然 C# 允许你像示例 9.3 所示从零开始编写整个结构体，但 C# 9.0 的 `record` 关键字启动了许多样板代码（boilerplate code），使得我们不再有理由使用 `record` 关键字来开始编写，特别是因为你可以定义所有生成代码的自定义版本，根据需要覆盖默认的生成实现。

注意，在 C# 9.0 中，不带 `struct` 关键字的 `record` 关键字是编译器允许的。然而，在 C# 10.0 中（引入了用于结构体的记录类型），添加了 `record class` 的显式声明。为了清晰起见，我们建议始终使用 `record class`，而不是简化的仅限 `record` 的语法。

![](img/ffe0f34eac7523830420733690014d17_533_0.png)

# 指南

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

