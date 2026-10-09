

// 步骤 2：检查 ReferenceEquals，如果
// 这是一个引用类型
// if (ReferenceEquals(this, obj))
// {
//	return true;
// }
//
// 步骤 4：可能检查等价的哈希码
// if (this.GetHashCode() != obj.GetHashCode())
// {
//	return false;
// }
//
// 步骤 5：检查 base.Equals，如果基类重写了 Equals()
// System.Diagnostics.Debug.Assert(
//	base.GetType() != typeof(object));
// if ( !base.Equals(obj) )
// {
//	return false;
// }
//
// 步骤 6：使用 Longitude 上的 Equals 重载
// 比较标识字段的相等性
return ( Longitude.Equals(obj.Longitude) &&
	Latitude.Equals(obj.Latitude) );

// 步骤 7：重写 GetHashCode
public override int GetHashCode()
{
	int hashCode = Longitude.GetHashCode();
	hashCode ^= Latitude.GetHashCode(); // 异或 (Xor, eXclusive OR)
	return hashCode;
}
}
```

在此实现中，前两个检查相对直观。然而，值得一提的是，如果该类型是密封类，则可以避免步骤 3。

步骤 4 到 6 发生在接受 Coordinate 数据类型的 Equals() 重载中。这样，两个 Coordinate 的比较将完全避免使用 Equals(object obj) 及其 GetType() 检查。

由于 GetHashCode() 未被缓存，且效率并不比步骤 5 高，因此 GetHashCode() 的比较被注释掉了。同样，base.Equals() 也未被使用，因为基类并未重写 Equals()。（该断言检查 base 不是 object 类型，但并未验证基类是否重写了 Equals()，这是正确调用 base.Equals() 所必需的。无论如何，由于 GetHashCode() 不一定返回唯一值（它仅用于标识操作数是否不同），因此单凭它无法确定性地识别相等的对象。）

与 GetHashCode() 类似，Equals() 绝不应该抛出任何异常。任何对象都可以与任何其他对象进行比较，这样做绝不应导致异常。

### 准则
- 应同时实现 GetHashCode()、Equals()、== 运算符和 != 运算符，而不能只实现其中某一个而忽略其他三个。
- 在实现 Equals()、== 和 != 时，请使用相同的算法。
- 避免在 GetHashCode()、Equals()、== 和 != 的实现中抛出异常。
- 避免对可变引用类型进行相等性运算符重载，或者当实现会显著更慢时。
- 在实现 IComparable 时，应实现所有与相等性相关的方法。

## 使用元组重写 GetHashCode() 和 Equals()

如前面两节所示，Equals() 和 GetHashCode() 的实现相当复杂，但实际代码通常是样板代码。对于 Equals()，需要在避免无限递归或空引用异常的同时比较所有包含的标识数据结构。对于 GetHashCode()，需要通过异或操作组合每个非空标识数据结构的唯一哈希码。使用 C# 7.0 元组，结果证明这非常简单。

对于 Equals(Coordinate coordinate)，你可以将每个标识成员分组到一个元组中，并将它们与同类型的目标参数进行比较：

```csharp
public bool Equals(Coordinate coordinate) =>
    return (Longitude, Latitude).Equals(
        (coordinate.Longitude, coordinate.Latitude));
