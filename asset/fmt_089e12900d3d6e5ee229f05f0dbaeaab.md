
# 解析

`SortedDictionary` 内部是一个二叉搜索树，在这里不再详细阐述其具体原理，但我可以提到它是一种优化元素搜索的结构。实际上还有另一个集合类，从程序员的角度来看它与 `SortedDictionary` 相同，但内部同样也是一个二叉搜索树。区别在于，`SortedList` 使用的内存比 `SortedDictionary` 少，反之，`SortedDictionary` 在插入和删除键时效率更高。

键是排序的，因此首先根据姓氏进行比较，如果姓氏相同，则根据名字进行比较。

# PageKey 和 Index

`PageKey` 定义键为字符串。注意该类如何实现 `IComparable` 接口，比较不区分大小写。

`SortedDictionary` 提供三种服务：
- 你可以向列表添加新关键字，可以是插入或更新现有的。

# 测试

```csharp
static Random rand = new Random();

static string[] words = { "Write", "if", "for", "while", "Variable", ... };

static void Main(string[] args) {
    Index index = new Index();
    for (int i = 0; i < 50; i++)
        index.Add(words[rand.Next(words.Length)], rand.Next(200));
    index.Print();
    Console.WriteLine();
    Print("Variable", index.Pages("Variable"));
    Print("Variables", index.Pages("Variables"));
    Print("Variables", index.Pages("Variables"));
}

static void Print(string name, int[] pages) {
    Console.Write(name);
    if (pages.Length > 0) {
        Console.Write(", ");
        for (int i = 0; i < pages.Length; i++) Console.Write(" " + pages[i]);
    }
    Console.WriteLine();
}
```

在程序开始时定义了一些单词。然后它们被随机插入到带有随机页码的索索引中：

# C# 1 编程简介与 C# 语言

# 第 4 部分 IO（输入输出）

在以前，文件是编程中的核心概念，即使它们现在的作用不再如以前那样，了解如何写入和读取文件仍然是重要的。

当 IO 和文件不再像以前那样发挥作用时，是因为需要处理存储在磁盘上的持久数据的应用程序通常会使用数据库产品，因此任何与文件和数据相关的内容都交给了当前的数据库系统。尽管如此，仍然存在需要访问普通文件的情况，主要体现在两种情况：如何读取和写入纯文件，以及如何序列化和反序列化对象。

与 .NET 中其他地方一样，对文件的访问通过许多现成的类减轻了程序员的负担，这些类主要位于 `System.IO` 命名空间。这是一个包含许多类的综合命名空间，幸运的是不需要了解所有的，所以我将集中在最少需要的类上。

从程序的角度来看，文件基本上是一个字节序列，在很多方面，人们可以将文件看作一个没有上限的一维数组（大小显然受限于磁盘上的可用空间）。下一次文件操作（读取或写入）执行的位置由所谓的“指针”决定，它实际上只是相对于文件开头的计数器。

## #28 文本文件

文本文件是一个包含多行的文件，其中每行都是一个字符串。.NET 中的字符串被表示为 Unicode 字符序列，每个字符以 2 字节的形式写入文件，但它是由 IO 系统进行封装的。文本文件对于以逗号分隔文件或类似形式交换数据仍然很重要。人们还应该注意，例如 HTML 或 XML 文件就是文本文件。

## ## 考试 51

### 写入和读取文本

我将编写一个程序，展示如何写入和读取简单的文本文件。当程序运行时，用户必须输入文本行，这些行将被保存到文件中。当用户直接按回车键时，输入结束，程序将读取文件并在屏幕上打印内容。

# 如何操作

创建文件并对其进行写入可以通过以下算法描述：

```
打开/创建文件
获取数据
只要有数据
在文件中写入一行
获取数据
关闭文件
```

重要的一点是，每次执行的实际方式实际上是相同的，只有“获取数据”这一操作可能会变化。同样地，读取文本文件可以写为以下算法：

```
打开文件
读取一行
只要有一行
使用该行
读取一行
关闭文件
```

在这里同样重要需要说明的是，无论文件内容如何，该过程都是相同的，只有“使用该行”这一操作是变化的。

程序可以写如下所示：

```csharp
using System;
using System.IO;
namespace Exam53
{
    class Program
    {
        static void Main(string[] args)
        {
            Write();
            Read();
        }
        public static string GetLine()
        {
            Console.Write("?");
            return Console.ReadLine();
        }
        public static void PutLine(string line)
        {
            Console.WriteLine(line);
        }
        public static void Write()
        {
            StreamWriter writer = new StreamWriter("Tekst.txt");
            string line = GetLine();
            while (line.Length > 0)
            {
                writer.WriteLine(line);
                line = GetLine();
            }
            writer.Close();
        }
```

