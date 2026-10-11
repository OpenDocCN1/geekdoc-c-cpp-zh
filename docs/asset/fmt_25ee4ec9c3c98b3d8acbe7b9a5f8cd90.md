
外观上，这个例子与 `List<T>` 相同，但在外层大括号内部，你有第二层大括号包裹的项，字典中的一个条目。因为这个字典 `dict` 具有整数键和字符串值，每对内部大括号包含其中一个，并用逗号分隔。键/值对也用逗号分隔。

初始化 `HashSet<int>`（参见下一节）与初始化列表非常相似：

```csharp
HashSet<int> biggerPrimes = new HashSet<int> { 19, 23, 29, 31, 37, 41 };
```

本书网站上的 `UsingVarWithArraysAndCollections` 示例演示了在数组和集合上使用 `var` 关键字。

# 使用集合

C# 3.0 添加了新的集合类型 `HashSet<T>`。集合是一个无序的且没有重复项的集合。

这个概念源于数学。想想性别集合（女性和男性）、一周的天数集合，或者三角形的变体集合（等腰、等边、直角、钝角）。与数学集合不同，C# 集合不能是无限，尽管它们可以大到可用内存。

你可以对集合进行与其他集合的操作，例如添加、删除和查找项。你还可以执行若干类集合操作，例如并集（union）和交集（intersection）。并集将两个集合的成员合并为一个。交集找到两个集合之间的重叠部分，结果是一个仅包含重叠成员的集合。集合适用于合并和消除项。

与字典一样，集合使用哈希表实现。集合类似于具有键但没有值的字典，使得它们在形状上类似于列表。详情请参见前面的“使用字典”章节。

要创建一个 `HashSet<T>`，你可以这样做：

```csharp
HashSet<int> smallPrimeNumbers = new HashSet<int>();
smallPrimeNumbers.Add(2);
smallPrimeNumbers.Add(3);
```

或者，更方便的是，你可以使用集合初始化器：

```csharp
HashSet<int> smallPrimeNumbers = new HashSet<int> { 2, 3, 5, 7, 11, 13 };
```

或者从现有的任何类列表集合（包括数组）创建集合：

```csharp
List<int> intList = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7 };
HashSet<int> numbers = new HashSet<int>(intList);
```

## 使用集合 133

执行这段代码后，`unique()` 排除了队列中自身的项（1, 3, 5, 7 和 9），同时也排除了队列中不在 `unique` 中的项（0, 2, 4, 6, 8 和 17）。最终 `unique` 中留下了 11、13 和 15。

同时，下一段代码使用 `SymmetricExceptWith()` 方法来创建一个与 `IntersectWith()` 相反的结果。`IntersectWith()` 仅使用重叠的项，而 `SymmetricExceptWith()` 则会提供两个列表中互不重叠的项。你的 `UniqueToSet` 项目最终包含了 5, 3, 11 和 10：

```csharp
Console.WriteLine("Finding just the non-overlapping items in two lists:");
Stack<int> stackOne = new Stack<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8 });
Stack<int> stackTwo = new Stack<int>(new int[] { 2, 4, 6, 7, 8, 10, 12 });
HashSet<int> nonoverlapping = new HashSet<int>(stackOne);
// 另一个收集存在于一个集合但不在另一个中的项
nonoverlapping.SymmetricExceptWith(stackTwo);
foreach(int n in nonoverlapping)
{
    Console.WriteLine(n.ToString());
    Console.WriteLine("Press Enter to terminate...");
    Console.Read();
}
```

我对栈（stack）的使用方式有些不传统，因为我是一性添加成员而不是逐一个地 `push`，并且是一次移除多个而不是逐一个地 `pop`。这些操作——推入弹出——才是与栈交互的正确方式。

请注意，这里演示的 `HashSet<...>` 方法都是 `void` 方法——它们不返回值。结果会反映在调用这些方法的哈希集合上：例如上述代码示例中的 `nonoverlapping`。