```

（有人可能会认为，如果显式比较每个标识成员会更易读，但我留给读者自行判断）。内部元组 (System.ValueTuple<...>) 使用 EqualityComparer<T>，这依赖于类型参数的 IEquatable<T> 实现（其中只包含一个 Equals<T>(T other) 成员）。因此，为了正确重写 Equals，你需要遵循准则：在重写 Equals() 时实现 IEquatable<T>。这样，你自己的自定义数据类型将利用你自定义的 Equals() 实现，而不是 Object.Equals()。

两个重载中更具说服力的可能是 GetHashCode() 及其元组的使用。而不是参与对非空标识成员进行复杂异或操作，你可以简单地实例化一个包含所有标识成员的元组，并返回该元组的 GetHashCode() 值，如下所示：

```csharp
public override int GetHashCode() =>
return (Radius, StartAngle, SweepAngle).GetHashCode();
```

请注意，在 C# 7.3 中，元组现在实现了 == 和 !=，这应该是其在最初实现时就应具备的特性，这是我们要在下一节中研究的主题。

## 运算符重载

前一节介绍了重写 Equals()，并提供了该类型也应实现 == 和 != 的准则。实现任何运算符称为运算符重载。本节描述了如何执行这种重载，不仅针对 == 和 !=，还包括其他受支持的运算符。

例如，string 提供了一个连接两个字符串的 + 运算符。这也许并不令人惊讶，因为 string 是预定义类型，所以可能具有特殊的编译器支持。然而，C# 允许为类或结构体添加 + 运算符支持。实际上，除了 x.y、f(x)、new、typeof、default、checked、unchecked、delegate、is、as、= 和 => 之外，所有运算符都受支持。其中一个特别值得注意的无法实现的运算符是赋值运算符；没有办法改变 = 运算符的行为。

在执行实现运算符重载的练习之前，请考虑这样一个事实：这类运算符无法通过 IntelliSense 发现。除非意图是让类型表现得像基本类型（例如，数值类型），否则应避免重载运算符。

## 比较运算符 (==, !=, <, >, <=, >=)

一旦重写了 Equals()，就可能存在不一致性。也就是说，两个对象可能为 Equals() 返回 true，但为 == 运算符返回 false，因为 == 默认执行引用相等性检查。为了纠正这个缺陷，重写等于 (==) 和不等于 (!=) 运算符也很重要。

在大多数情况下，这些运算符的实现可以将逻辑委托给 Equals()，或者反之。然而，对于引用类型，首先需要进行一些初始的空值检查（参见列表 10.6）。

### 列表 10.6：实现 == 和 != 运算符

```csharp
public sealed class ProductSerialNumber
{
    // ...

    public static bool operator ==(
        ProductSerialNumber leftHandSide,
        ProductSerialNumber rightHandSide)
    {
        // 检查 leftHandSide 是否为 null
        // (operator== 将是递归的)
        if(ReferenceEquals(leftHandSide, null))
        {
            // 如果 rightHandSide 也是 null 则返回 true，否则返回 false
            return ReferenceEquals(rightHandSide, null);
        }
        
        return (leftHandSide.Equals(rightHandSide));
    }

    public static bool operator !=(
        ProductSerialNumber leftHandSide,
        ProductSerialNumber rightHandSide)
    {
        return !(leftHandSide == rightHandSide);
    }
}
```

请注意，在此示例中，我们使用 ProductSerialNumber 而不是 Coordinate 来演示引用类型的逻辑，引用类型具有空值的额外复杂性。

请务必避免在相等性运算符 (leftHandSide == null) 中使用空值检查。这样做会递归地调用回该方法，导致循环持续直到堆栈溢出。为避免此问题，可以调用 ReferenceEquals() 来检查空值。

**准则**

- 避免在 == 运算符重载的实现中使用相等性比较运算符 (`==`)。

## 二进制运算符 (\\*, -, \\*, /, %, &, |, ^, <<, >>)

你可以将 Arc 添加到 Coordinate 中。然而，迄今为止的代码并未提供加法运算符支持。相反，你需要定义这样一个方法，如列表 10.7 所示。

### 列表 10.7：添加运算符

```csharp
struct Arc
{
    public Arc(
        Longitude longitudeDifference,
        Latitude latitudeDifference)
    {
        LongitudeDifference = longitudeDifference;
        LatitudeDifference = latitudeDifference;
    }

    public Longitude LongitudeDifference { get; }
    public Latitude LatitudeDifference { get; }
}

struct Coordinate
{
    // ...
    public static Coordinate operator +(
        Coordinate source, Arc arc)
    {
        Coordinate result = new Coordinate(
            new Longitude(
                source.Longitude + arc.LongitudeDifference),
            new Latitude(
                source.Latitude + arc.LatitudeDifference));
        return result;
    }
}
```

\\*, -, \\*, /, %, &, |, ^, << 和 >> 运算符实现为二进制静态方法，其中至少一个参数是包含类型。方法名称是运算符加上 *operator* 关键字作为前缀。如列表 10.8 所示，给定

