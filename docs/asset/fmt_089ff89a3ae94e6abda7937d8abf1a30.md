
188 泛型集合：集合、列表和字典

# 27.6 `List<T>` 类

泛型类 `List<T>` 实现了 `IList<T>` 和 `IList`。元素存储在数组中，数组根据元素的添加需要增长。元素访问很快，但在列表末尾之外的插入和删除开销较大。`List<T>` 类具有由 `IList<T>` 定义的成员以及其他成员：

- 构造函数 `List<T>()` 创建空列表。
- 构造函数 `List<T>(int capacity)` 创建具有给定初始容量的空列表。
- 构造函数 `List<T>(IEnumerable<T> enm)` 创建一个包含 `enm.elements` 的列表。
- 读写属性 `int Capacity` 获取或设置列表当前容量。如果容量小于元素数量，则抛出 `ArgumentOutOfRangeException`。
- `void AddRange(IEnumerable<T> enm)` 将元素添加到列表末尾。
- `IList<T> AsReadOnly()` 返回一个对给定列表进行封装的只读列表。
- `int BinarySearch(T x)` 使用二分查找搜索 `x`。对于 `a[i].CompareTo(x) == 0`，返回索引 `i>=0`；否则返回 `i`，使得 `-i` 为 k 的位置。列表必须排序，或者调用 `Sort(cmp)`；否则结果未定义。
- `int BinarySearch(T x, IComparer<T> cmp)` 工作方式类似，但使用 `cmp.Compare` 比较元素。列表必须排序，或者调用 `Sort(cmp)`；否则结果未定义。
- `int BinarySearch(int i, int n, IComparer<T> cmp)` 工作方式类似，但在索引 `i..(n-1)` 范围内搜索列表。
- `void CopyTo(int src, T[] arr, int dat, int n)` 将从位置 `src` 开始的 `n` 个元素复制到从位置 `dat` 开始的数组 `arr` 中。如果 `src<0` 或 `dat<0` 或 `n<0`，则抛出 `ArgumentOutOfRangeException`。
- `int IndexOf(T x, int i)` 返回大于或等于 `i` 的元素等于 `x` 的最小索引；否则返回 -1。如果 `i<0` 或 `i>Count`，则抛出 `ArgumentOutOfRangeException`。
- `int IndexOf(T x)` 返回大于 0 且小于 `Count` 的元素 `x` 的最小索引；另外两个重载与 `IndexOf` 类似，但在元素等于 `x` 时返回比最小索引更大的索引。
- `void RemoveRange(int i, int n)` 移除范围 `i..(n-1)` 中的元素。
- `void Reverse()` 反转列表顺序。
- `void Reverse(int i, int n)` 反转 `i..(n-1)` 范围内的元素。
- `void Sort()` 使用快速排序排序列表，使用它们的 `CompareTo` 方法比较元素。列表元素必须实现 `IComparable<T>`。排序是不稳定的。
- `void Sort(IComparer<T> cmp)` 使用 `cmp.Compare` 比较元素并排序列表。
- `void Sort(int i, int n, IComparer<T> cmp)` 排序索引为 `i..(n-1)` 的片段。
- `T[] ToArray()` 返回一个包含列表元素的新数组。
- `void TrimSize()` 将列表的容量缩小到实际元素数量。

泛型集合：集合、列表和字典 189

## 示例 227 简单的列表操作

这展示了基于数组的列表末尾快速添加元素与列表头部缓慢插入元素之间的区别。这两个操作所需的时间分别为 $O(1)$ 和 $O(n)$（参见第 181 页的表格）。对于其他列表操作，请参见示例 219 和 228。

```sharp
List<int> lst = new List<int>();

lst.Add(7); lst.Add(9); lst.Add(13);

Print(lst);

// 7 9 13 7

int i1 = 2;

int i2 = lst.IndexOf(7);

// 0

int i3 = lst.IndexOf(12);

// -1

lst.Remove(8); Print(lst);

// 7 9 13 7

lst.Remove(7); Print(lst);

// 9 13 7

lst.Insert(3, 88); Print(lst);

// 9 13 7 88

int count = 100000;

Console.WriteLine("Adding elements at end of list (fast)...");

for (int i=0; i<count; i++) lst.Add(i);

lst.Clear();

Console.WriteLine("Adding elements at head of list (slow)...");

for (int i=0; i<count; i++) lst.Insert(0, i);
```

## 示例 228 在列表中查询结果并返回数组

