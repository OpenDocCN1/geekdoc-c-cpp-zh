
## IDictionary<TK, TV> 接口

IDictionary<TK, TV> 接口定义了一种泛型集合的行为，该集合将唯一键映射到值。也就是说，它定义了一种存储键/值对的集合。IDictionary<TK, TV> 继承 IEnumerable<KeyValuePair<TK, TV>>、IEnumerator<KeyValuePair<TK, TV>> 和 ICollection<KeyValuePair<TK, TV>>，并且是非泛型 IDictionary 的泛型版本。IDictionary<TK, TV> 声明的方法总结在表 24-12 中。如果尝试指定 null 键，这些方法都会抛出 ArgumentNullException。

IDictionary<TK, TV> 定义以下属性：

| 属性 | 描述 |
|---|---|
| ICollection<TK> Keys { get; } | 获取键的集合。 |
| ICollection<TV> Values { get; } | 获取值的集合。 |

请注意，集合中包含的键和值可通过 Keys 和 Values 属性作为单独的列表使用。

IDictionary<TK, TV> 定义以下索引器：

```
TV this[TK key] { get; set; }
```

可以使用此索引器获取或设置元素的值。也可以使用它向集合中添加新元素。请注意，“索引”实际上并不是索引，而是项的键。

## IEnumerable<T> 和 IEnumerator<T>

IEnumerable<T> 和 IEnumerator<T> 是前面所述非泛型 IEnumerable 和 IEnumerator 接口的泛型等价物。它们声明相同的方法和属性，并以相同的方式工作。当然，泛型版本对类型参数所指定类型的数据进行操作。

IEnumerable<T> 声明 GetEnumerator() 方法，如下所示：

```
IEnumerator<T> GetEnumerator()
```

它返回该集合的 T 类型枚举器。因此，它返回类型安全的枚举器。

| 方法 | 描述 |
|---|---|
| void Add(TK k, TV v) | 将 k 和 v 指定的键/值对添加到调用集合中。如果 k 已存储在集合中，则抛出 ArgumentException。 |
| bool ContainsKey(TK k) | 如果调用集合包含 k 作为键，则返回 true。否则，返回 false。 |
| bool Remove(TK k) | 移除键等于 k 的项。 |
| bool TryGetValue(TK k, out TV v) | 尝试检索与 k 关联的值，并将其放入 v 中。如果成功则返回 true，否则返回 false。如果未找到 k，则 v 被赋予其默认值。 |

IEnumerator<T> 具有与非泛型 IEnumerator 相同的两个方法：MoveNext() 和 Reset()。它还声明 Current 属性的泛型版本，如下所示：

```
T Current { get; }
```

它返回对下一个对象的 T 引用。因此，Current 的泛型版本是类型安全的。

IEnumerator 和 IEnumerator<T> 之间还有一个区别：IEnumerator<T> 继承 IDisposable 接口，而 IEnumerator 不继承。IDisposable 定义 Dispose() 方法，该方法用于释放非托管资源。

> 注意 IEnumerator<T> 还实现了非泛型 IEnumerable 接口。因此，它支持非泛型版本的 GetEnumerator()。IEnumerator<T> 还实现了非泛型 IEnumerator 接口，因此支持非泛型版本的 Current。

## IComparer<T>

IComparer<T> 接口是前面所述 IComparer 的泛型版本。两者之间的主要区别在于 IComparer<T> 是类型安全的，它声明 Compare() 的泛型版本，如下所示：

```
int Compare(T obj1, T obj2)
```

此方法比较 obj1 与 obj2，如果 obj1 大于 obj2 则返回大于零的值，如果两个对象相同则返回零，如果 obj1 小于 obj2 则返回小于零的值。

## IEqualityComparer<T>

IEqualityComparer<T> 接口等同于其非泛型对应接口 IEqualityComparer。它定义以下两个方法：

```
bool Equals(T obj1, T obj2)
int GetHashCode(T obj)
```

如果 obj1 和 obj2 相等，Equals() 必须返回 true。GetHashCode() 必须返回 obj 的哈希代码。

## KeyValuePair<TK, TV> 结构

System.Collections.Generic 定义了一个名为 KeyValuePair<TK, TV> 的结构，用于存储键及其值。存储键/值对的泛型集合类（例如 Dictionary<TK, TV>）使用它。此结构定义以下两个属性：

```
public TK Key { get; };
public TV Value { get; };
```

这些属性保存与某个项关联的键或值。可以使用以下构造函数构造 KeyValuePair<TK, TV> 对象：

```
public KeyValuePair(TK k, TV v)
```

这里，k 是键，v 是值。

