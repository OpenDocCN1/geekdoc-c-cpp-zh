

## 11 集合

- 理解集合接口和类型
- 使用列表、队列和栈
- 使用链表和排序列表
- 使用字典和集合
- 评估性能

本章的 wrox.com 代码下载可在 http://www.wrox.com/go/professionalcsharp6 的 Download Code 选项卡中找到。本章代码分为以下主要示例：

- 列表示例
- 队列示例
- 链表示例
- 排序列表示例
- 字典示例
- 集合示例

第7章“数组和元组”介绍了数组以及 Array 类实现的接口。数组的大小是固定的。如果元素数量是动态的，则应使用集合类而非数组。

`List<T>` 是一个可以与数组相比的集合类；但还有其它类型的集合：队列、栈、链表、字典和集合。其它集合类在访问集合中的元素时具有部分不同的 API，并且通常在内存中存储项的内部结构也不同。本章介绍所有这些集合类及其差异，包括性能差异。

本章还讨论位数组和可供多个线程使用的并发集合。

大多数集合类位于 `System.Collections` 和 `System.Collections.Generic` 命名空间中。泛型集合类位于 `System.Collections.Generic` 命名空间中。专门用于特定类型的集合类位于 `System.Collections.Specialized` 命名空间中。线程安全的集合类位于 `System.Collections.Concurrent` 命名空间中。不可变集合类位于 `System.Collections.Immutable` 命名空间中。

当然，还有其它方式对集合类进行分组。根据集合类实现的接口，可以将集合分为列表、集合和字典。

> **注意** *你可以在第7章中阅读关于接口 `IEnumerable` 和 `IEnumerator` 的详细信息。*

下表描述了集合和列表实现的最重要接口。

| 接口 | 描述 |
|---|---|
| `IEnumerable<T>` | `foreach` 语句需要 `IEnumerable` 接口。该接口定义了 `GetEnumerator` 方法，该方法返回一个实现 `IEnumerator` 接口的枚举器。 |
| `ICollection<T>` | `ICollection<T>` 由泛型集合类实现。通过它你可以获取集合中的项数（`Count` 属性），并将集合复制到数组（`CopyTo` 方法）。你还可以添加和删除集合中的项（`Add`、`Remove`、`Clear`）。 |
| `IList<T>` | `IList<T>` 接口用于可以从其位置访问元素的列表。该接口定义了一个索引器，以及从特定位置插入或删除项的方法（`Insert`、`RemoveAt` 方法）。`IList<T>` 派生自 `ICollection<T>`。 |
| `ISet<T>` | 此接口由集合实现。集合允许将不同的集合并为并集，获取两个集合的交集，并检查两个集合是否重叠。`ISet<T>` 派生自 `ICollection<T>`。 |
| `IDictionary<TKey, TValue>` | `IDictionary<TKey, TValue>` 接口由具有键和值的泛型集合类实现。通过该接口可以访问所有键和值，可以使用 `key` 类型的索引器访问项，并且可以添加或删除项。 |
| `ILookup<TKey, TValue>` | 与 `IDictionary<TKey, TValue>` 接口类似，查找具有键和值。但是，对于查找，集合可以用一个键包含多个值。 |
| `IComparer<T>` | `IComparer<T>` 接口由比较器实现，用于通过 `Compare` 方法对集合中的元素进行排序。 |
| `IEqualityComparer<T>` | `IEqualityComparer<T>` 由可用于字典中键的比较器实现。通过此接口，可以比较对象是否相等。 |

### 列表

对于可调整大小的列表，.NET Framework 提供了泛型类 `List<T>`。此类实现了 `IList`、`ICollection`、`IEnumerable`、`IList<T>`、`ICollection<T>` 和 `IEnumerable<T>` 接口。

以下示例使用 Racer 类的成员作为要添加到集合中的元素，以表示一级方程式赛车手。该类有五个属性：Id、FirstName、LastName、Country 和 Wins 数量。通过该类的构造函数，可以传递赛车手的姓名和获胜次数来设置成员。ToString 方法被重写以返回赛车手的姓名。Racer 类还实现了泛型接口 `IComparable<T>` 以对赛车手元素进行排序，以及 `IFormattable`（代码文件 ListSamples/Racer.cs）：

```
public class Racer: IComparable<Racer>, IFormattable
{
    public int Id { get; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Country { get; set; }
    public int Wins { get; set; }

    public Racer(int id, string firstName, string lastName, string country)
        : this(id, firstName, lastName, country, wins: 0)
    { }

    public Racer(int id, string firstName, string lastName, string country, int wins)
    {
        Id = id;
        FirstName = firstName;
        LastName = lastName;
        Country = country;
        Wins = wins;
    }
    public override string ToString() => $"{FirstName} {LastName}";
    public string ToString(string format, IFormatProvider formatProvider)
    {
        if (format == null) format = "N";
        switch (format.ToUpper())
        {
            case "N": // name
                return ToString();
            case "F": // first name
                return FirstName;
            case "L": // last name
                return LastName;
            case "W": // Wins
                return $"{ToString()}, Wins: {Wins}";
            case "C": // Country
                return $"{ToString()}, Country: {Country}";
            case "A": // All
                return $"{ToString()}, Country: {Country} Wins: {Wins}";
            default:
                throw new FormatException(String.Format(formatProvider, $"Format {format} is not supported"));
        }
    }
    public string ToString(string format) => ToString(format, null);
    public int CompareTo(Racer other)
    {
        int compare = LastName?.CompareTo(other?.LastName) ?? -1;
        if (compare == 0)
        {
            return FirstName?.CompareTo(other?.FirstName) ?? -1;
        }
        return compare;
    }
}
```

### 创建列表

你可以通过调用默认构造函数来创建列表对象。对于泛型类 `List<T>`，必须在声明中指定列表值的类型。以下代码演示了如何声明一个 `int` 类型的 `List<T>` 和一个包含 `Racer` 元素的列表。`ArrayList` 是一个非泛型列表，其元素接受任何 `Object` 类型。

使用默认构造函数会创建一个空列表。一旦向列表添加元素，列表的容量就会扩展为允许 4 个元素。如果添加第五个元素，列表会调整为允许 8 个元素。如果 8 个元素还不够，列表会再次调整为包含 16 个元素。每次调整大小，列表的容量都会翻倍。

```
var intList = new List<int>();
var racers = new List<Racer>();
```

当列表的容量发生变化时，整个集合会重新分配到新的内存块。在 `List<T>` 的实现中，使用了类型为 `T` 的数组。重新分配时，会创建一个新数组，`Array.Copy` 将元素从旧数组复制到新数组。为了节省时间，如果你预先知道列表中应包含的元素数量，可以通过构造函数定义容量。以下示例创建了一个容量为 10 个元素的集合。如果容量不足以容纳添加的元素，容量会调整为 20，然后调整为 40 个元素——再次翻倍：

```
List<int> intList = new List<int>(10);
```

你可以使用 `Capacity` 属性获取和设置集合的容量：

```
intList.Capacity = 20;
```

容量与集合中元素的数量不同。集合中元素的数量可以通过 `Count` 属性读取。当然，容量总是大于或等于项的数量。只要没有向列表添加元素，计数就为 0：

```
WriteLine(intList.Count);
```

