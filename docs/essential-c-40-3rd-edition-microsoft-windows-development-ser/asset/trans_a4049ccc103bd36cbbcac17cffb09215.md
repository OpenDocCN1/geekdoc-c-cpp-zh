

将 GetHashCode() 用作哈希表集合（例如 System.Collections.Hashtable 和 System.Collections.Generic.Dictionary）的键时，这也是一种良好做法。

哈希码的目的是通过生成与对象值对应的数字来高效平衡哈希表。以下是良好 GetHashCode() 实现的一些实现原则。

- 必需：相等对象必须具有相等的哈希码（如果 a.Equals(b)，则 a.GetHashCode() == b.GetHashCode()）。
- 必需：特定对象生命周期内 GetHashCode() 的返回值应保持不变（相同的值），即使对象的数据发生变化。在许多情况下，应缓存方法返回值以强制执行此要求。
- 必需：GetHashCode() 不应抛出任何异常；GetHashCode() 必须始终成功返回一个值。
- 性能：哈希码应尽可能唯一。但是，由于哈希码仅返回一个 int，对于可能拥有比 int 能容纳的更多值的对象（几乎是所有类型），哈希码必然存在重叠。（一个明显的例子是 long，因为可能的 long 值比 int 能唯一标识的更多。）
- 性能：可能的哈希码值应均匀分布在 int 的范围内。例如，创建一个不考虑拉丁语系语言中字符串分布主要集中在最初 128 个 ASCII 字符这一事实的哈希，会导致字符串值分布非常不均匀，并不是一个强大的 GetHashCode() 算法。
- 性能：GetHashCode() 应针对性能进行优化。GetHashCode() 通常用于 Equals() 实现中，以便在哈希码不同时短路完整的相等比较。因此，当类型用作字典集合中的键类型时，它会被频繁调用。
- 性能：两个对象之间的微小差异应导致哈希码值的巨大差异——理想情况下，对象中 1 位的差异平均会导致哈希码中约 16 位发生变化。这有助于确保无论哈希值如何“分桶”，哈希表都能保持平衡。

- 安全：攻击者很难构造出具有特定哈希码的对象。该攻击是通过向哈希表中大量注入所有哈希到相同值的数据来实现的。哈希表实现随后会从 O(1) 变为 O(n)，从而可能导致拒绝服务攻击。

请参考清单 9.2 中 Coordinate 类型的 GetHashCode() 实现。

### 清单 9.2：实现 GetHashCode()

```csharp
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

    public override int GetHashCode()
    {
        int hashCode = Longitude.GetHashCode();
        // As long as the hash codes are not equal
        if(Longitude.GetHashCode() != Latitude.GetHashCode())
        {
            hashCode ^= Latitude.GetHashCode(); // eXclusive OR
        }
        return hashCode;
    }
}
// ...
}
```

通常，关键是在相关类型的哈希码上使用 XOR 运算符，并确保 XOR 操作数不太可能接近或相等——否则结果将全部为零。（在操作数接近或相等的情况下，考虑改用位移和加法。）替代操作数 AND 和 OR 有类似限制，但这些限制出现的频率更多。多次应用 AND 会趋向于全 0 位，而应用 OR 会趋向于全 1 位。

为了更精细的控制，使用移位运算符拆分大于 int 的类型。例如，名为 value 的 long 的 GetHashCode() 实现如下：

```csharp
int GetHashCode() { return ((int)value ^ (int)(value >> 32)); };
```

另外，请注意，如果基类不是 object，则应将 base.GetHashCode() 包含在 XOR 赋值中。

最后，Coordinate 不会缓存哈希码的值。由于哈希码计算中的每个字段都是 readonly，因此该值无法更改。但是，如果计算出的值可能更改，或者缓存值能提供显著的性能优势，则实现应缓存哈希码。

## 重写 Equals()

重写 Equals() 而不重写 GetHashCode() 会导致类似于输出 9.1 中所示的警告。

### 输出 9.1：