## 泛型集合类

如本节开头所述，泛型集合类在很大程度上与非泛型对应类并行，尽管在某些情况下名称已更改。此外，在组织结构和功能上也存在一些差异。泛型集合定义在 System.Collections.Generic 中。本章描述的泛型集合如表 24-13 所示。这些类构成泛型集合的核心。

> 注意 System.Collections.Generic 还包括以下类：SynchronizedCollection<T> 是基于 IList<T> 的同步集合。SynchronizedReadOnlyCollection<T> 是基于 IList<T> 的只读同步集合。SynchronizedKeyCollection<K, V> 是一个抽象类，由 System.ServiceModel.UriSchemeKeyedCollection 用作基类。KeyedByTypeCollection<T> 是一个使用类型作为键的集合。

## List<T> 集合

List<T> 类实现泛型动态数组，在概念上类似于非泛型 ArrayList 类。List<T> 实现 ICollection、ICollection<T>、IList、IList<T>、IEnumerable 和 IEnumerable<T> 接口。List<T> 具有如下所示的构造函数：

```
public List()
public List(IEnumerable<T> c)
public List(int capacity)
```

第一个构造函数构建一个具有默认初始容量的空 List。第二个构造函数构建一个 List，它用 c 指定的集合中的元素初始化，并且初始容量至少等于元素数。第三个构造函数构建一个具有指定初始容量的数组列表。容量是用于存储元素的底层数组的大小。随着元素被添加到 List<T>，容量会自动增长。每次必须扩大列表时，其容量都会增加。

| 类 | 描述 |
|---|---|
| Dictionary<TK, TV> | 存储键/值对。提供与非泛型 Hashtable 类相似的功能。 |
| HashSet<T> | 使用哈希表存储一组唯一值。 |
| LinkedList<T> | 在双向链表中存储元素。 |
| List<T> | 动态数组。提供与非泛型 ArrayList 类相似的功能。 |
| Queue<T> | 先进先出列表。提供与非泛型 Queue 类相似的功能。 |
| SortedDictionary<TK, TV> | 键/值对的排序列表。 |
| SortedList<TK, TV> | 键/值对的排序列表。提供与非泛型 SortedList 类相似的功能。 |
| Stack<T> | 先进后出列表。提供与非泛型 Stack 类相似的功能。 |

表 24-13 核心泛型集合类

除了其实现的接口所定义的方法之外，**List<T>** 还定义了几个自己的方法。表 24-14 展示了其中的一些示例。

| 方法 | 描述 |
| --- | --- |
| public void AddRange(IEnumerable<T> c) | 将 c 中的元素添加到调用列表的末尾。 |
| public virtual int BinarySearch(T v) | 在调用集合中搜索 v 中传入的值。返回匹配元素的索引。如果未找到该值，则返回负值。调用列表必须已排序。 |
| public int BinarySearch(T v, IComparer<T> comp) | 使用 comp 指定的比较对象在调用集合中搜索 v 中传入的值。返回匹配元素的索引。如果未找到该值，则返回负值。调用列表必须已排序。 |
| public int BinarySearch(int startIdx, int count, T v, IComparer<T> comp) | 使用 comp 指定的比较对象在调用集合中搜索 v 中传入的值。搜索从 startIdx 开始，并持续 count 个元素。返回匹配元素的索引。如果未找到该值，则返回负值。调用列表必须已排序。 |
| public List<T> GetRange(int idx, int count) | 返回调用列表的一部分。返回的范围从 idx 开始，并持续 count 个元素。返回的对象引用与调用对象相同的元素。 |
| public int IndexOf(T v) | 返回 v 在调用集合中首次出现的索引。如果未找到 v，则返回 -1。 |
| public void InsertRange(int startIdx, IEnumerable<T> c) | 将 c 的元素插入调用集合中，从 startIdx 指定的索引开始。 |
| public int LastIndexOf(T v) | 返回 v 在调用集合中最后出现的索引。如果未找到 v，则返回 -1。 |
| public void RemoveRange(int idx, int count) | 从调用集合中移除 count 个元素，从 idx 开始。 |
| public void Reverse( ) | 反转调用集合的内容。 |
| public void Reverse(int startIdx, int count) | 反转调用集合中从 startIdx 开始的 count 个元素。 |
| public void Sort( ) | 将集合按升序排序。 |
| public void Sort(IComparer<T> comp) | 使用指定的比较对象对集合排序。如果 comp 为 null，则使用每个对象的默认比较器。 |
| public void Sort(Comparison<T> comp) | 使用指定的比较委托对集合排序。 |

**表 24-14** 由 **List<T>** 定义的方法示例

