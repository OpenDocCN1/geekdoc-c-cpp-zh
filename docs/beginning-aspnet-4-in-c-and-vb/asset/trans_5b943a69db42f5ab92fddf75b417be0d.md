
用于演示 BitArray 类的示例创建了一个包含 8 位、索引从 0 到 7 的位数组。SetAll() 方法将全部 8 位设置为 true。然后 Set() 方法将位 1 更改为 false。除了 Set 方法之外，还可以使用索引器，如索引 5 和 7 所示。

```
var bits1 = new BitArray(8);
bits1.SetAll(true);
bits1.Set(1, false);
bits1[5] = false;
bits1[7] = false;
Console.Write("initialized: ");
DisplayBits(bits1);
Console.WriteLine();
```

这是初始化后位显示的结果：

```
initialized: 10111010
```

Not() 方法生成 BitArray 位的反码：

```
Console.Write(" not ");
DisplayBits(bits1);
bits1.Not();
Console.Write(" not = ");
DisplayBits(bits1);
Console.WriteLine();
```

Not() 的结果是所有位都被反转。如果位为 true，则变为 false；如果位为 false，则变为 true：

```
not 10111010 = 01000101
```

在这里，创建了一个新的 BitArray。使用构造函数，变量 bits1 用于初始化数组，因此新数组具有相同的值。然后将位 0、1 和 4 的值设置为不同的值。在使用 Or() 方法之前，会显示位数组 bits1 和 bits2。Or() 方法会更改 bits1 的值：

```
var bits2 = new BitArray(bits1);
bits2[0] = true;
bits2[1] = false;
bits2[4] = true;
DisplayBits(bits1);
Console.Write(" or ");
DisplayBits(bits2);
Console.Write(" = ");
bits1.Or(bits2);
DisplayBits(bits1);
Console.WriteLine();
```

使用 Or() 方法时，会从两个输入数组中获取已设置的位。在结果中，如果位在第一个或第二个数组中被设置，则该位被设置：

```
01000101 or 10001101 = 11001101
```

接下来，使用 And() 方法对 bits2 和 bits1 进行操作：

```
DisplayBits(bits2);
Console.Write(" and ");
DisplayBits(bits1);
Console.Write(" = ");
bits2.And(bits1);
DisplayBits(bits2);
Console.WriteLine();
```

And() 方法的结果仅在两个输入数组中位都被设置时才设置位：

```
10001101 and 11001101 = 10001101
```

最后使用 Xor() 方法进行异或：

```
DisplayBits(bits1);
Console.Write(" xor ");
DisplayBits(bits2);
bits1.Xor(bits2);
Console.Write(" = ");
DisplayBits(bits1);
Console.WriteLine();
```

使用 Xor() 方法时，结果位仅在位在第一个或第二个输入中被设置但不同时在两者中被设置时才被设置：

```
11001101 xor 10001101 = 01000000
```

## BitVector32

如果您事先知道需要的位数，可以使用 BitVector32 结构代替 BitArray。BitVector32 更高效，因为它是一种值类型，并且将位存储在整数内部的栈上。使用单个整数即可容纳 32 位。如果需要更多位，可以使用多个 BitVector32 值或 BitArray。BitArray 可以根据需要增长；BitVector32 则不行。

下表显示了与 BitArray 非常不同的 BitVector32 成员：

| BitVector32 成员 | 描述 |
|---|---|
| Data | Data 属性以整数形式返回 BitVector32 背后的数据。 |
| Item | 可以使用索引器设置 BitVector32 的值。索引器被重载——您可以使用掩码或类型为 BitVector32.Section 的 section 来获取和设置值。 |
| CreateMask() | CreateMask() 是一个静态方法，可用于为 BitVector32 中的特定位创建掩码。 |
| CreateSection() | CreateSection() 是一个静态方法，可用于在 32 位内创建多个 section。 |

示例代码使用默认构造函数创建一个 BitVector32，其中全部 32 位初始化为 false。然后创建掩码以访问位向量内部的位。第一次调用 CreateMask() 创建用于访问第一位的掩码。调用 CreateMask() 后，bit1 的值为 1。再次调用 CreateMask() 并将第一个掩码作为参数传递给 CreateMask() 会返回用于访问第二位的掩码，其值为 2。bit3 然后具有值 4 以访问第 3 位。bit4 具有值 8 以访问第 4 位。

然后使用索引器和掩码访问位向量内部的位并相应地设置字段：

