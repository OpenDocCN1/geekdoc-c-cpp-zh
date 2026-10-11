
```csharp
public static decimal Sum<TSource>(
    IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate, TSource, TAccumulate> func,
    Func<TAccumulate, TResult> resultSelector);
```

# 转换操作符—更改类型

## Count 与 LongCount 的优化

`Count` 和 `LongCount` 的第二个重载版本接受过滤器谓词作为参数，这允许你计算通过该函数返回布尔值 `true` 的元素数量。例如，要统计整数数组中能被十整除的整数个数，可以使用以下代码，结果为 `214,748,364`：

```
var nums = Enumerable.Range(1, int.MaxValue);
var q3 = nums.Count(i => i % 10 == 0);
```

`Count` 操作符对实现了 `ICollection<T>` 接口的序列进行了优化。实现此接口的集合支持自身的 `Count` 属性，并且避免了通过遍历其底层集合来返回计数。对于这些集合，`Count` 返回 `source.Count` 的结果。当使用指定谓词的重载时，这种优化是无法可能的；为了应用谓词函数，无法避免对序列进行完整的循环。

# LINQ TO OBJECTS 是否具有内置性能优化？

来自微软的 Alexandra Rusina 写的一篇有趣的博客详细介绍了内置在标准查询操作符和 LINQ to Objects 提供程序中的性能优化。它详细阐述了 `IList` 和 `ICollection` 测试如何允许某些操作符实现更快的执行。

这些信息可以在 `http://blogs.msdn.com/csharpfaq/archive/2009/01/26/does-the-linq-to-objects-provider-have-built-in-performance-optimization.aspx` 找到。

# 转换操作符—更改类型

LINQ to Objects 有许多操作符，可以对序列中的元素以及序列本身进行类型转换。这对于访问从一个集合类型到某个特定实例方法，或者访问元素的实例属性来说通常是必要的。

## AsEnumerable 操作符

`AsEnumerable` 操作符更改源序列的编译类型，将序列或集合转换回 `System.Collections.Generic.IEnumerable<T>`。这允许控制将调用哪种 LINQ 提供程序，并在选择 LINQ 提供程序时被广泛使用——最常见的情况是当选择在内存中执行部分 LINQ to SQL 查询，而不是在数据库中执行时。这种技术在第 9 章中得到了演示，它用于将查询分割为顺序和并行实现。

`AsEnumerable` 只有一个具有以下方法签名的重载：

```
// 返回作为 IEnumerable<T> 的序列。
public static IEnumerable<TSource> AsEnumerable<TSource>(this IEnumerable<TSource> source);
```

为了演示此操作符，以下示例代码创建一个名为 `list` 的 `List<int>`，然后使用 `AsEnumerable` 操作符将此集合转换为 `IEnumerable<int>`。图 5-1 显示了 Visual Studio 2010 中的 Intellisense 弹出窗口。所有实例方法和扩展方法在 `list` 实例上都可用。图 5-2 显示该集合应用了 `AsEnumerable` 操作符，它被强制转换为 `IEnumerable<T>` 类型，且只有扩展方法可用，`List<T>` 的实例属性 `Count` 除非被转换回 `ICollection<int>` 或 `List<int>`，否则将不再可见。

```
List<int> list = new List<int> { 1, 2, 3, 4, 5 };
// enumerable 将是编译时类型
// 作为一个 IEnumerable<T>
IEnumerable<int> enumerable = list.AsEnumerable();

List<int> list = new List<int> { 1, 2, 3, 4, 5 };
// <List<int>>
// enumerable 但是
// Count
// Count
Iumerable LongCount() enumerable();
list.Count
```

图 5-1 Visual Studio 2010 中 `List<T>` 的 Intellisense。注意除了扩展方法 `Count()` 之外的 `Count` 实例属性。

| `List<int> list = new List<int> {1, 2, 3, 4, 5};` |
| :--- |
| // enumerable <Ctrl-Alt-Space> |
| // 编译时类型 |
| `IEnumerable<int> enumerable = list.Count;` |

