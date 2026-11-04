

```
string ageString;
int age;
do
{
    Console.Write("Enter your age: ");
    ageString = Console.ReadLine();
}
while (!int.TryParse(ageString, out age));

Console.WriteLine("Your age is {0}.", age);
```

在这段代码中，我们还使用格式字符串的概念将获取到的年龄输出到屏幕上。我们将在后面的“格式化文本”一节中更详细地讨论这个框架特性。目前，只需将 {0} 视为传递给 WriteLine 的第一个 params 数组元素的占位符即可。

由于当今的软件环境受到全球化的影响，从文本中解析值并不是在世界各地都能以统一方式奏效的事情。数字、日期等值的文本形式高度依赖于用户的文化。软件的恰当全球化本身就是一个独立主题，已有整本书专门讨论该主题，因此我们将只限于一个处理不同数字样式的基本示例。用于处理数字的核心枚举称为 NumberStyles，定义在 System.Globalization 命名空间中。它是一个支持使用标志的枚举，因此可以组合样式。图 26.12 展示了该枚举的值。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1331_0.png)

图 26.12 NumberStyles 枚举的值。

一个例子是 AllowThousands 标志，它指定可以使用千位分隔符。与 AllowDecimalPoint 结合使用时，字符串 87,654.32 在英语中是有效的数字字符串。该枚举中的一些值只是将标志组合成一个方便的

```
Console.Write("Enter your salary: ");
salaryString = Console.ReadLine();
}
while (!decimal.TryParse(salaryString, NumberStyles.Currency,
    new CultureInfo(culture), out salary));

Console.WriteLine("Your salary is {0}.", salary);
```

下面是一些示例输入和输出，清楚地展示了根据区域性不同，解析我们的输入可能会失败：

输入你的区域性：en-US
输入你的薪资：87,654.32
你的薪资是 87654.32。

输入你的区域性：en-US
输入你的薪资：87.654,32
输入你的薪资：

输入你的区域性：nl-BE
输入你的薪资：87.654,32
你的薪资是 87654.32。

注意所有 WriteLine 调用的输出都是相同的。稍后你将看到我们如何影响字符串格式化，使其遵循特定的区域性设置。事实上，解析和格式化或多或少可以看作互逆函数。

## 特殊值

大多数基元类型都有一些与该类型领域内在相关的特殊值。例如，整数数据类型具有特定范围，其边界可以使用 MinValue 和 MaxValue 等常量字段获取：

```
Console.WriteLine("32-bit signed integers range from {0} to {1}.",
    int.MinValue, int.MaxValue);
```

对于浮点数，还存在其他特征值，例如由除以零等情况产生的 NaN（非数字）值，以及 IEEE 浮点数规范中定义的无穷大值：

显然，这些字段是只读的或常量，由 BCL 和运行时填充。有关 const（例如用于 int.MaxValue）和只读（例如用于 DateTime.MinValue）之间区别的更多信息，请参阅第 11 章“字段、属性和索引器”中关于字段的讨论。

## 使用关键字还是类型名称？

在前面的示例中，我们一直使用基元类型的 C# 关键字（如 int 和 decimal）来访问静态成员。或者，我们也可以使用与它们对应的类型名称，例如 System 命名空间中的 Int32 和 Decimal。使用哪种风格仅仅是用户偏好问题，两者含义完全相同。

对于有 Java 背景的开发者来说，这起初可能会令人困惑，因为在 Java 中 int 和 Integer 的含义不同：前者表示基元值，而后者用于指代包装此类值的“装箱”引用类型。在 .NET 中，装箱行为与值相对于 object 基类型的使用有关。

## 使用数组

数组是一类常用的类型族，它们实际上是一种类型构造器：给定任意类型，都可以基于它构造数组类型。为了便于执行某些常见操作，存在 System.Array 类型。所有数组都派生自该类型，从而获得一些有用的实例级成员和属性。例如，数组的秩表示维度数：

```
var xs = new int[10];
var ys = new int[3,4];
var zs = new int[3][];
```

对于第一个数组，秩为 1，因为只有一个维度。第二个数组的秩为 2，因为使用了多维数组特性。对于最后一个数组（交错数组），zs 的秩仍然是 1：

```
Console.WriteLine(xs.Rank); // 1
Console.WriteLine(ys.Rank); // 2
Console.WriteLine(zs.Rank); // 1
```

要查找数组不同维度上的有效索引范围，可以使用 GetLowerBound 和 GetUpperBound 等方法。在实践中，它们很少被使用，人们更倾向于使用从零到数组长度减一生成范围的 for 循环，或由 foreach 循环处理所有繁重工作。

在各种情况下，System.Array 上的静态成员更令人感兴趣。以下代码展示了几个示例：

