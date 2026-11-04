

枚举时，`SortedDictionary<TK, TV>` 会以 **KeyValuePair<TK, TV>** 结构的形式返回键/值对。请回忆一下，此结构定义了以下两个字段：

```csharp
public TK Key;
public TV Value;
```

这些字段保存与某个条目关联的键或值。在大多数情况下，你不需要直接使用 **KeyValuePair<TK, TV>**，因为 **SortedDictionary<TK, TV>** 允许你分别处理键和值。但是，在枚举 **SortedDictionary<TK, TV>** 时（例如在 foreach 循环中），被枚举的对象就是 **KeyValuePairs**。

在 **SortedDictionary<TK, TV>** 中，所有键都必须是唯一的，并且键在作为键使用期间不能发生更改。值不必是唯一的。

下面的示例演示了 **SortedDictionary<TK, TV>**。它重新实现了上一节中展示的 **Dictionary<TK, TV>** 示例。在此版本中，员工和薪资数据库根据姓名（即键）进行排序。

```csharp
// Demonstrate the generic SortedDictionary<TK, TV> class.
using System;
using System.Collections.Generic;

class GenSortedDictionaryDemo {
    static void Main() {
        // Create a Dictionary that holds employee
        // names and their corresponding salary
        SortedDictionary<string, double> dict =
            new SortedDictionary<string, double>();

        // Add elements to the collection.
        dict.Add("Butler, John", 73000);
        dict.Add("Swartz, Sarah", 59000);
        dict.Add("Pyke, Thomas", 45000);
        dict.Add("Frank, Ed", 99000);

        // Get a collection of the keys (names).
        ICollection<string> c = dict.Keys;

        // Use the keys to obtain the values (salaries).
        foreach(string str in c)
            Console.WriteLine("{0}, Salary: {1:C}", str, dict[str]);
    }
}
```

输出如下：

```
Butler, John, Salary: $73,000.00
Frank, Ed, Salary: $99,000.00
Pyke, Thomas, Salary: $45,000.00
Swartz, Sarah, Salary: $59,000.00
```

如你所见，现在列表根据键（即员工姓名）进行了排序。

## SortedList<TK, TV> 类

`SortedList<TK, TV>` 类存储排序后的键/值对列表。它是非泛型 `SortedList` 类的泛型等效版本。`SortedList<TK, TV>` 实现了 `IDictionary`、`IDictionary<TK, TV>`、`ICollection`、`ICollection<KeyValuePair<TK, TV>>`、`IEnumerable` 和 `IEnumerable<KeyValuePair<TK, TV>>`。`SortedList<TK, TV>` 的大小是动态的，并会根据需要自动增长。`SortedList<TK, TV>` 与 `SortedDictionary<TK, TV>` 类似，但二者具有不同的性能特征。例如，`SortedList<TK, TV>` 使用的内存较少，而在插入无序元素时，`SortedDictionary<TK, TV>` 的速度更快。

`SortedList<TK, TV>` 提供了多个构造函数。下面列举其中一些：

```csharp
public SortedList()
public SortedList(IDictionary<TK, TV> dict)
public SortedList(int capacity)
public SortedList(IComparer<TK> comp)
```

第一个构造函数创建一个具有默认容量的空列表。第二个构造函数创建一个包含与 dict 中相同元素的列表。第三个构造函数允许你指定初始容量。如果你预先知道需要一个特定大小的列表，那么指定该容量可以避免在运行时调整列表大小，因为调整大小是一个开销较大的过程。第四种形式允许你指定一种比较方法，用于比较列表中包含的对象。

向 `SortedList<TK, TV>` 列表添加元素时，其容量会根据需要自动增长。当超过当前容量时，容量会增加。指定容量的优点是可以避免或减少调整集合大小所产生的开销。当然，只有在你大致知道将存储多少个元素时，指定初始容量才有意义。

除了实现的接口所定义的方法之外，`SortedList<TK, TV>` 还定义了自己的多个方法。表 24-18 列出了其中一些方法。请注意，`GetEnumerator()` 返回的枚举器会将列表中存储的键/值对枚举为 `KeyValuePair` 类型的对象。

### 表 24-18 SortedList<TK, TV> 定义的几个常用方法

