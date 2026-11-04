
为了说明栈的用法，请看下面的代码片段：

```
var stack = new Stack();
stack.Push(1);
stack.Push(2);
stack.Push(3);
var three = (int)stack.Pop();
var two = (int)stack.Peek();
var twoLeft = stack.Count;
```

与 Queue 类型类似，Stack 在内部使用数组实现。Pop 是常数时间操作，而 Push 的行为取决于可用容量。如果有空闲存储空间，Push 是 O(1)；否则，由于数组需要重新分配，它会变成线性时间。

## BitArray

最后一个值得一提的非泛型集合类型是 BitArray 类型，它提供了高效的位向量实现。使用 Boolean 数组来跟踪某个系统中一组实体的开/关标志，在存储方面并不是很高效，每个 Boolean 都需要整整一个字节（更不用说潜在的 32 位对齐问题）。如果能够以位为单位对标志进行编码，情况就会好得多。BitArray 类型正是为此提供的：

```
const int N = 20;

var first = new BitArray(N, false);
for (int i = 0; i < first.Length; i += 2)
    first[i] = true;

var second = new BitArray(N, false);
for (int i = 1; i < second.Length; i += 2)
    second[i] = true;

Print("First: ", first);            // 101010101010101010
Print("Second: ", second);          // 010101010101010101
Print("Xor: ", first.Xor(second));  // 111111111111111111
```

在内部，BitArray 使用整数数组将 Boolean 值编码为单个位。它提供了 And、Or、Xor 和 Not 等逻辑运算符，并且整个位数组可以作为 Boolean 序列进行迭代：

```
private static void Print(string title, BitArray bitArray) {
    Console.Write(title);
    foreach (bool b in bitArray)
        Console.Write(b ? "1" : "0");
    Console.WriteLine();
}
```

### 为什么 ICloneable 是个笑话

尽管初衷是好的，但由于缺少对预期克隆语义的规范，ICloneable 实际上变得相当无用。Object.MemberwiseClone 被定义为创建浅拷贝：所有字段都会被复制，但不会沿引用继续复制。（只复制引用，而引用所指向的内容不会被克隆。）对于深克隆，被引用的对象也会被克隆。ICloneable 的 Clone 方法没有指定期望哪种类型的克隆，因此它无法作为可靠且明确的契约使用。

## 泛型集合类型

既然我们已经了解了非泛型集合类型，现在是时候使用 System.Collections.Generic 中的泛型集合来改进集合的静态类型化了。使用泛型集合的优势在第 15 章中已被反复指出，包括在元素类型层面于编译时检测类型错误，以及提升性能。

### List<T>

ArrayList 类型的泛型对应物是泛型 List<T> 类型，其中类型参数 T 不出所料地表示元素类型。List<T> 上可用的方法与 ArrayList 上的几乎相同。我们甚至可以轻松地将之前的 ArrayList 示例移植到 List<int>：

```csharp
var lst = new List<int>();
lst.Add(1);                       // {  1 }
lst.AddRange(new[] { 2, 3, 7, 6, 5, 4 }); // {  1, 2, 3, 7, 6, 5, 4 }
lst.Insert(index: 0, item: 0);    // { 0, 1, 2, 3, 7, 6, 5, 4 }
lst.RemoveAt(index: 4);           // { 0, 1, 2, 3,    6, 5, 4 }
lst.Remove(item: 1);              // { 0,    2, 3,    6, 5, 4 }
lst.RemoveRange(index: 2, count: 3); // { 0,    2,          4 }
lst.Reverse();                    // { 4, 2, 0 }
lst.Sort();                       // { 0, 2, 4 }
bool hasTwo = lst.Contains(2);    // true
int two = lst[1];                 // 2
```

### 命名参数？

![](img/a16f85e62ce9bdc527f4b09dbfe26092_791_0.png)

你可能已经注意到，在前面非泛型集合类型的示例中，我有时会使用命名参数。这并不是让上述代码通过编译所必需的，而是作为一种文档形式，说明所用参数的含义。过去，我常常通过内联注释（使用 /* parameter name */）来记录某些参数，但我更喜欢命名参数。

