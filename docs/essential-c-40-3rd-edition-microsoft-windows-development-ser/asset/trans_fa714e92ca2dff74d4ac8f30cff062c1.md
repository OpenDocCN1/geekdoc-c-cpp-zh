

```
_Longitude = longitude;
    _Latitude = latitude;
}

public Longitude Longitude { get { return _Longitude; } }
private readonly Longitude _Longitude;

public Latitude Latitude { get { return _Latitude; } }
private readonly Latitude _Latitude;

// ...
}
```

```
class Program
{
    public void Main()
    {
        //...

        Coordinate coordinate1 =
            new Coordinate(new Longitude(48, 52),
                new Latitude(-2, -20));

        // Value types will never be reference equal.
        if (Coordinate.ReferenceEquals(coordinate1,
            coordinate1))
        {
            throw new Exception(
                "coordinate1 reference equals coordinate1");
        }

        Console.WriteLine(
            "coordinate1 does NOT reference equal itself");
    }
}
```

与第 8 章中将 Coordinate 定义为引用类型不同，接下来的定义是值类型（struct），因为 Longitude 和 Latitude 数据的组合在逻辑上被视为一个值，且大小小于 16 字节。（在第 8 章中，Coordinate 聚合的是 Angle 而不是 Longitude 和 Latitude。）将 Coordinate 声明为值类型的一个促成因素是，它是一个（复杂的）数值，具有针对它的特定操作。相比之下，像 Employee 这样的引用类型不是你进行数值操作的值，而是指向现实生活中的对象。

## 实现 Equals()

要确定两个对象是否相等（它们具有相同的标识数据），你使用对象的 Equals() 方法。object 上此虚方法的实现使用 ReferenceEquals() 来评估相等性。由于此实现通常不够充分，有时有必要用更合适的实现重写 Equals()。

对于对象相互相等，预期是它们内部的标识数据相等。例如，对于 ProductSerialNumbers，ProductSeries、Model 和 Id 必须相同；然而，对于 Employee 对象，也许比较 EmployeeIds 就足以判断相等性。要纠正 object.Equals() 的实现，有必要重写它。例如，值类型重写 Equals() 实现，以改用类型包含的字段。

重写 Equals() 的步骤如下。

- 1. 检查 null。
- 2. 如果类型是引用类型，检查引用相等性。
- 3. 检查等效类型。
- 4. 调用一个类型化的帮助方法，它可以将操作数视为比较类型而不是对象（参见清单 9.5 中的 Equals(Coordinate obj) 方法）。
- 5. 可能检查等效哈希码以短路广泛的逐字段比较。（两个相等的对象不能有不同的哈希码。）
- 6. 如果基类重写了 Equals()，检查 base.Equals()。
- 7. 比较每个标识字段的相等性。
- 8. 重写 GetHashCode()。
- 9. 重写 == 和 != 运算符（参见下一节）。

清单 9.5 显示了 Equals() 实现的示例。

```
Listing 9.5: Overriding Equals()
public struct Longitude
{
    // ...
}
```

```
public struct Latitude
{
    // ...
}
```

```
public struct Coordinate
{
    public Coordinate(Longitude longitude, Latitude latitude)
    {
        _Longitude = longitude;
        _Latitude = latitude;
    }

    public Longitude Longitude { get { return _Longitude; } }
    private readonly Longitude _Longitude;

    public Latitude Latitude { get { return _Latitude; } }
    private readonly Latitude _Latitude;

    public override bool Equals(object obj)
    {
        // STEP 1: Check for null
        if (obj == null)
        {
            return false;
        }
        // STEP 3: equivalent data types
        if (this.GetType() != obj.GetType())
        {
            return false;
        }
        return Equals((Coordinate)obj);
    }

    public bool Equals(Coordinate obj)
    {
        // STEP 1: Check for null if a reference type
        // (e.g., a reference type)
        // if (obj == null)
        // {
        //     return false;
        // }

        // STEP 2: Check for ReferenceEquals if this
        // is a reference type
        // if (ReferenceEquals(this, obj))
        // {
        //     return true;
        // }
    }
}
```