**图 5-2** 通过调用 `AsEnumerable()` 操作符创建的 `IEnumerable<T>` 的 Visual Studio 2010 Intellisense。注意 `Count` 实例属性已无法访问。

证明 `IList<T>` 可索引路径，然后在集合上调用 `AsEnumerable()`，以便编写执行原始 `IEnumerable<T>` 路径的测试，该路径无法从通过索引访问元素中受益。

## Cast 操作符

`Cast` 操作符将非泛型 `IEnumerable` 集合中的所有元素产生给类型。这主要是为了适应 .NET 1.0 风格的集合，它们早于 .NET Framework 2.0 的泛型类型特性，例如 `ArrayList` 集合，它以 `object` 类型持有引用。如果元素类型无法转换为新类型，则会抛出 `System.InvalidCastException`。

```
// 将 IEnumerable 集合转换为
// IEnumerable<T>。无法转换为新类型，
// 将抛出 InvalidCastException。
public static IEnumerable<TResult> Cast<TResult>(this IEnumerable source);
```

为了演示使用 `Cast<T>` 操作符，以下代码初始化了一个非泛型的 `ArrayList` 集合。在 .NET Framework 1.0 中引入。该集合仅可以使用几个操作符，并可以访问所有 LINQ 标准查询操作符，这些操作符需要如图 5-6 所示使用 `Cast` 操作符。

### 列表 5-6 针对 .NET 1.0 `ArrayList` 类型的 LINQ 查询示例，该类型实现了 `IEnumerable<T>`

```
ArrayList list = new ArrayList();
list.Add(1);
list.Add(2);
list.Add(3);

// ArrayList 未实现 IEnumerable<T>
// 意味着无法对集合实例访问
// LINQ 操作符，直到使用 Cast<T> 转换集合。
// 转换为 IEnumerable<int>
var avg = (from i in list.Cast<int>()
           where i < 3
           select i).Average();
```

## OfType 操作符

`OfType` 操作符根据给定的类型过滤集合中的元素。这在许多类型的应用程序中都很常见，例如在绘图程序中，集合中的每个元素可以是不同的“形状”类型，这些类型继承自一个基类，如下代码所示：

```
public class Shape { }
public class Rectangle : Shape { }
public class Circle : Shape { }
```

`OfType` 操作符允许你对持有所有形状的集合编写查询，并根据子类型 `Rectangle` 或 `Circle` 进行隔离。列表 5-8 演示了如何将集合元素限制为特定类型，这将返回源集合中 `Rectangle` 的数量。

### 列表 5-8 `OfType` 操作符可以根据其类型过滤集合元素

```
List<Shape> shapes = new List<Shape> {
new Rectangle(),
new Circle(),
new Rectangle(),
new Circle(),
new Rectangle() };
```

```
var q = from rect in shapes.OfType<Rectangle>()
           select rect;
```

`Console.WriteLine("Number of Rectangles = {0}", q.Count());`

## ToArray 运算符

`ToArray` 运算符从任何 `IEnumerable<T>` 序列返回给定类型的数组 `<T>`。使用此运算符最常见的原因是强制立即执行查询，以便将结果数据捕获为快照。

`ToArray` 只有一个重载，其方法签名如下：

```csharp
// 从 System.Collections.Generic.IEnumerable<T> 
// 返回类型为 T 的数组。
public static TSource[] ToArray<TSource>(
    this IEnumerable<TSource> source);
```

为了演示 `ToArray` 运算符的使用，列表 5-9 在 `IEnumerable<int>` 序列上执行查询，并将结果捕获在 `int[]` 数组中。

### 列表 5-9 `ToArray` 运算符枚举 `IEnumerable<T>` 序列并将结果返回数组

```csharp
IEnumerable<int> data = Enumerable.Range(1, 5);

int[] q = (from i in data
    where i < 3
    select i).ToArray();

Console.WriteLine("Returns {0}, {1}",
q[0], q[1]);
```

## ToDictionary 运算符

`ToDictionary` 运算符将 `IEnumerable<TValue>` 序列转换为 `Dictionary<TKey, TValue>` 集合。`System.Collections.Generic.Dictionary<TKey, TValue>` 集合类型维护键值对列表，并确保每个键都是唯一的。如果在转换过程中尝试插入重复键，将抛出 `System.ArgumentException`。

