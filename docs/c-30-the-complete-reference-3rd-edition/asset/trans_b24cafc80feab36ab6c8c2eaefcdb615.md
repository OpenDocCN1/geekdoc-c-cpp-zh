

除了其实现的接口所指定的属性之外，BitArray 还添加了 Length，如下所示：

```
public int Length { get; set; }
```

Length 设置或获取集合中的位数。因此，Length 给出的值与为所有集合定义的标准 Count 属性相同。然而，Count 是只读的，而 Length 不是。因此，Length 可用于更改 BitArray 的大小。如果缩短 BitArray，位将从高位端截断。如果加长 BitArray，false 位将添加到高位端。

BitArray 定义以下索引器：

```
public bool this[int idx] { get; set; }
```

可以使用此索引器获取或设置元素的值。

以下示例演示了 BitArray：

```
// Demonstrate BitArray.
using System;
using System.Collections;

class BADemo {
    public static void ShowBits(string rem, BitArray bits) {
        Console.WriteLine(rem);
        for(int i=0; i < bits.Count; i++)
            Console.Write("{0, -6} ", bits[i]);
        Console.WriteLine("\n");
    }
    static void Main() {
        BitArray ba = new BitArray(8);
        byte[] b = { 67 };
        BitArray ba2 = new BitArray(b);
        ShowBits("Original contents of ba:", ba);
        ba = ba.Not();
        ShowBits("Contents of ba after Not:", ba);
        ShowBits("Contents of ba2:", ba2);
        BitArray ba3 = ba.Xor(ba2);
        ShowBits("Result of ba XOR ba2:", ba3);
    }
}
```

输出如下：

```
Original contents of ba:
False False False False False False False False

Contents of ba after Not:
True   True   True   True   True   True

Contents of ba2:
True   False  False  False  False  True   False

Result of ba XOR ba2:
False  False  True   True   True   False  True
```

## 专用集合

.NET Framework 提供了一些专用集合，它们经过优化，可用于处理特定类型的数据或以特定方式工作。这些非泛型集合类定义在 `System.Collections.Specialized` 命名空间内。下表对它们进行了概要说明：

| 专用集合 | 描述 |
|---|---|
| CollectionsUtil | 包含用于创建集合的工厂方法。 |
| HybridDictionary | 一种集合：当集合中元素很少时，它使用 **ListDictionary** 存储键/值对；当集合增长超过一定大小后，会自动使用 **Hashtable** 存储元素。 |
| ListDictionary | 一种将键/值对存储在链表中的集合。仅建议用于小型集合。 |
| NameValueCollection | 一种排序的键/值对集合，其中键和值的类型均为 **string**。 |
| OrderedDictionary | 一种可索引的键/值对集合。 |
| StringCollection | 一种针对存储字符串优化的集合。 |
| StringDictionary | 一种键/值对的哈希表，其中键和值的类型均为 **string**。 |

`System.Collections` 还定义了三个抽象基类：**CollectionBase**、**ReadOnlyCollectionBase** 和 **DictionaryBase**，它们可以被继承，并用作开发自定义专用集合的起点。

## 泛型集合

泛型的加入极大地扩展了集合 API，基本上使集合类和接口的数量翻倍。泛型集合声明在 `System.Collections.Generic` 命名空间中。在许多情况下，泛型集合类只是前面讨论的非泛型类的泛型等价物。然而，这种对应关系并非一一对应。例如，有一个名为 `LinkedList` 的泛型集合实现了双向链表，但没有非泛型等价物。在某些情况下，泛型类和非泛型类之间存在并行功能，但名称不同。例如，`ArrayList` 的泛型版本称为 `List`，`Hashtable` 的泛型版本称为 Dictionary。此外，各种接口和类的具体内容包含少量重组，例如某些功能从一个接口转移到另一个接口。不过总体而言，如果你理解非泛型集合，就能轻松使用泛型集合。