| 方法 | 说明 |
|---|---|
| public void Add(TK k, TV v) | 将由 k 和 v 指定的键/值对添加到列表中。如果 k 已在列表中，则其值不会改变，并且会引发 ArgumentException。 |
| public bool ContainsKey(TK k) | 如果 k 是调用列表中的键，则返回 true；否则返回 false。 |
| public bool ContainsValue(TV v) | 如果 v 是调用列表中的值，则返回 true；否则返回 false。 |
| public IEnumerator<KeyValuePair<TK, TV>> GetEnumerator() | 返回调用列表的枚举器。 |
| public int IndexOfKey(TK k) | 返回由 k 指定的键的索引。如果该键不在列表中，则返回 -1。 |
| public int IndexOfValue(TV v) | 返回由 v 指定的值第一次出现的位置。如果该值不在列表中，则返回 -1。 |
| public bool Remove(TK k) | 从列表中移除与 k 关联的键/值对。如果操作成功，则返回 true；如果 k 不在列表中，则返回 false。 |
| public void RemoveAt(int idx) | 移除索引为 idx 的键/值对。 |
| public void TrimExcess() | 移除调用列表的多余容量。 |

除了实现的接口所定义的属性之外，`SortedList<TK, TV>` 还定义了以下属性：

| 属性 | 说明 |
|---|---|
| public int Capacity { get; set; } | 获取或设置调用列表的容量。 |
| public IComparer<TK> Comparer { get; } | 获取调用列表的比较器。 |
| public IList<TK> Keys { get; } | 获取键的集合。 |
| public IList<TV> Values { get; } | 获取值的集合。 |

`SortedList<TK, TV>` 定义了以下索引器（该索引器由 `IDictionary<TK, TV>` 定义）：

```csharp
public TV this[TK key] { get; set; }
```

你可以使用此索引器获取或设置元素的值，也可以使用它向集合中添加新元素。请注意，这里的“索引”实际上并不是索引，而是项目的键。

下面的示例演示了 `SortedList<TK, TV>`。它再次改写了员工数据库示例。在此版本中，数据库存储在 `SortedList` 中。

```csharp
// Demonstrate a SortedList<TK, TV>.
using System;
using System.Collections.Generic;

class GenSLDemo {
    static void Main() {
        // Create a sorted SortedList for
        // employee names and salary.
        SortedList<string, double> sl =
            new SortedList<string, double>();

        // Add elements to the collection.
        sl.Add("Butler, John", 73000);
        sl.Add("Swartz, Sarah", 59000);
        sl.Add("Pyke, Thomas", 45000);
        sl.Add("Frank, Ed", 99000);

        // Get a collection of the keys.
        ICollection<string> c = sl.Keys;

        // Use the keys to obtain the values.
        foreach(string str in c)
            Console.WriteLine("{0}, Salary: {1:C}", str, sl[str]);

        Console.WriteLine();
    }
}
```

输出如下：

```
Butler, John, Salary: $73,000.00
Frank, Ed, Salary: $99,000.00
Pyke, Thomas, Salary: $45,000.00
Swartz, Sarah, Salary: $59,000.00
```

正如输出所示，列表根据员工姓名（即键）进行了排序。

## Stack<T> 类

`Stack<T>` 是非泛型 `Stack` 类的泛型等效版本。`Stack<T>` 支持先进后出的堆栈。它实现了 `ICollection`、`IEnumerable` 和 `IEnumerable<T>` 接口。`Stack<T>` 直接实现了 `ICollection<T>` 定义的 `Clear()`、`Contains()` 和 `CopyTo()` 方法。（不支持 `Add()` 和 `Remove()` 方法，也不支持 `IsReadOnly` 属性。）`Stack<T>` 是一个动态集合，会根据需要增长，以容纳必须存储的元素。它定义了以下构造函数：

```csharp
public Stack()
public Stack(int capacity)
public Stack(IEnumerable<T> c)
```

第一种形式创建一个具有默认初始容量的空堆栈。第二种形式创建一个具有由 capacity 指定的初始容量的空堆栈。第三种形式创建一个包含由 c 指定的集合中元素的堆栈。

除了实现的接口所定义的方法（以及它自行实现的 `ICollection<T>` 所定义的方法）之外，`Stack<T>` 还定义了表 24-19 中所示的方法。`Stack<T>` 的工作方式与其非泛型对应版本完全相同。要将对象放到堆栈顶部，请调用 `Push()`。要移除并返回顶部元素，请调用 `Pop()`。你可以使用 `Peek()` 返回顶部对象，但不会将其移除。如果在调用堆栈为空时调用 `Pop()` 或 `Peek()`，则会引发 `InvalidOperationException`。

