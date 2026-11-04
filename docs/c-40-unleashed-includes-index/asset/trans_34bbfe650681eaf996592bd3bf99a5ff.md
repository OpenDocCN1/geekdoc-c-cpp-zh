
![](img/a16f85e62ce9bdc527f4b09dbfe26092_794_0.png)

图 16.6 LinkedList<T> 和 LinkedListNode<T> 中的引用。

这里展示了一个创建和操作列表的示例：

```csharp
var lst = new LinkedList<string>();

var elem1 = lst.AddFirst("isn't");
var elem2 = lst.AddBefore(elem1, "This");
var elem3 = lst.AddAfter(elem1, "a");
var elem4 = lst.AddLast("list");
var elem5 = lst.AddBefore(elem4, "singly");
var elem6 = lst.AddAfter(elem5, "linked");

lst.Last.Previous.Previous.Value = "doubly";
lst.First.Next.Value = "is";

foreach (var word in lst)
    Console.Write(word + " ");

Console.WriteLine();
```

请注意，所有操作列表的操作都通过 LinkedList<T> 类型进行。这使得列表能够以一致的方式维护列表结构，保持所有 Next 和 Previous 引用处于良好状态。同样地，在第一个元素前添加一个元素需要将 First 引用更新为指向列表新的“头部”。在最后一个元素后添加一个元素需要更新 Last 引用。

手动通过跟踪 Next 或 Previous 引用遍历列表时，请注意列表不是循环的。空引用表示已到达列表的末尾或开头。换句话说，First.Previous 和 Last.Next 将始终返回 null。

### 破损集合初始化器的案例

`LinkedList<T>` 不支持方便的 C# 3.0 集合初始化器语法。查看该类型的接口实现列表，你可能会认为它应该支持；毕竟它实现了 `ICollection` 接口，而该接口上有一个 `Add` 方法，对吧？然而，该集合类型显式实现了该接口，从而使 `Add` 方法在类本身上为私有。因此，编译器找不到可用于集合初始化器的 `Add` 方法来调用。不过以下方法可行：

```csharp
var lst = new LinkedList<string>();
((ICollection<string>)lst).Add("Hello"); // calling through the interface
```

因此，集合初始化器在发现 `Add` 方法方面的鸭子类型特性有时（但很少）会与该功能相悖。

## `Dictionary<TKey, TValue>`

为了提供 `Hashtable` 的泛型类型替代方案，发明了 `Dictionary<TKey, TValue>` 类型。`Hashtable` 对其键和值都使用 `System.Object`，而泛型字典允许键和值的静态类型化。让我们再次交叉翻译我们的原始示例：

```csharp
var tbl = new Dictionary<string, int>();
tbl.Add("Bart", 26);
tbl["John"] = 62;

bool bartIsKnown = tbl.ContainsKey("Bart");
bool someIsAged62 = tbl.ContainsValue(62);
foreach (var name in tbl.Keys)
    Console.WriteLine("Age of {0} is {1}", name, tbl[name]);

tbl.Remove("Bart");
```

代码看起来仍然完全相同，这要归功于与 `Hashtable` 相比的镜像 API 设计。这使得有 `Hashtable` 使用经验的人能够立即在泛型字典的世界中感到宾至如归。明显的差异是你不能再犯任何类型错误了。这在图 16.7 中再次得以说明，同时也展示了 IntelliSense 如何引导你走向正确的方向。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_796_0.png)

图 16.7 泛型强制执行的更强类型检查。

请注意示例如何为 foreach 循环的迭代变量使用隐式类型局部变量。由于泛型周围的所有类型信息在编译时已知，正如出色的 IntelliSense 体验所证明的那样，编译器可以静态推断循环变量的类型应该是什么。这在图 16.8 的代码编辑器检查中得到了证明。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_796_1.png)

图 16.8 编译时可用的丰富类型信息。

顺便说一下，直接遍历字典类型（而不是单独遍历键或值）也是可能的。通过查看泛型类型的定义，你可以追踪这是为什么：