在过去的60年里，马斯塔里特管理学院通过先进的管理教育提升了全球专业人士和组织的管理能力。

我们广泛的开放注册高管课程为您提供独特的互动、启发和多文化学习体验。

为应对明天的管理挑战做好准备并从今天开始应用。

更多信息，请访问 www.msm.nl 或拨打 +41 33 78 808 或通过 admissions@msm.nl 联系我们

全球网络化管理学院

在 bookboom.com 免费下载电子书

```csharp
public static void Read()
{
    StreamReader reader = new StreamReader("Tekst.txt");
    string line = reader.ReadLine();
    while (line != null)
    {
        PutLine(line);
        line = reader.ReadLine();
    }
    reader.Close();
}
```

### 解释

首先注意有一个针对 `System.IO` 的 `using` 语句。这在所有使用文件的应用程序中通常都是这样的。

`GetLine()` 方法对应于算法中的“获取数据”，它在屏幕上以问号的形式写入一个简单的提示并执行 `ReadLine()`。该方法返回一个带有用户输入内容的字符串。

`Write()` 方法创建并打开文件：

```csharp
StreamWriter writer = new StreamWriter("Tekst.txt");
```

该文件名为 `Tekst.txt`，通过 `StreamWriter` 类创建并打开以写入。注意，这里使用 `writer` 将字符串写入文件：

```csharp
writer.WriteLine(line);
```

在循环结束后，文件会被关闭。

还有几点需要注意。当你通过 `StreamWriter` 对象打开文件时，如果文件已经创建，它将被覆盖。如果你不想覆盖文件，可以为构造函数指定第二个参数，这将以追加模式打开文件。

在 bookboom.com 免费下载电子书

# C# 1 编程简介与 C# 语言

并将缓冲区的内容写入文件。

`Read()` 方法展示了如何读取文本文件的内容并打印在屏幕上。这里通过 `StreamReader` 对象打开文件：

```csharp
StreamReader reader = new StreamReader("Tekst.txt");
```

然后程序尝试读取文件中的行：

```csharp
string line = reader.ReadLine();
```

如果执行顺利（`line` 不为 `null`），则以 `line` 为参数执行 `PutLine()`，然后程序再次读取文件。结果是重复直到文件中没有数据。

这就是关于文本文件的全部内容，但对于如何获取数据，而如何处理从文件中读取的行取决于具体的任务。

## 考试 54

### 写入逗号分隔文件

以下示例在原理上与上面相同，但数据的处理并不完全简单，这也是一个更符合实际的文本文件示例。实际上有两个程序，接下来的程序也涉及同一个示例。

逗号分隔文件是一种包含多行的文本文件，每行包含多个元素，各个元素之间由分隔符隔开。分隔符通常是逗号（因此得名），但原则上可以是任何符号，只要是一个不出现在单个文本元素中的符号即可。在本例中，使用分号作为分隔符。

# C# 1 编程与 C# 语言简介

第一个程序将创建一个文本文件，用户在其中输入一个电话号码，随后是一个或多个产品数量（你可以将其想象为销售额），以此指示电话号码。对于每个电话号码，程序会在文件中写入一行，包含电话号码和产品数量，字段之间用分号分隔。结果可能是如下文件：

```
Kommandoprompt
D:\Document>type salg.txt
7520258:1088:23:5:567,85
9914140:1:25:10:5
9751457:
7520258:310:275:5:209,1
D:\Document>
```

请注意，同一个电话号码可能会出现多次，并且可能存在只有电话没有数量的行。

代码如下：

```csharp
class Program
static void Main(string[] args)
{
  StreamWriter writer = new StreamWriter("F:\\Salg.txt", true);
  string line = PhoneNumber();
  while (line.Length > 0)
  {
    writer.WriteLine(line);
    line = PhoneNumber();
  }
  writer.Close();
}

static string PhoneNumber()
{
  while (true)
  {
    Console.Write("Enter phone no. as 8 digits: ");
    string phone = Console.ReadLine().Trim();
    if (phone.Length == 0) return "";
    if (PhoneOk(ref phone))
    {
      StringBuilder builder = new StringBuilder(phone);
      double amount = Amount();
      while (amount > 0)
      {
        builder.Append(String.Format(":0:F2", amount));
        amount = Amount();
      }
      return builder.ToString();
    }
    Console.WriteLine("Illegal phone no.");
  }
}

static bool PhoneOk(ref string tlnfrr)
{
```