有时方法必须返回结果数组，而结果的数量提前未知。在这种情况下，结果可以在列表中产生并传输到数组。此方法执行数据库查询，从查询中读取记录并放入 `List<Record>`，然后将其转换为数组。完整的示例代码展示了如何打开数据库连接。

```csharp
using System.Data.Odbc; // OdbcConnection OdbcDataReader

using System.Collections.Generic; // List<T>

struct Record {
    public string Name, msg;
}

static Record[] GetMessages(OdbcConnection conn) {
    string query = "SELECT name, msg FROM Message ORDER BY name";
    OdbcCommand cmd = new OdbcCommand(query, conn);
    OdbcDataReader reader = cmd.ExecuteReader();
    List<Record> results = new List<Record>();
    while (reader.Read())
        results.Add(new Record(reader.GetString(0), reader.GetString(1)));
    reader.Close();
    return results.ToArray();
}
```

190 泛型集合：集合、列表和字典

# 27.7 `Dictionary<K,V>` 和 `SortedDictionary<K,V>` 类

`Dictionary<K,V>` 和 `SortedDictionary<K,V>` 实现了 `IDictionary<K,V>`（第 27.5 节），用于表示具有键 K 和关联值 V。`Dictionary<K,V>` 实现为哈希表，因此具有良好的 `GetHashCode` 但没有排序。`SortedDictionary<K,V>` 实现为有序树，因此键应该是 `IComparable<K>`。作为键的对象应该是不可变的；如果随后修改了对象，条目可能会从字典中丢失。`Dictionary<K,V>` 和 `SortedDictionary<K,V>` 拥有 `Dictionary<K,V>` 的方法、构造函数，以及附加方法：

- `Dictionary<K,V>()` 创建空字典。
- `Dictionary<K,V>(int capacity)` 创建具有给定初始容量的空字典。
- `Dictionary<K,V>(IEnumerable<KeyValuePair<K,V>> enm)` 创建包含 `enm.elements` 的字典。
- 读写属性 `int Capacity` 获取或设置字典当前容量。如果容量小于元素数量，则抛出 `ArgumentOutOfRangeException`。
- `void AddRange(IEnumerable<KeyValuePair<K,V>> enm)` 将元素添加到字典末尾。
- `IList<KeyValuePair<K,V>> AsReadOnly()` 返回一个对给定列表进行封装的只读列表。
- `int BinarySearch(K key)` 使用二分查找搜索 key。对于 `a[i].CompareTo(key) == 0`，返回索引 `i>=0`；否则返回 `i`，使得 `-i` 为 key 的位置。列表必须排序，或者调用 `Sort(cmp)`；否则结果未定义。
- `int BinarySearch(K key, IComparer<K> cmp)` 工作方式类似，但使用 `cmp.Compare` 比较元素。列表必须排序，或者调用 `Sort(cmp)`；否则结果未定义。
- `int BinarySearch(int i, int n, IComparer<K> cmp)` 工作方式类似，但在索引 `i..(n-1)` 范围内搜索。
- `void CopyTo(int src, KeyValuePair<K,V>[] arr, int dat, int n)` 将从位置 `src` 开始的 `n` 个元素复制到从位置 `dat` 开始的数组 `arr` 中。如果 `src<0` 或 `dat<0` 或 `n<0`，则抛出 `ArgumentOutOfRangeException`。
- `int IndexOf(K key, int i)` 返回大于或等于 `i` 的元素等于 key 的最小索引；否则返回 -1。如果 `i<0` 或 `i>Count`，则抛出 `ArgumentOutOfRangeException`。
- `int IndexOf(K key)` 返回大于 0 且小于 `Count` 的元素 `key` 的最小索引；另外两个重载与 `IndexOf` 类似，但在元素等于 `key` 时返回比最小索引更大的索引。
- `void RemoveRange(int i, int n)` 移除范围 `i..(n-1)` 中的元素。
- `void Reverse()` 反转列表顺序。
- `void Reverse(int i, int n)` 反转 `i..(n-1)` 范围内的元素。
- `void Sort()` 使用快速排序排序列表，使用它们的 `CompareTo` 方法比较元素。列表元素必须实现 `IComparable<T>`。排序是不稳定的。
- `void Sort(IComparer<K> cmp)` 使用 `cmp.Compare` 比较元素并排序列表。
- `void Sort(int i, int n, IComparer<K> cmp)` 排序索引为 `i..(n-1)` 的片段。
- `KeyValuePair<K,V>[] ToArray()` 返回一个包含列表元素的新数组。
- `void TrimSize()` 将列表的容量缩小到实际元素数量。

