

在这种实现中，前两个检查相对明显。然而，有趣的是，如果类型是密封的，则可以避免步骤 3。

步骤 4–6 发生在重载的 Equals() 中，该重载专门接受 Coordinate 数据类型。这样，两个 Coordinates 的比较将完全避免 Equals(object obj) 及其 GetType() 检查。

由于 GetHashCode() 未被缓存并且效率也不高于步骤 5，因此 GetHashCode() 比较被注释掉了。同样，base.Equals() 也未使用，因为基类未重写 Equals()。 （断言检查基类不是 object 类型，但并未验证基类是否重写了 Equals()，而这正是适当调用 base.Equals() 所必需的。）无论如何，因为 GetHashCode() 不一定返回唯一值（它只是标识操作数是否不同），因此单独使用它并不能确定地标识相等对象。

与 GetHashCode() 类似，Equals() 绝不应抛出任何异常。比较任何对象与任何其他对象都是有效的，并且这样做绝不应导致异常。

### Guidelines

- **DO** 一起实现 GetHashCode()、Equals()、== 运算符和 != 运算符——不要只实现其中一个而缺少其他三个。
- **DO** 在实现 Equals()、== 和 != 时使用相同的算法。
- **AVOID** 从 GetHashCode()、Equals()、== 和 != 的实现中抛出异常。
- **AVOID** 在可变引用类型上重载相等运算符，或如果实现会显著变慢。
- **DO** 在实现 IComparable 时实现所有与相等相关的方法。

# Operator Overloading

前一节讨论了重写 Equals() 并提供了指导，即类还应实现 == 和 !=。实现任何运算符称为 *operator overloading*。本节描述如何执行此类重载，不仅针对 == 和 !=，还针对其他受支持的运算符。

例如，string 提供了 + 运算符来连接两个字符串。这也许并不令人惊讶，因为 string 是预定义类型，因此可能具有特殊的编译器支持。然而，C# 允许向类或结构体添加 + 运算符支持。事实上，所有运算符都受支持，除了 x.y、f(x)、new、typeof、default、checked、unchecked、delegate、is、as、= 和 =>。一个特别值得注意的无法实现的运算符是赋值运算符；没有办法改变 = 运算符的行为。

在进行运算符重载的练习之前，请考虑这样一个事实：此类运算符无法通过 IntelliSense 发现。除非类型旨在像原始类型（例如数值类型）一样工作，否则应避免重载运算符。

# Comparison Operators (==, !=, <, >, <=, >=)

一旦重写了 Equals()，就可能存在不一致的情况。也就是说，两个对象对于 Equals() 返回 true，但对于 == 运算符返回 false，因为 == 默认执行引用相等检查。为了纠正此缺陷，重要的是也要重载等于 (==) 和不等于 (!=) 运算符。

在大多数情况下，这些运算符的实现可以将逻辑委托给 Equals()，反之亦然。然而，对于引用类型，首先需要进行一些初始空值检查（参见 Listing 9.6）。

# LISTING 9.6: Implementing the == and != Operators

```
public sealed class ProductSerialNumber
{
    // ...

    public static bool operator ==(
        ProductSerialNumber leftHandSide,
        ProductSerialNumber rightHandSide)
    {
        // Check if leftHandSide is null.
        // (operator== would be recursive)
        if(ReferenceEquals(leftHandSide, null))
        {
            // Return true if rightHandSide is also null
            // and false otherwise.
            return ReferenceEquals(rightHandSide, null);
        }
```

