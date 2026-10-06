

## 表 6-1 内置字符串比较器

| 名称 | 描述 |
| :--- | :--- |
| CurrentCulture | 使用当前文化的单词比较规则进行区分大小写的字符串比较。当前文化由 `System.Threading.CurrentThread.CurrentCulture` 属性决定。 |
| CurrentCultureIgnoreCase | 使用当前文化的单词比较规则进行区分大小写的字符串比较。当前文化由 `System.Threading.CurrentThread.CurrentCulture` 属性决定。 |
| InvariantCulture | 使用不变文化（invariant culture）的单词比较规则进行区分大小写的字符串比较。 |
| InvariantCultureIgnoreCase | 使用不变文化的单词比较规则进行不区分大小写的字符串比较。 |
| Ordinal | 区分大小写的顺序字符串比较。 |
| OrdinalIgnoreCase | 不区分大小写的顺序字符串比较。 |

## 何时使用 CURRENTCULTURE 和 INVARIANTCULTURE

除了担心区分大小写的字符串比较之外，考虑所比较字符串的文化敏感性以及比较结果如何显示给用户也是关重要的。
微软在 MSDN 上提供了相关指南（参见 http://msdn.microsoft.com/en-us/library/kzcwbcsc.aspx），这些指南通常指出：如果排序结果要显示给终端用户，则应使用文化敏感排序（即以 `CurrentCulture` 开头的内置比较器，例如在列表框中对项目排序）。在内部比较字符串时，应使用不区分种的比较（即以 `InvariantCulture` 开头的内置比较器），并且字符串比较的结果不应依赖于终端用户的文化设置，例如在将文件中的 XML 标记与应用程序处理所需的标记进行比较时。

## 构建和使用自定义的 EqualityComparer 类型

在第 4 章的“指定你自己的键比较函数” 节中，你首先看到了通过编写自定义的等效性比较器类型来自定义 LINQ 评估对象等效性的方法。作为一个示例，我们编写了一个自定义比较类型，根据古老的读音比较算法 Soundex 来解析等效性。`SoundexEqualityComparer` 的代码如列表 4-5 所示，除了用于分组扩展方法外，同一个等效性比较器还可以用于 LINQ 集合运算符。例如，列表 6-7 显示了如何使用 Soundex 算法来确定名称列表中存在多少个不同的读音名称。以下代码将正确返回控制台文本：`Number of unique phonetic names = 4`。

## 列表 6-7 使用自定义等效性比较器配合 Distinct 

```csharp
// 查找列表中读音相同的常用名称数量
string[] names = new string[] { "Janet", "Janette", "Joanne","Jo-anne", "Johanne", "Katy", "Katie","Ralph", "Ralphe" };

var q = names.Distinct(
    new SoundexEqualityComparer());

Console.WriteLine("Number of unique phonetic names = {0}",
    q.Count());
```

## HashSet<T> 类

`HashSet<T>` 在 .NET Framework 3.5 中作为 `System.Collections.Generic` 命名空间的一部分引入。`HashSet` 是一个包含唯一元素的无序集合，并提供了一系列标准的集合运算符，如交集和并集（更多）。它具有标准的集合操作 `Add`（尽管此方法返回布尔值，表示元素是否已于集合中）、`Remove` 和 `Contains`，但由于它使用基于哈希的实现来实现对象标识，这些操作可以直接访问，而不需要像 `List<T>` 集合那样遍历整个列表，其复杂度为 O(1) 而非 O(n)。

虽然 `HashSet` 上的运算符似乎与 LINQ 集合运算符 `Intersect` 和 `Union` 重叠，但这些 `HashSet` 实现会修改被调用时的的集合，而不是像 LINQ 运算符那样返回一个新的 `IEnumerable<T>` 集合。