我们起初觉得 `UnionWith()` 和 `IntersectWith()` 的用法有点别扭；我想要得到一个新的结果，而在应用这些方法时让原始（输入）集合保持不变。在第二本书中，我们遇到了（很高兴地报告）新的 LINQ 查询运算符，它们为这些方法增加了可以返回全新新集合的版本。将你在这里看到的与你所看到的相结合，你可以兼得其利。这种好处多到我就不多说了。

你什么时候会使用 `HashSet<>`？每当你处理两个或多个集合并想要找到重叠项——或者创建一个包含两个其他集合的集合，或者从一个集合中排除一组项时——集合都是非常有用的。许多 `HashSet<T>` 方法可以将集合与其他集合类关联起来。当然，你可以用集合做更多事情，所以可以在帮助文件中查找 `HashSet<T>` 术语并尝试 `HashSetExample`。

![](img/36596fb11aa4233d5cab0d6ddd1d822_158_0.png)

## 134 关于使用旧式集合

在远古时代，在 C# 2.0 之前，当查罗亚斯特在说话时，所有的集合类都实现实现为 `Object` 类型的集合。你不能仅为字符串或整数创建集合。这种集合允许你存储任何类型的数据，因为 C# 中的所有对象都派生自 `Object`。因此，你可以同时向同一个集合添加整数和字符串，而不会看到错误信息（由于 C# 的继承和多态性，我在第二书中会讨论）。

但在基于 `Object` 的安排中出现了一个严重的缺点：为了提取你已知放入集合的整数，你必须将其强制转换为你得到的 `int` 对象：

```csharp
ArrayList List = new ArrayList(); // 一个旧式的 Object 列表
int MyInt = (int)List[0]; // 提取列表中的第一个整数
```

这就像你的整数被放在了惊喜蛋里面。如果你不进行强制转换，就会产生错误，因为例如，`Object` 不支持 `+` 操作或其他在整数上预期的的方法、属性和运算符。你可以忍着这些局限性进行工作，但这种代码很容易出错，而且所有的强制类型转换非常枯燥。（此外，正如我在第二本书中讨论的，处理惊喜蛋会因为“装箱”（boxing）现象而增加一些开销。过多的装箱会减慢你的程序。）

而且，如果集合恰好包含多种类型的对象——问题就会变得更加棘手。不过，你可以转换为你所需的特定类型。有了这些局限性，你就能理解为什么旧集合是有问题的了。

如果集合恰好包含多种类型的对象——问题就会变得更加棘手。不过，你可以转换为你所需的特定类型。有了这些局限性，你就能理解为什么旧集合是有问题的了。

![](img/36596fb11aa4233d5cab0d6ddd1d822_159_0.png)

## 138 遍历文件目录

```cs
// 每隔 20 行停止，以免数据滚出
// 控制台屏幕上方。
if ((line % 20) == 0)
{
    Console.WriteLine("按回车键继续下 20 行");
    Console.ReadLine();
}
```

```cs
// DumpBuffer - 将字符缓冲区以十六进制格式作为单行写出。
public static void DumpBuffer(byte[] buffer, int numBytes)
{
    for(int index = 0; index < numBytes; index++)
    {
        byte b = buffer[index];
        Console.Write("{0:X2}, ", b);
    }
    Console.WriteLine();
}
```

在命令行中，用户指定的目录作为程序的参数。以下命令“十六进制转储”（hex-dumps）temp 目录下的每个文件（包括二进制文件和文本文件）：

`loopthroughfiles c:\randitemp`

如果你没有输入目录名称，程序默认使用当前目录。（十六进制转储将输出显示为十六进制——16 进制——系统中的数字。参见旁边的边栏，“获取十六进制”。）

> `FileRead` 和 `FileWrite` 是从控制台读取输入，而此程序从命令行获取输入。我尽量不让你们困惑——我正试图展示解决同一个问题的不同方法。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_163_0.png)