```
// STEP 4: Possibly check for equivalent hash codes
// if (this.GetHashCode() != obj.GetHashCode())
//     return false;
// }

// STEP 5: Check base.Equals if base overrides Equals()
// System.Diagnostics.Debug.Assert(
//     Base.GetType() == typeof(object));
// if ( !base.Equals(obj) )
//     return false;
// }

// STEP 6: Compare identifying fields for equality
// return ( (Longitude.Equals(obj.Longitude) &&
//     (Latitude.Equals(obj.Latitude)) );
}

// STEP 7: Override GetHashCode.
public override int GetHashCode()
{
    int hashCode = Longitude.GetHashCode();
    hashCode ^= Latitude.GetHashCode(); // Xor (Exclusive OR)
    return hashCode;
}
}
```

在此实现中，前两个检查相对明显。检查 4-6 发生在专门接受 Coordinate 数据类型的 Equals() 重载中。这样，两个 Coordinates 的比较将完全避免 Equals(object obj) 及其 GetType() 检查。

由于 GetHashCode() 未缓存且效率不高于步骤 5，因此 GetHashCode() 比较被注释掉了。同样，base.Equals() 未被使用，因为基类未重写 Equals()。（断言检查基类不是 object 类型，但它不检查基类是否重写了 Equals()，而这是适当调用 base.Equals() 所必需的。）无论如何，由于 GetHashCode() 不一定返回唯一值（它只在操作数不同时识别），它本身不能确定性地识别相等对象。

与 GetHashCode() 类似，Equals() 也绝不应抛出任何异常。将任何对象与任何其他对象进行比较是有效的，这样做绝不应导致异常。

## 实现相等性的准则

在学习重写对象虚拟成员的细节时，会出现几条准则。

- Equals()、== 运算符和 != 运算符应一起实现。
- 类型应在 Equals()、== 和 != 实现中使用相同的算法。
- 实现 Equals()、== 和 != 时，还应实现类型的 GetHashCode() 方法。
- GetHashCode()、Equals()、== 和 != 绝不应抛出异常。
- 实现 IComparable 时，还应实现与相等性相关的方法。

## 运算符重载

前一节介绍了重写 Equals()，并提供了类还应实现 == 和 != 的准则。实现任何运算符的术语是运算符重载，本节描述了如何执行此操作，不仅适用于 == 和 !=，也适用于其他受支持的运算符。

例如，string 提供了一个 + 运算符来连接两个字符串。这也许并不令人惊讶，因为 string 是预定义类型，因此可能具有特殊的编译器支持。但是，C# 允许为类或结构体添加 + 运算符支持。事实上，所有运算符都受支持，除了 x.y、f(x)、new、typeof、default、checked、unchecked、delegate、as、is 和 =>。一个特别值得注意的无法实现的运算符是赋值运算符；无法更改 = 运算符的行为。

## 比较运算符 (==, !=, <, >, <=, >=)

重写 Equals() 后，可能存在不一致性。两个对象可能对 Equals() 返回 true，但对 == 运算符返回 false，因为 == 默认也执行引用相等性检查。要纠正这一点，还需要重载等于 (==) 和不等于 (!=) 运算符。

在大多数情况下，这些运算符的实现可以将逻辑委托给 Equals()，或者反过来。但是，首先需要进行一些初始 null 检查（参见清单 9.6）。

```
Listing 9.6: Implementing the == and != Operators

public sealed class Coordinate
{
    // ...

    public static bool operator ==(
        Coordinate leftHandSide,
        Coordinate rightHandSide)
    {
        // Check if LeftHandSide is null.
        // (operator== would be recursive)
        if (ReferenceEquals(leftHandSide, null))
        {
            // Return true if rightHandSide is also null
            // but false otherwise.
            return ReferenceEquals(rightHandSide, null);
        }

        return (leftHandSide.Equals(rightHandSide));
    }

    public static bool operator !=(
        Coordinate leftHandSide,
        Coordinate rightHandSide)
    {
        return !(leftHandSide == rightHandSide);
    }
}
```

请注意，要执行 null 检查，不能使用对 null 的相等性检查（leftHandSide == null）。这样做会递归地回调到该方法，导致循环直到栈溢出。为避免这种情况，请调用 ReferenceEquals() 来检查 null。