```csharp
public class Dictionary<TKey, TValue> : IDictionary<TKey, TValue>, ...
```

从这里，我们进入 IDictionary<TKey, TValue> 泛型接口，进而引向 ICollection 泛型接口：

```csharp
public interface IDictionary<TKey, TValue> :
    ICollection<KeyValuePair<TKey, TValue>>
```

这里事情变得更有趣了：ICollection<T> 接口使用 KeyValuePair<TKey, TValue> 泛型类型作为参数。但首先，让我们通过跟踪 ICollection<T> 轨迹来完成对泛型字典可枚举性质的追踪：

```csharp
public interface ICollection<T> : IEnumerable<T>
```

为了结束这次类型追踪练习，我们发现了每个泛型字典类型如何实现 IEnumerable<T>，其中 T 被替换为 KeyValuePair 泛型构造类型。KeyValuePair<TKey, TValue> 的定义如下：

```csharp
public struct KeyValuePair<TKey, TValue> {
    public KeyValuePair(TKey key, TValue value);

    public TKey Key { get; }
    public TValue Value { get; }
}
```

基于这一观察，我们也可以按如下方式遍历字典，使用 Key 和 Value 属性提取名称和年龄值：

```csharp
foreach (var entry in tbl)
    Console.WriteLine(entry.Key + " is " + entry.Value);
```

再一次，局部变量类型推断确切地知道我们在谈论什么，如图 16.9 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_797_0.png)

图 16.9 IDictionary<TKey, TValue> 是 IEnumerable<KeyValuePair<TKey, TValue>>。

## 隐式类型局部变量

虽然隐式类型局部变量或使用 var 关键字的局部变量类型推断主要是为了与匿名类型一起使用而引入的，但其用途远不止于此。泛型（集合）类型是类型推断可以证明在减少代码冗余方面非常有用的地方之一。使用泛型类型，可以在短时间内构造大型类型名称：

```csharp
Dictionary<string, List<int>> personLottoNumbers
    = new Dictionary<string, List<int>>();
```

简单对象的实例化甚至不再适合一行，因为类型必须声明两次。尽管一些程序员将 var 关键字视为披着羊皮的狼，但很难否认以下写法更简洁：

```csharp
var personLottoNumbers = new Dictionary<string, List<int>>();
```

你丢失了类型信息吗？没有。代码更简洁吗？是的。如果问我，这就是双赢的局面。

当谈论这种集合类型时，我们应该检查的最后一个方法是方便且自解释的 TryGetValue 方法：

```csharp
int ageOfMarge;
if (tbl.TryGetValue("Marge", out ageOfMarge))
    // Code if the key was found, with ageOfMarge set to the retrieved value.
```

泛型字典类型与 Hashtable 类型一样，基于哈希以提供通过键高效查找条目。这意味着关于为键类型提供良好的哈希函数以及确保键值不可变性的相同注意事项同样适用。

Hashtable 类型直接使用 System.Object 的 GetHashCode 和 Equals 虚方法进行键对象存储，而泛型字典类型通过 IEqualityComparer<T> 接口引入了另一个抽象层：

```csharp
public interface IEqualityComparer<in T> {
    bool Equals(T x, T y);
    int GetHashCode(T obj);
}
```

尽管可以为泛型字典构造函数提供自定义相等比较器实现，但通常依赖于使用默认的 EqualityComparer<T>。它在内部使用 System.Object 虚方法，以与非泛型 Hashtable 集合类型使用的默认行为保持一致。使用自定义相等比较器可以派上用场，以覆盖键类型关于哈希码计算和相等性检查的默认行为（例如，实现不区分大小写的键区分）。这在 .NET Framework 中已通过 StringComparer 类型完成：

```csharp
var ages = new Dictionary<string, int>(StringComparer.CurrentCultureIgnoreCase)
{
    { "Homer", 38 },
    { "Bart", 10 }
};
Console.WriteLine(ages["bart"]); // different casing, still works
```