还要注意，某些参数名与 ArrayList 上的参数名不同（特别是 obj 已被替换为 item），以便为 API 用户提供更有意义的名称。在高质量的框架设计中，命名非常重要！

与 ArrayList 相比，List<T> 具有相似的性能特征，这是基于以下事实：底层基于数组的存储可能需要在插入元素时增长。可以通过构造函数重载设置初始容量。

除了上一个示例中展示的熟悉方法外，List<T> 还拥有大量受典型函数式编程技术启发的方法，用于处理集合和数据序列。其中大多数方法依赖于委托，第 17 章“委托”对委托进行了深入介绍。为了说明这些方法，我们使用 lambda 表达式语法，它提供了一种将一段代码传递给方法的简写方式（例如，用于表达筛选条件）：

```
    var lst = new List<int> { 1, 2, 3, 4, 5, 6, 7 };

    // Convert all elements and create a new list.
    List<string> numbers = lst.ConvertAll(n => n.ToString());

    // Condition holds for any element (Exists) or all elements (TrueForAll)?
    bool hasLargerThanFive = lst.Exists(n => n > 5);            // true
    bool noElementsThirteen = lst.TrueForAll(n => n != 13);     // true

    // Find element(s) or indexes.
    int firstEven = lst.Find(n => n % 2 == 0);                  // 2
    int lastEven = lst.FindLast(n => n % 2 == 0);               // 6
    List<int> allOdds = lst.FindAll(n => n % 2 != 0);           // { 1, 3, 5, 7 }
    int indexOfFirstLargerThanThree = lst.FindIndex(n => n > 3); // 3
    int indexOfLastLessThanFive = lst.FindLastIndex(n => n < 5); // 3
```

## 与 LINQ 的重叠

这里展示的许多方法在 LINQ 中被泛化为查询运算符，最初被称为序列运算符。关键区别在于，LINQ 查询运算符作用于序列（即 IEnumerable<T> 对象），这使得它们比仅适用于 List<T> 更具通用性。

然而，还有更多内容：正如你将看到的，大多数 LINQ 查询运算符都是惰性的。这意味着应用查询运算符的结果不会在遍历结果之前计算。例如，List<T> 的 FindAll 方法会立即遍历所有元素，以生成包含筛选结果的新列表对象，但 LINQ 的 Where 方法会延迟计算，直到有人遍历生成的 IEnumerable<T>。这可能是有益的（例如，在以下情况中）：

```
var fiveEvensLazy = lst.Where(n => n % 2 == 0).Take(5);
var fiveEvensEager = lst.FindAll(n => n % 2 == 0).Take(5);
```

在后一种情况下，会为所有偶数创建一个全新的中间 List<int>；而前一行代码是惰性求值的。当我们在第 19 章“语言集成查询精要”中更深入地讨论 LINQ 时，这一点会清楚得多。学习 LINQ 之后，请回到这里，将 List<T> 的方法映射到它们对应的查询运算符上。（例如，FindAll 对应于 Where。）

## LinkedList<T>

LinkedList<T> 是一个双向链表，这意味着可以在常数时间内沿两个方向在连续元素之间导航。链表中的各个元素表示为 LinkedListNode<T> 对象，如下所示：

```
// Illustrating the public contract of the class, omitting implementations.
public sealed class LinkedListNode<T> {
    public LinkedList<T> List { get; }
    public LinkedListNode<T> Next { get; }
    public LinkedListNode<T> Previous { get; }
    public T Value { get; set; }
}
```

使用 Next 和 Previous，你可以沿两个方向遍历链表。要找到包含该节点的链表，请沿着 List 引用查找。LinkedList<T> 本身提供对 First 和 Last 元素的访问：

```
// Illustrating the public contract of the class, omitting implementations.
public class LinkedList<T> {
    public LinkedListNode<T> First { get; }
    public LinkedListNode<T> Last { get; }
}
```

图 16.6 展示了链表与其节点之间所有交叉引用的示意图。

LinkedList<T> 的常见操作包括：向链表头部或尾部添加元素（分别使用 AddFirst 和 AddLast），在给定链表节点之前或之后插入元素，以及移除第一个、最后一个或任意元素。此外还提供了在链表中查找元素并返回对应链表节点的方法，这些方法需要线性时间，因为它们必须遍历链表。