`Dictionary` 集合允许根据键值高效访问元素，如果代码频繁需要根据键值查找元素，那么将序列转换为字典是提高查找性能的一种方法。

`ToDictionary` 运算符有四个方法重载。

```csharp
// 为序列中的元素创建字典
// 键选择器函数返回的键值必须是唯一的，
// 否则将抛出 System.ArgumentException。
// 使用 EqualityComparer<TSource>.Default 
// 比较键的唯一性。
public static Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector);
```

```csharp
// 为序列中的元素创建字典
//并将元素投影到新类型。
// 键选择器函数返回的键值必须是唯一的，
// 否则将抛出 System.ArgumentException。
// 使用 EqualityComparer<TSource>.Default 
// 比较键的唯一性。
public static Dictionary<TKey, TElement> ToDictionary<TSource, TElement>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TSource, TElement> elementSelector);
```

```csharp
// 为序列中的元素创建字典
// 键选择器函数返回的键值必须是唯一的，
// 否则将抛出 System.ArgumentException。
// 使用比较器测试键的唯一性。
public static Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    IComparer<TKey> comparer);
```

```csharp
// 为序列中的元素创建字典
//并将返回的元素投影到新类型。
// 键选择器函数返回的键值必须是唯一的，
// 否则将抛出 System.ArgumentException。
// 使用比较器测试键的唯一性。
public static Dictionary<TKey, TElement> ToDictionary<TSource, TElement>(
    this IEnumerable<TSource> source,
    Func<TSource, TKey> keySelector,
    Func<TSource, TElement> elementSelector,
    IComparer<TKey> comparer);
```

为了演示 `ToDictionary` 运算符的使用，列表 5-10 根据姓氏和名字的组合作为键创建了一个示例联系人的字典，允许通过名称高效查找联系人。

### 列表 5-10 `ToDictionary` 运算符为序列中的元素创建字典

```csharp
List<Contact> contacts = Contact.SampleData();

// 将结果实例化为字典
Dictionary<string, Contact> conDictionary = 
contacts.ToDictionary<Contact, string>(
    c => c.LastName + c.FirstName);

// 所有联系人记录现在都在字典中
// 通过键查找记录 = 非常高效
Contact record = conDictionary["Kamph" + "Mack"];

Console.WriteLine("Kamph DOB = {0}", record.DateOfBirth);
```

## ToList 运算符

`ToList` 运算符从任何 `IEnumerable<T>` 序列返回 `System.Collections.Generic.List<T>`。使用此运算符最常见的原因是强制立即执行查询，以便将结果数据捕获为快照。

`ToList` 只有一个重载，其方法签名如下：

```csharp
// 从 System.Collections.Generic.IEnumerable<T> 
// 返回 System.Collections.Generic.List<T>。
public static List<TSource> ToList<TSource>(
    this IEnumerable<TSource> source);
```

为了演示 `ToList` 运算符的使用，列表 5-12 在 `IEnumerable<int>` 序列上执行查询，然后使用 `ForEach` 方法将结果写入 `List<T>` 并输出到控制台窗口。

### 列表 5-12 `ToList` 运算符枚举 `IEnumerable<T>` 序列并将结果返回 `List<T>`

```csharp
IEnumerable<int> data = Enumerable.Range(1, 5);

// 查询并捕获结果到 List<int>
List<int> q = (from i in data
    where i < 3
    select i).ToList();

// ForEach 是 List<T> 的方法
q.ForEach(j => Console.WriteLine(j));
```

## ToLookup 运算符

`ToLookup` 运算符在第 4 章“数据分组与连接”中首次介绍，它用于促进两个序列之间非常高效的一对多连接。`ToLookup` 根据共享相同键值的元素创建子序列。`ToLookup` 在规模和行为上与 `ToDictionary` 相似，区别在于它们如何处理具有相同键值的重复元素。`ToLookup` 允许给定键值对应多个元素，而 `ToDictionary` 在发生这种情况时会抛出异常。

`ToLookup` 算符可用的方法签名如下：