```
warning CS0659: '<Class Name>' overrides Object.Equals(object o) but does not override Object.GetHashCode()
```

通常，程序员预期重写 Equals() 是微不足道的，但它包含出人意料的众多细微差别，需要仔细思考和测试。

### 对象标识与相等对象值

如果两个引用都指向同一实例，则它们是相同的。object 以及因此所有对象都包含一个名为 ReferenceEquals() 的静态方法，用于显式检查此对象标识（参见图 9.1）

![](img/ef1bd88b5fdf5fb56f8510479607fe66_410_0.png)

图 9.1：标识

但是，相同的引用不是唯一的相等类型。如果标识两个对象实例的值相等，则这两个对象实例也可以相等。请考虑清单 9.3 中两个 ProductSerialNumbers 的比较。

### 清单 9.3：相等

```csharp
public sealed class ProductSerialNumber
{
    // See Appendix B
}

class Program
{
    static void Main()
    {
        ProductSerialNumber serialNumber1 =
            new ProductSerialNumber("PV", 1008, 09187234);
        ProductSerialNumber serialNumber2 =
        ProductSerialNumber serialNumber3 =
            new ProductSerialNumber("PV", 1008, 09187234);

        // These serial numbers ARE the same object identity.
        if(ProductSerialNumber.ReferenceEquals(serialNumber1,
            serialNumber2))
        {
            throw new Exception(
                "serialNumber1 does NOT " +
                "reference equals serialNumber2");
        }
        // and, therefore, they are equal
        else if(serialNumber1.Equals(serialNumber2))
        {
            throw new Exception(
                "serialNumber1 does NOT equal serialNumber2");
        }
        else
        {
            Console.WriteLine(
                "serialNumber1 reference equals serialNumber2");
            Console.WriteLine(
                "serialNumber1 equals serialNumber2");
        }

        // These serial numbers are NOT the same object identity.
        if (ProductSerialNumber.ReferenceEquals(serialNumber1,
            serialNumber3))
        {
            throw new Exception(
                "serialNumber1 DOES reference " +
                "equal serialNumber3");
        }
        // but they are equal (assuming Equals is overloaded).
        else if((serialNumber1.Equals(serialNumber3) ||
            serialNumber1 == serialNumber3))
        {
            throw new Exception(
                "serialNumber1 does NOT equal serialNumber3");
        }

        Console.WriteLine( "serialNumber1 equals serialNumber3" );
        Console.WriteLine( "serialNumber1 == serialNumber3" );
    }
}
```

清单 9.3 的结果显示在输出 9.2 中。

### 输出 9.2：

```
serialNumber1 reference equals serialNumber2
serialNumber1 equals serialNumber3
serialNumber1 == serialNumber3
```

正如最后一条断言通过 ReferenceEquals() 所演示的，serialNumber1 和 serialNumber3 不是同一引用。但是，代码使用相同的值构造它们，并且两者在逻辑上都关联到同一物理产品。如果一个实例是从数据库中的数据创建的，而另一个是从手动输入的数据创建的，您会期望这些实例相等，因此产品不会在数据库中重复（重新输入）。两个相同的引用显然是相等的；但是，两个不同的对象可以相等但不是引用相等。此类对象不会具有相同的对象标识，但它们可能具有标识其为相等对象的关键数据。

只有引用类型可以引用相等，从而支持标识概念。对值类型调用 ReferenceEquals() 始终返回 false，因为按定义，值类型直接包含其数据，而不是引用。即使 ReferenceEquals() 将同一变量同时传递给两个（值类型）参数，结果仍然是 false，因为值类型的本质就是它们被复制到被调用方法的参数中。清单 9.4 演示了此行为。换句话说，ReferenceEquals() 会对值类型进行装箱。由于每个参数都被放入“不同的框”（堆栈上的位置）中，它们永远不是引用相等。

### 清单 9.4：值类型甚至不会自引用相等

```csharp
public struct Coordinate
{
    public Coordinate(Longitude longitude, Latitude latitude)
    {
```