```
public Latitude LatitudeDifference { get; }
}

struct Coordinate
{
    // ...
    public static Coordinate operator +(Coordinate source, Arc arc)
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

+, -, *, /, %, &, |, ^, << 和 >> 运算符被实现为二进制静态方法，其中至少一个参数是包含类型的。方法名称是运算符前面加上 operator 作为关键字。如 Listing 9.8 所示，给定 - 和 + 二进制运算符的定义，你可以向坐标添加和减去 Arc。注意 Longitude 和 Latitude 也需要实现 + 运算符，因为它们被 source.Longitude + arc.LongitudeDifference 和 source.Latitude + arc.LatitudeDifference 调用。

# LISTING 9.8: Calling the – and + Binary Operators

```
public class Program
{
    public static void Main()
    {
        Coordinate coordinate1,coordinate2;
        coordinate1 = new Coordinate(
            new Longitude(48, 52), new Latitude(-2, -20));
        Arc arc = new Arc(new Longitude(3), new Latitude(1));

        coordinate2 = coordinate1 + arc;
        Console.WriteLine(coordinate2);

        coordinate2 = coordinate2 - arc;
        Console.WriteLine(coordinate2);

        coordinate2 += arc;
        Console.WriteLine(coordinate2);
    }
}
```

Listing 9.8 的结果显示在 Output 9.3 中。

# OUTPUT 9.3

```
51° 52' 0 E  -1° -20' 0 N
48° 52' 0 E  -2° -20' 0 N
51° 52' 0 E  -1° -20' 0 N
```

对于 Coordinate，你实现 - 和 + 运算符以返回在添加/减去 Arc 后的坐标位置。这允许你将多个运算符和操作数串联起来，如 result = ((coordinate1 + arc1) + arc2) + arc3。此外，通过在 Arc 上支持相同的运算符 (+/-)（参见 Listing 9.9），你可以消除括号。这种方法之所以可行，是因为第一个操作数 (arc1 + arc2) 的结果是另一个 Arc，然后你可以将其添加到下一个 Arc 或 Coordinate 类型的操作数。

相比之下，考虑如果提供一个 - 运算符，其参数为两个 Coordinates 并返回两个坐标之间的距离对应的 double 会发生什么。将 double 添加到 Coordinate 是未定义的，因此你无法串联运算符和操作数。在定义返回不同类型的运算符时应谨慎，因为这样做违反直觉。

# Combining Assignment with Binary Operators
(+=, -=, *=, /=, %=, &=, ...)

如前所述，不支持重载赋值运算符。然而，结合二进制运算符的赋值运算符 (+=, -=, *=, /=, %=, &=, |=, ^=, <<= 和 >>=) 在重载二进制运算符时实际上被重载了。给定不带赋值的二进制运算符的定义，C# 会自动允许与运算符结合使用赋值。 因此，使用 Listing 9.7 中的 Coordinate 定义，你可以有如下代码

```
coordinate += arc;
```

这等价于以下内容：

```
coordinate = coordinate + arc;
```

# Conditional Logical Operators (&&, ||)

与赋值运算符类似，条件逻辑运算符不能显式重载。然而，由于逻辑运算符 & 和 | 可以被重载，并且条件运算符包含逻辑运算符，因此实际上可以重载条件运算符。x && y 被处理为 x & y，其中 y 必须求值为 true。类似地，x || y 被处理为 x | y 仅当 x 为 false 时。为了支持在例如 if 语句中将类型求值为 true 或 false，有必要重写 true/false 一元运算符。

# Unary Operators (+, -, !, ~, ++, --, true, false)

重载一元运算符与重载二进制运算符非常相似，只是它们只接受一个参数，也是包含类型的。Listing 9.9 重载了 Longitude 和 Latitude 的 + 和 – 运算符，然后在 Arc 中重载相同运算符时使用这些运算符。

# LISTING 9.9: Overloading the – and + Unary Operators

```
public struct Latitude
{
    // ...
    public static Latitude operator -(Latitude latitude)
    {
        return new Latitude(-latitude.DecimalDegrees);
    }
    public static Latitude operator +(Latitude latitude)
    {
        return latitude;
    }
}

public struct Longitude
{
    // ...
    public static Longitude operator -(Longitude longitude)
    {
        return new Longitude(-longitude.DecimalDegrees);
    }
    public static Longitude operator +(Longitude longitude)
    {
        return longitude;
    }
}

public struct Arc
```
