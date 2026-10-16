

## 摘要

本章介绍了使用不同种类的泛型集合。数组的大小是固定的，但可以使用列表来获得动态增长的集合。若要按先进先出的方式访问元素，可以使用队列；对于后进先出的操作，可以使用堆栈。链表允许快速插入和移除元素，但搜索速度较慢。使用键和值，可以使用字典，它在搜索和插入元素时速度很快。集合（Set）对于唯一项非常有用，可以是有序的（`SortedSet<T>`）也可以是无序的（`HashSet<T>`）。

第12章“特殊集合”将详细介绍一些特殊的集合类。

## 12 特殊集合

### 本章内容

- 使用位数组和位向量
- 使用可观察集合
- 使用不可变集合
- 使用并发集合

### 本章的 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 http://www.wrox.com/go/professionalcsharp6 的 Download Code 标签页中找到。本章代码分为以下几个主要示例：

- BitArray 示例
- BitVector 示例
- 可观察集合示例
- 不可变集合示例
- 管道示例

### 概述

第11章“集合”介绍了列表、队列、堆栈、字典和链表。本章继续介绍特殊集合，例如处理位的集合、更改时可被观察的集合、不可更改的集合，以及可从多个线程同时访问的集合。

### 使用位

如果需要处理许多位，可以使用 `BitArray` 类和 `BitVector32` 结构。`BitArray` 位于 `System.Collections` 命名空间中，`BitVector32` 位于 `System.Collections.Specialized` 命名空间中。这两种类型最重要的区别是：`BitArray` 是可调整大小的——如果事先不知道需要的位数，这将非常有用——并且它可以包含大量位。`BitVector32` 基于堆栈，因此速度更快。`BitVector32` 只包含32位，存储在一个整数中。

### BitArray

`BitArray` 类是一个引用类型，包含一个 `int` 数组，每32位使用一个新整数。此类的成员如下表所示。

| BitArray 成员 | 说明 |
| --- | --- |
| Count Length | Count 和 Length 的 get 访问器都返回数组中的位数。通过 Length 属性，还可以定义新的大小并调整集合的大小。 |
| Item Get Set | 可以使用索引器读写数组中的位。索引器的类型是 bool。除了使用索引器，还可以使用 Get 和 Set 方法访问数组中的位。 |
| SetAll | SetAll 方法根据传递给该方法的参数设置所有位的值。 |
| Not | Not 方法生成数组中所有位的逆值。 |
| And Or Xor | 使用 And、Or 和 Xor 方法可以组合两个 BitArray 对象。And 方法执行二进制 AND，只有当两个输入数组中的位都设置时，结果位才被设置。Or 方法执行二进制 OR，只要两个输入数组中有一个或两个设置了位，结果位就会被设置。Xor 方法是异或，仅当输入位中只有一个被设置时，结果位才被设置。 |

辅助方法 DisplayBits 遍历 BitArray，并根据位是否被设置向控制台显示 1 或 0（代码文件 BitArraySample/Program.cs）：

```csharp
public static void DisplayBits(BitArray bits)
{
	foreach (bool bit in bits)
	{
		Write(bit ? 1 : 0);
	}
}
```

BitArraySample 使用以下依赖项和命名空间：

**依赖项**

NETStandard.Library

**命名空间**

System
System.Collections
static System.Console

演示 BitArray 类的示例创建了一个包含 8 位的位数组，索引从 0 到 7。SetAll 方法将所有 8 位设置为 true。然后，Set 方法将位 1 更改为 false。除了使用 Set 方法，还可以使用索引器，如索引 5 和 7 所示：

```csharp
var bits1 = new BitArray(8);
bits1.SetAll(true);
bits1.Set(1, false);
bits1[5] = false;
bits1[7] = false;
Write("initialized:");
DisplayBits(bits1);
WriteLine();
```

以下是初始化位的显示结果：

```
initialized: 10111010
```

Not 方法生成 BitArray 位的逆值：

```csharp
Write(" not");
DisplayBits(bits1);
bits1.Not();
Write(" =");
DisplayBits(bits1);
WriteLine();
```

Not 的结果是所有位都被反转。如果位原来是 true，则变为 false；如果原来是 false，则变为 true：

```
not 10111010 = 01000101
```