# 27.8 `KeyValuePair<K,V>` 结构体

泛型 `KeyValuePair<K,V>` 结构体持有来自字典（第 27.5 节和 27.7 节）的键值对或条目。参见示例 221。`KeyValuePair<K,V>` 结构体具有以下方法：

- `KeyValuePair(K k, V v)` 创建 k 和 v 的值对。
- 只读属性 `K` 返回键值对中的键。
- 只读属性 `V` 返回键值对中的值。

# 27.9 `ISet<T>` 接口和 `HashSet<T>` 及 `SortedSet<T>` 类

泛型接口 `ISet<T>` 继承自 `IEnumerable<T>` 并描述不包含重复元素的集合（即集合）。该接口由 `HashSet<T>` 和 `SortedSet<T>` 类实现，它们都具有 `Add`、`Contains` 和 `Remove` 方法的实现；参见第 18 页。有序集合的枚举（第 27.2 节）按增加顺序产生元素。哈希集合按任意顺序产生元素。

`ISet<T>` 接口支持操作，每个操作接受一个 `IEnumerable<T>` 类型的参数 B。修改集合 A 的有 `ExceptWith(集合差, A\B)`、`IntersectWith(集合交集, A∩B)`、`SymmetricExcept(对称差, (A\B)∪(B\A))` 和 `Union(集合并集)`。

返回 bool 且不修改集合 A 的有 `IsProperSubset(A ⊂ B)`、`IsProperSuperset(A > B)`、`IsSubsetOf(A ⊆ B)`、`IsSupersetOf(A ≥ B)`、`Overlaps(A∩B ≠ 0)` 和 `Equals(A = B)`.

# 通用集合：集合、列表和字典

## 示例 229 简单的字典操作

当使用索引器 `dict[k]` 获取字典中不存在的键的值时，会抛出 `ArgumentException`。当使用它来设置键的值时（如 `dict[k]=`），无论该键是否已在字典中，操作都会成功。

```csharp
Dictionary<String, int> dict = new Dictionary<String, int>();

dict.Add("Sweden", 46); dict.Add("Germany", 49);

dict["Japan"] = 81; // 新条目，无异常

Console.WriteLine(dict.Keys); // Japan Germany

Console.WriteLine(dict.Count); // 3

Console.WriteLine("Greece"); // ArgumentException

dict.Add("Germany", 49); // ArgumentException

bool b1 = dict.Remove("Greece"); // False (但不抛异常)

bool b2 = dict.Remove("Japan"); // True

Console.WriteLine(dict.Keys); // Sweden Germany

bool b3 = dict.Contains("Germany"); // True

dict["Sweden"] = 45; // 无异常

Console.WriteLine("Sweden"); // 45
```

## 示例 230 快速集合成员测试：使用 Hash Set 还是二分搜索？

为了从示例 225 的文件索引中排除关键字（第 2 节），需要一种快速识别名称的方法。`IsKeyword` 方法使用一个由 77 个元素的 C 关键字数组构建的 `HashSet`，而 `IsKeyword2` 方法在排序后的数组中进行二分搜索。在这种情况下，`HashSet` 的速度比二分搜索快十倍以上。

```csharp
static readonly string[] keywordarray = 
{ "abstract", "as", "base", "bool", "break", "byte", ..., "while" };

static readonly HashSet<string> keywords = new HashSet<string>();

static bool IsKeyword(string id) { return keywords.Contains(id); }

static bool IsKeyword2(string id) { return Array.BinarySearch(keywordarray, id) >= 0; }
```

## 示例 231 将集合作为字典的键

将非确定性有限自动机 (NFA) 转换为确定性有限自动机 (DFA) 的标准算法创建了整数集合的复合状态。最好是将复合类型替换为整数。该方法接受复合状态集合作为参数，并返回一个重命名器，该重命名器将复合状态映射到示例 226 中的 `Set<int>`，从而将基于元素的哈希值映射到简单的状态名（一个 `int`）。

```csharp
static Dictionary<Set<int>, int> MkRenamer(ICollection<Set<int>> states) {
    IDictionary<Set<int>, int> renamer = new Dictionary<Set<int>, int>();
    int count = 0;
    foreach (Set<int> k in states)
        renamer.Add(k, count++);
    return renamer;
}
```