一般来说，泛型集合的工作方式与非泛型集合相同，区别在于泛型集合是类型安全的。因此，泛型集合只能存储与其类型参数兼容的项。所以，如果你想要一个能够存储不相关的混合类型的集合，应使用某个非泛型类。然而，对于集合只存储一种类型对象的所有情况，泛型集合现在是最佳选择。

泛型集合由一组接口以及实现这些接口的类定义。以下各节将分别介绍它们。

### 泛型接口

System.Collections.Generic 定义了许多泛型接口，它们都与相应的非泛型接口对应。表 24-10 总结了这些泛型接口。

### ICollection<T> 接口

ICollection<T> 接口定义了所有泛型集合共有的功能。它继承 IEnumerable 和 IEnumerable<T> 接口。ICollection<T> 是非泛型 ICollection 接口的泛型版本。然而，两者之间存在一些差异。

ICollection<T> 定义以下属性：

- int Count { get; }
- bool IsReadOnly { get; }

Count 包含集合当前持有的项数。如果集合为只读，则 IsReadOnly 为 true；如果集合为读/写，则其为 false。

| 接口 | 描述 |
|---|---|
| ICollection<T> | 定义泛型集合的基础功能。 |
| IComparer<T> | 定义泛型 Comparer() 方法，用于对集合中存储的对象进行比较。 |
| IDictionary<TK, TV> | 定义由键/值对组成的泛型集合。 |
| IEnumerable<T> | 定义泛型 GetEnumerator() 方法，该方法为集合类提供枚举器。 |
| IEnumerator<T> | 提供成员，使集合的内容能够一次获取一个。 |
| IEqualityComparer<T> | 比较两个对象是否相等。 |
| IList<T> | 定义可通过索引器访问的泛型集合。 |

表 24-10 泛型集合接口

ICollection<T> 定义以下方法。注意，它比其非泛型对应接口定义了更多方法。

| 方法 | 描述 |
|---|---|
| void Add(T obj) | 将 obj 添加到调用集合中。如果集合为只读，则引发 NotSupportedException。 |
| void Clear() | 从调用集合中删除所有元素，并将 Count 设置为零。 |
| bool Contains(T obj) | 如果调用集合包含传入 obj 的对象，则返回 true，否则返回 false。 |
| void CopyTo(T[] target, int startIdx) | 将调用集合的内容复制到 target 指定的数组，从 startIdx 指定的索引开始。 |
| bool Remove(T obj) | 从调用集合中移除 obj 的第一个匹配项。如果移除了 obj，则返回 true；如果在调用集合中未找到它，则返回 false。 |

如果集合为只读，其中若干方法将引发 NotSupportedException。由于 ICollection<T> 继承 IEnumerable 和 IEnumerable<T>，它还包括 GetEnumerator() 方法的泛型和非泛型形式。

由于 ICollection<T> 继承 IEnumerable<T>，它支持由 Enumerable 定义的扩展方法。尽管这些扩展方法主要针对 LINQ 设计，但它们也可用于其他用途，包括集合。

### IList<T> 接口

IList<T> 接口定义了一种泛型集合的行为，该集合允许通过从零开始的索引访问元素。它继承 IEnumerable、IEnumerable<T> 和 ICollection<T>，是非泛型 IList 接口的泛型版本。IList<T> 定义表 24-11 所示的方法。其中两个方法意味着修改集合。如果集合为只读或大小固定，则 Insert() 和 RemoveAt() 方法将引发 NotSupportedException。

IList<T> 定义以下索引器：

```
T this[int idx] { get; set; }
```

此索引器设置或获取 idx 指定索引处元素的值。

| 方法 | 描述 |
|---|---|
| int IndexOf(T obj) | 如果调用集合中包含 obj，则返回 obj 第一个匹配项的索引。如果未找到 obj，则返回 -1。 |
| void Insert(int idx, T obj) | 将 obj 插入到 idx 指定的索引处。 |
| void RemoveAt(int idx) | 从调用集合中移除 idx 指定索引处的对象。 |