```
var bits1 = new BitVector32();
int bit1 = BitVector32.CreateMask();
int bit2 = BitVector32.CreateMask(bit1);
int bit3 = BitVector32.CreateMask(bit2);
int bit4 = BitVector32.CreateMask(bit3);
int bit5 = BitVector32.CreateMask(bit4);

bits1[bit1] = true;
bits1[bit2] = false;
bits1[bit3] = true;
bits1[bit4] = true;
bits1[bit5] = true;
Console.WriteLine(bits1);
```

O(n) 表示对于集合中的每个元素都需要相同量的额外时间。`ArrayList` 的 `Add()` 方法在需要重新分配集合时可能为 O(n) 操作。更改容量会导致列表的复制，并且复制所需的时间随每个元素线性增加。

O(log n) 表示操作所需的时间会随着集合中的元素数量增加。但每个元素的增加时间不是线性的而是对数性的。`SortedDictionary<TKey, TValue>` 对集合内部的插入操作具有 O(log n) 行为；`SortedList<TKey, TValue>` 对相同功能具有 O(n) 行为。在这里，`SortedDictionary<TKey, TValue>` 快得多，因为将元素插入树结构比插入列表更有效。

下表列出了集合类及其在添加、插入和删除项目等不同操作上的性能。使用此表您可以为您的用途选择最佳的集合类。左侧列列出集合类。Add 列给出向集合添加项目的计时信息。`List<T>` 和 `HashSet<T>` 类定义 `Add` 方法以向集合添加项目。对于其他集合类，使用不同的方法向集合添加元素；例如，`Stack<T>` 类定义 `Push()` 方法，而 `Queue<T>` 类定义 `Enqueue()` 方法。您也可以在表中找到此信息。

如果单元格中有多个大 O 值，原因是如果集合需要调整大小，调整大小需要一段时间。例如，对于 `List<T>` 类，添加项目需要 O(1)。如果集合的容量不够大并且集合需要调整大小，则调整大小需要 O(n) 时间。集合越大，调整大小操作所需的时间越长。最好通过将集合的容量设置为可以容纳所有元素的值来避免调整大小。

如果单元格内容为 na，这意味着此操作不适用于此集合类型。

| 集合 | 添加 | 插入 | 删除 | 项 | 排序 | 查找 |
|---|---|---|---|---|---|---|
| List\<T\> | O(1) 或如果集合必须调整大小则 O(n) | O(n) | O(n) | O(1) | O(n log n)，最坏情况 O(n\^2) | O(n) |
| Stack\<T\> | Push(), O(1) 或如果栈必须调整大小则 O(n) | 不适用 | Pop(), O(1) | 不适用 | 不适用 | 不适用 |
| Queue\<T\> | Enqueue(), O(1) 或如果队列必须调整大小则 O(n) | 不适用 | Dequeue(), O(1) | 不适用 | 不适用 | 不适用 |
| HashSet\<T\> | Add(), O(1) 或如果集合必须调整大小则 O(n) | 不适用 | O(1) | 不适用 | 不适用 | 不适用 |
| SortedSet\<T\> | Add(), O(1) 或如果集合必须调整大小则 O(n) | 不适用 | O(1) | 不适用 | 不适用 | 不适用 |
| LinkedList\<T\> | AddLast() O(1) | AddAfter() O(1) | O(1) | 不适用 | 不适用 | O(n) |

## 11 语言集成查询

### 本章内容？

- 使用 List\<T\> 对对象进行传统查询
- 扩展方法
- LINQ 查询运算符
- 并行 LINQ
- 表达式树

LINQ（语言集成查询）将查询语法集成到 C# 编程语言内部，使得可以用相同的语法访问不同的数据源。LINQ 通过提供抽象层使此操作成为可能。

本章为您提供 LINQ 的核心基础以及使新功能成为可能的 C# 语言扩展。

> 如果要在数据库中使用 LINQ，您应阅读第 31 章“ADO.NET Entity Framework”。阅读本章后，如需查询 XML 数据，请阅读第 33 章“操作 XML”。

### LINQ 概述

本章从一个简单的 LINQ 查询开始，然后深入 LINQ 的全部潜力。C# 语言提供集成查询语言，该语言被转换为方法调用。本节向您展示转换的外观，以便您可以使用 LINQ 的所有可能性。

#### 列表和实体

本章中的 LINQ 查询将在包含 1950 年至 2008 年一级方程式冠军的集合上执行。这些数据需要使用实体类和列表进行准备。

对于实体，定义了类型 Racer。Racer 定义了多个属性以及一个重载的 ToString() 方法，用于以字符串格式显示一名车手。此类实现了接口