## 获取十六进制

和二进制（0 和 1）一样，十六进制（或称 "hex"）是计算机编程的基础。在 16 进制中，数字是 0 到 9 以及 A, B, C, D, E, F —— A=10, B=11...F=15。为了说明这一点（使用 0x 前缀表示十六进制）：

0x2A = 十进制 42；2*16 + A*1（其中 A=10）

字母数字可以是大大写，也可以是小写：C 和 c 相同。这看起来很奇怪，但非常有用，尤其是当你调试或对内存内容进行底层操作时。

```text
0xD = 十进制 13
0x10 = 十进制 16；1*16 + 0*1
```

## 遍历文件目录 139

`LoopThroughFiles` 的第一行寻找程序参数。如果参数列表为空（`args.Length` 为零），程序将调用 `Directory.GetCurrentDirectory()`。如果你在 Studio 内部运行而不是从命令行运行，值默认为 LoopThroughFiles 项目目录下的 bin\Debug 子目录。

第一卷

第七章

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_164_0.png)

`Directory` 类为用户提供了一组操作目录的方法。`FileInfo` 类提供了移动、复制和删除文件等其他任务的方法。

### 遍历集合

程序通过调用 `GetFileList()` 创建指定目录中所有文件的列表。该方法返回一个 `FileInfo` 对象的数组。每个 `FileInfo` 对象都包含有关文件的信息——例如，文件名（带有文件完整路径的 FullName，或不带路径）、创建日期和最后修改日期。`Main()` 使用你的老朋友 `foreach` 语句遍历文件列表。它显示每个文件的名称，并将文件传递给 `DumpHex()` 方法显示在控制台上。

在循环结束时，它允许程序员查看 `DumpHex()` 的输出。

`GetFileList()` 方法开始时创建一个 `FileInfo` 列表。这是事件的一个返回值。这里有一个调用 `GetFileList()` 时需要记住的小技巧：如果发生错误，它会显示错误消息并返回一个长度为零的列表![](img/36596fb11aa4233d5cab0d6ddd1d82e8_164_1.png)

小心返回对象的引用。例如，除非你想通过使用那些队列而不是你的类来导致内存泄漏，否则不要返回底层队列之一的引用。那是通往损坏的门票。`GetFileList()` 随后创建一个 `DirectoryInfo` 对象。正如其名称所示，`DirectoryInfo` 对象包含关于目录的相同类型的信息：名称、排序和序列号类型之类的内容。然而，`DirectoryInfo` 对象可以通过数组的形式访问目录中的文件。一如往常，`GetFileList()` 封装了目录和文件相关的代码。结尾的 `catch` 块捕获了因输入错误而产生的任何错误。

## 140 遍历文件目录

`DumpHex()` 方法有点棘手，因为很难将输出格式化得恰好。`DumpHex()` 首先打开文件，获取文件的全（包括路径），并以只读模式打开 `FileStream`。然后 `DumpHex()` 每次读取 10 字节遍历文件。它将每个十六进制格式显示为单行。每 20 行，它会暂停直到用户按下回车键。垂直方向，控制台窗口默认容纳 25 行（用户可以更改窗口大小，允许更多或更少的行）。否则，数据会在你阅读之前从屏幕顶部消失。模运算符 (`%`) 返回除法的余数。因此，当行数为 20、40 时，`(line % 20) == 0` 为真。这种逻辑在许多需要执行此类操作的情况下都是有用的。`DumpHex` 以十六进制格式写入字节。字节的范围是 0 到 255，这里是前 20 行：

Hex dump of C:\Programs\Test.txt:

001 53, 74, 72, 75, 74, 61, 20, 

002 69, 74, 65, 64, 29, 0A, 

003 72, 69, 74, 65, 63, 20, 0A, 

004 65, 75, 6c, 65, 20, 46, 65, 

005 66, 69, 6c, 65, 64, 65, 20, 