```
var rnd = new Random();
var xs = new int[20];
for (int i = 0; i < 10; i++)
    xs[i] = rnd.Next(10);

Array.Resize(ref xs, 10); // drop last ten, like LINQ's Take
Array.Sort(xs); // in-place quicksort, like LINQ's OrderBy
Array.Reverse(xs); // in-place reversal, like LINQ's Reverse

var ys = new int[10];
Array.Copy(xs, ys, xs.Length); // more overloads available
Array.ForEach(ys, Console.WriteLine); // like a foreach-loop

int fiveAt = Array.BinarySearch(ys, 5); // -1 if not found
bool anyEven = Array.Exists(ys, i => i % 2 == 0); // like LINQ's Any

// Other operations include:
// - TrueForAll (like LINQ's All operator)
// - Find and FindAll (like LINQ's Select operator)
// - Ways to find indexes for an element
```

注意这里代码注释中大量出现了“like LINQ”的说明。从历史角度理解这一点肯定有帮助，因为数组从框架早期就已存在，而 LINQ 对序列运算符的泛化是在 .NET 3.5 中引入的。对于其中一些操作，使用 Array 类型的静态方法与使用 LINQ 运算符之间存在相当大的差异。特别是，许多 Array 方法以就地方式操作数据，而 LINQ to Objects 会生成新序列（基于 `IEnumerable<T>`），不会改变底层数据。此外，Array 方法会基于数组特有的特征（例如高效索引能力以及对数组边界的预先了解）进行大量优化。BinarySearch 和 Sort 之类的方法可以利用这些属性提供非常高效的实现。

## 段

与数组相关的一个相对鲜为人知的类型是 `ArraySegment<T>`，它在 .NET 2.0 中被加入框架。它基本上允许将一个数组与偏移量和长度捆绑在一起。该结构的使用者可以查询这些信息（例如，弄清他们被允许操作数组的哪一部分）：

```
var xs = new[] { 3, 7, 2, 5, 1, 4, 0, 9, 6, 8 };
// ^^^^^^^^
var ys = new ArraySegment<int>(xs, 3, 5);

// Retrieving start and end elements in the segment
var fst = ys.Array[ys.Offset]; // 5
var lst = ys.Array[ys.Offset + ys.Count - 1]; // 9
```

对于对算法感兴趣的读者，一个很好的练习是实现某种递归排序算法，其中排序操作的边界通过 ArraySegment 值来传递。

## 缓冲区

数组表示为连续的内存块，CLR 会根据数组的元素类型知道如何索引到其中。例如，保存 Int32 值的数组每个元素将占用 4 个字节。要访问第五个元素，必须在数组内存中跳过 16 字节的偏移量才能到达该元素。

在本机代码世界中，开发者经常通过计算数组内存中的偏移量，以低级别方式操作数组。此类操作往往会导致大量 bug，并且实际上可能违反内存和类型安全（例如，当访问超出数组边界时）。为了恢复其中一些较低级别的操作技术，可以使用 Buffer 类型，同时保持各种形式的安全性。例如，不能对保存引用的数组使用 Buffer 操作，因为摆弄引用是一种危险行为，应交给垃圾回收器处理。

一个简单操作的示例是获取数组的字节大小：

```
var xs = new[] { 3, 7, 2, 5, 1, 4, 0, 9, 6, 8 };
var len1 = Buffer.ByteLength(xs); // xs.Length * sizeof(int)
var len2 = xs.Length * sizeof(int);
```

掌握这类知识后，你就可以对落在数组边界内的字节进行各种操作。显然，这是一项相当专业化的任务，需要用户了解基元类型在内存中的布局方式。其中一项知识是字节的小端序。下面的示例对一个存储在数组中的 32 位有符号整数的字节进行了一些操作：

```
var xs = new[] { 3, 7, 2, 5, 1, 4, 0, 9, 6, 8 };

byte b1 = Buffer.GetByte(xs, 0); // 3 due to little-endian architecture
byte b2 = Buffer.GetByte(xs, 1); // 0
byte b3 = Buffer.GetByte(xs, 2); // 0
byte b4 = Buffer.GetByte(xs, 3); // 0

Console.WriteLine("{0:X}", xs[0]); // 0x00000003
Buffer.SetByte(xs, 1, 0x42);       //
Buffer.SetByte(xs, 3, 0x17);       // ^^
Console.WriteLine("{0:X}", xs[0]); // 0x17004203
```

这里，数组用于元素的内存中的前 4 个字节由组成第一个元素所用 32 位整数值 3 的字节占据。通过 GetByte 方法，我们实际上可以看到这些字节的原始形式。SetByte 方法会改动这些字节，从而完成右侧注释中突出显示的操作。注意使用了 {0:X} 格式字符串，它将传递给 WriteLine 的第一个 params 数组参数以十六进制格式输出。稍后，我们将更广泛地看到字符串格式化的丰富性。可以说，字符串格式化提供了大量灵活性，远不止在字符串中“打孔”和填充“空洞”。