在下面的示例中，创建了一个新的 BitArray。通过构造函数，使用变量 bits1 来初始化数组，因此新数组具有相同的值。然后，将位 0、1 和 4 的值设置为不同的值。在使用 Or 方法之前，会显示位数组 bits1 和 bits2。Or 方法会更改 bits1 的值：

```csharp
var bits2 = new BitArray(bits1);
bits2[0] = true;
bits2[1] = false;
bits2[4] = true;
DisplayBits(bits1);
Write(" or");
DisplayBits(bits2);
Write(" =");
bits1.Or(bits2);
DisplayBits(bits1);
WriteLine();
```

使用 Or 方法时，会从两个输入数组中获取已设置的位。在结果中，如果该位在第一个数组或第二个数组中已设置，则结果位将被设置：

```
01000101 or 10001101 = 11001101
```

接下来，使用 And 方法对 bits2 和 bits1 进行操作：

```csharp
DisplayBits(bits2);
Write(" and");
DisplayBits(bits1);
Write(" =");
bits2.And(bits1);
DisplayBits(bits2);
WriteLine();
```

And 方法的结果只设置两个输入数组中均被设置的位：

```
10001101 and 11001101 = 10001101
```

最后，使用 Xor 方法执行异或操作：

```csharp
DisplayBits(bits1);
Write(" xor");
DisplayBits(bits2);
bits1.Xor(bits2);
Write(" =");
DisplayBits(bits1);
WriteLine();
```

使用 Xor 方法时，只有在第一个或第二个输入中设置了该位（但不能同时在两个输入中设置）时，结果位才会被设置：

```
11001101 xor 10001101 = 01000000
```

### BitVector32

如果事先知道需要多少位，则可以使用 BitVector32 结构而不是 BitArray。BitVector32 更高效，因为它是一个值类型，将位存储在整数内的堆栈上。一个整数可以容纳 32 位。如果需要更多位，可以使用多个 BitVector32 值或使用 BitArray。BitArray 可以根据需要增长；而 BitVector32 无法做到这一点。

下表显示了与 BitArray 有很大不同的 BitVector 成员：

| BitVector 成员 | 说明 |
| --- | --- |
| Data | Data 属性将 BitVector32 背后的数据作为整数返回。 |
| Item | 可以使用索引器设置 BitVector32 的值。索引器已重载；可以使用掩码或 BitVector32.Section 类型的节来获取和设置值。 |
| CreateMask | CreateMask 是一个静态方法，可用于创建掩码以访问 BitVector32 中的特定位。 |
| CreateSection | CreateSection 是一个静态方法，可用于在 32 位中创建多个节。 |

BitVectorSample 使用以下依赖项和命名空间：

**依赖项**

NETStandard.Library
System.Collections.Specialized

**命名空间**

System.Collections.Specialized
System.Text
static System.Console

下面的示例使用默认构造函数创建了一个 BitVector32，所有 32 位都初始化为 false。然后创建掩码以访问位向量中的位。第一次调用 CreateMask 会创建一个访问第一个位的掩码。调用 CreateMask 后，bit1 的值为 1。再次调用 CreateMask 并将第一个掩码作为参数传递给 CreateMask，会返回一个访问第二个位的掩码，该掩码为 2。接着 bit3 的值为 4，用于访问第 3 位；bit4 的值为 8，用于访问第 4 位。

然后，将掩码与索引器结合使用，以访问位向量中的位并相应地设置字段（代码文件 BitVectorSample/Program.cs）：

```csharp
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
WriteLine(bits1);
```

BitVector32 重写了 ToString 方法，该方法不仅显示类的名称，还会根据位是否被设置而显示 1 或 0：

```
BitVector32{000000000000000000000000000011101}
```

除了使用 CreateMask 方法创建掩码之外，还可以自己定义掩码；也可以一次设置多个位。十六进制值 abcdef 与二进制值 1010 1011 1100 1101 1110 1111 相同。由该值定义的所有位都被设置：

```csharp
bits1[0xabcdef] = true;
WriteLine(bits1);
```

通过显示的输出，可以验证已设置的位：

```
BitVector32{00000000101010111100110111101111}
```

将 32 位分成不同的节可能非常有用。例如，IPv4 地址被定义为一个四字节的数字，存储在一个整数中。可以通过定义四个节来拆分该整数。在多播 IP 消息中，会使用多个 32 位值。其中的一个