006 66, 69, 65, 63, 73, 20, 6F, 

007 64, 69, 65, 63, 74, 79, 20, 

008 72, 73, 74, 79, 61, 6D, 29, 

009 38, 0A, 20, 20, 42, 65, 74, 

010 68, 73, 74, 75, 72, 61, 6D, 

011 20, 20, 74, 65, 72, 73, 74, 

012 72, 69, 65, 64, 20, 65, 75, 

013 63, 65, 20, 74, 69, 6c, 65, 

014 20, 69, 74, 65, 72, 20, 78, 

015 65, 74, 74, 61, 72, 6D, 20, 

016 68, 73, 74, 75, 74, 61, 00, 

017 69, 65, 74, 74, 74, 20, 20, 0A, 

018 64, 69, 72, 65, 73, 74, 6f, 72, 

019 20, 69, 6e, 76, 61, 6c, 69, 74, 

020 20, 64, 69, 72, 65, 63, 74, 79,

# 142 迭代遍历 foreach 集合：迭代器

```cs
// Pass in any kind of collection:
void MyClearMethod(Collection aCol, int index)
{
    aCol[index] = 0; // 索引并不适用于所有类型的集合。
    //...
}
```

每种集合类型都可以（并且已经）定义它们自己的访问方法。例如，链表可能提供一个 `GetNext()` 方法来获取对象链中的下一个元素，而栈集合可能提供 `Push()` 和 `Pop()` 来添加或移除对象。

一种更通用的方法是为每个集合类提供一个独立的迭代器类，这在导航该特定集合时是明智的。每个集合都定义了自己的 `IteratorX` 类。与 `x` 不同，`IteratorX` 提供了一个通用的 `IEnumerator`，这是迭代的金标准。这种技术使用第二个对象（即迭代器）作为指向集合的某种指针或光标。

迭代器（枚举器）方法具有以下优势：

- 每个集合类都可以定义自己的自己的迭代器类。由于迭代类实现了标准的 `IEnumerator` 接口，因此编写代码通常很简单。

- 应用代码不需要知道集合代码的工作原理。只要程序员理解如何使用迭代器，迭代类就可以处理细节。这就是良好的封装。

- 应用代码可以为同一个集合创建多个独立的迭代器对象。由于迭代器包含它自己的状态信息（在迭代器内部“知道自己所处的位置”），因此每个迭代器都可以独立地遍历集合。它可以同时运行多个迭代器，且每个迭代器都处于集合中的不同位置。

为了让 `foreach` 循环成为可能，`IEnumerator` 接口必须支持从数组到链表的所有类型的集合。例如，你不能使用迭代器来访问集合类内部的位置，因为大多数集合不提供随机访问。（你需要发明一种具有该能力的不同枚举接口，但它无法与 `foreach` 配合工作。）

`IEnumerator` 提供了这三个方法：

- `Reset()`：将枚举器指向集合的开头。注意：`IEnumerator` 的泛型版本 `IEnumerator<T>` 不提供 `Reset()` 方法。对于泛型 `LinkedList`，只需从调用 `MoveNext()` 开始即可。

- `MoveNext()`：将枚举器从集合中的当前对象移动到下一个对象。

- `Current`：这是一个属性而非方法，用于检索枚举器当前位置存储的数据。

下面的方法演示了这一原理。`MyCollection` 的程序员创建了一个迭代器类（未显示），例如 `IteratorMyCollection`（使用我在在本章较早之前描述的迭代器命名规范）。应用程序员在 `MyCollection` 中有许多 `ContainedDataObjects`。以下代码段使用三个标准的 `IEnumerator` 方法来读取这些对象：

```cs
// The following code segment uses the three standard IEnumerator methods to read these objects:
IEnumerator enumerator = MyCollection.GetEnumerator();
while (enumerator.MoveNext())
{
    ContainedDataObject data = enumerator.Current;
    // Process the data
}
```