出于此原因，`HashSet` 运算符的名称被区分为 `IntersectWith` 和 `UnionWith`，而 LINQ 运算符也可以在 `HashSet` 集合上作为 `Intersect` 和 `Union` 使用。这种命名区分避免了冲突，并允许在特定情况下选择所需的行为。
`HashSet` 实现了 `IEnumerable<T>` 模式，因此可以用于 LINQ 查询。列表 6-8 展示了如何在通过合并两个集合生成的 `HashSet` 中查找偶数。该示例的控制台输出见输出 6-6。

## 列表 6-8 针对 HashSet 集合的 LINQ 查询——参见输出 6-6

```csharp
int[] first = new int[] { 1, 2, 3 };
int[] second = new int[] { 3, 4, 5 };

// 通过与第二个集合合并来修改当前集合。
HashSet<int> set = new HashSet<int>(first);
set.Union(second);

// 仅返回集合中的偶值。
// HashSet 中的值是 IEnumerable<T>。
var q = from i in set
    where i % 2 == 0
    select i;

foreach (var item in q)
    Console.WriteLine(item);
```

## 输出 6-6

2
4

`HashSet` 与 LINQ 运算符支持之间的差异在此列出（如 Visual Studio 文档所示），尽管如表 6-2 所示和在列表 6-9 中实现，构建 LINQ 等效近似值是很容易的。

## 表 6-2 LINQ 集合运算符与 HashTable 类型方法的比较

| HashSet<T> 运算符 | LINQ 等效运算符 | 描述 |
| :--- | :--- | :--- |
| UnionWith | Union | 两个集合中的所有所有唯一元素。 |
| IntersectWith | Intersect | 仅位于两个集合中的元素。 |
| ExceptWith | Except | 第一个集合中的元素，但第二个集合中列出的除外。 |
| 无需操作，因为唯一元素可以添加到 HashSet<T> 中 | Distinct | 从集合中删除重复元素。HashSet 不允许向集合添加重复元素，因此它没有等效的 Distinct 运算符。 |
| SymmetricExceptWith | 未提供。要用 LINQ 模拟相同结果，按以下方式组合两个互补的 Except 运算符：a.Except(b).Concat(b.Except(a)); | 返回出现在任一集合中但不同于两者的元素。这是集合的异或操作。 |
| Overlaps | 未提供。要用 LINQ 模拟相同结果，确定与第二个集合的交集，如果有任何结果，则按以下方式返回 true：b.Intersect(a).Distinct().Any(); | 如果给定集合中的任何元素出现在第二个集合中，则返回布尔值 true。 |

## 表 6-2 LINQ 集合运算符与 HashTable 类型方法的比较

| HashSet<T> 运算符 | LINQ 等效运算符 | 描述 |
| :--- | :--- | :--- |
| IsSubsetOf | 未提供。要用 LINQ 模拟相同结果，如果与第二个集合的交集计数等于集合中唯一元素的计数，则按以下方式返回布尔值 true：
```csharp
var aCount =
 a.Distinct().Count();
var intersectCount =
  a.Intersect(b)
  .Distinct()
  .Count();
return intersectCount == aCount;
``` | 如果给定集合中的所有元素存在第二个集合中，则返回布尔值 true。如果集合共享相同的元素，将返回布尔值 true。 |
| IsProperSubsetOf | 未提供。要用 LINQ 模拟相同结果，如果与第二个集合的交集计数小于第二个集合唯一元素的计数，且交集计数等于集合中唯一元素的计数，则按以下方式返回布尔值 true：
```csharp
var aCount =
 a.Distinct().Count();
var bCount =
 b.Distinct().Count();
var intersectCount =
  a.Intersect(b)
  .Distinct()
  .Count();
return (intersectCount < bCount) && (intersectCount == aCount);
``` | 如果给定集合中的所有元素存在第二个集合中，则返回布尔值 true。如果元素完全相同，将返回布尔值 false；集合必须是真正的子集，其元素数量至少比第二个集合少一个。 |

