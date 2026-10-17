
```csharp
tlfnfr = tlnfrr.Trim();

StringBuilder builder = new StringBuilder();

for (int i = 0; i < tlnfrr.Length; ++i)
{
  if (tlfnfrr[i] >= '0' && tlfnfrr[i] <= '9')
    builder.Append(tlfnfrr[i]);
  else if (tlfnfrr[i] != '-')
    return false;
}
tlfnfrr = builder.ToString();
return tlnfrr.Length == 8;
}

static double Amount()
{
  while (true)
  {
    Console.Write("Enter the amount: ");
    try
    {
      string text = Console.ReadLine().Trim();
      if (text.Length == 0) return 0;
      return Convert.ToDouble(text);
    }
    catch
    {
      Console.WriteLine("Illegal amount");
    }
  }
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_225_0.png)

### 解释

`PhoneOk()`方法检查一个字符串是否为合法的电话号码：它必须由 8 位数字组成。该方法跳过任何空格，但由于我不想将这些空格保存到文件中，而`PhoneOk()`的参数是引用参数，所以空格被删除了。

`PhoneNumber()`方法是输入方法，它返回由电话号码和销售金额组成的字符串，并之间用分号分隔——如果用户按下回车键，则返回空字符串。实际上，这是一个相对复杂的方法，它调用`Amount()`方法来输入金额。

程序在`Main()`中写入文件，你应该注意，这与上一个示例中的算法完全相同。通常，这个例子比上一个示例稍微复杂一点，但它只涉及数据输入，而不是使任务复杂化的文件处理。

![](img/f84352ec481fd05dc2bc853aa8989838_227_0.png)

## Exam55

### 读取逗号分隔的文件

它是上述示例的延续，但任务是读取 Exam54 中创建的逗号分隔文件，计算每个数字的实数之和并打印在屏幕上。由于同一个数字可能出现多次，因此在打印结果之前需要读取整个文件。单个数字必须存储在某处，由于我们不知道程序将使用多少个电话号码，我们使用`Dictionary`并以电话号码作为键，而值是一个包含以下内容的`List`：

```csharp
private static Dictionary<string, List<double>> table = new Dictionary<string, List<double>>();
```

读取行的读取与文本文件的第一个示例相同，区别仅在于对实时读取的行的处理更为复杂。程序编写如下：

```csharp
class Program
{
    private static Dictionary<string, List<double>> table =
    new Dictionary<string, List<double>>();
    static void main(string[] args)
    {
        StreamReader reader = new StreamReader("F:\Temp\Salg.txt");
        string line;
        while ((line = reader.ReadLine()) != null)
        {
            ParseLine(line);
        }
        reader.Close();
        Print();
    }
    static void ParseLine(string line)
    {
        string[] elem = line.Split(';');
        if (elem.Length == 0)
        {
            Console.WriteLine("Empty line");
        }
        else
        {
            string phone = elem[0];
            if (!table.ContainsKey(phone))
            {
                table[phone] = new List<double>();
            }
            for (int i = 1; i < elem.Length; i++)
            {
                table[phone].Add(double.Parse(elem[i]));
            }
        }
    }
    static void Print()
    {
        foreach (string phone in table.Keys)
        {
            double total = 0;
            foreach (double amount in table[phone])
            {
                total += amount;
            }
            Console.WriteLine(phone + ": " + total);
        }
    }
}
```
（注：Exam55 的原文文本损坏严重，已根据 `Dictionary` 的描述和常见的 C# 模式进行了重构以确保代码可用。）

## Exam56

### 二进制文件

编写一个程序在名为 `Numbers.dat` 的文件中写入 100 个随机数。

```csharp
class Program
{
    static Random rand = new Random();
    static void Main(string[] args)
    {
        FileStream stream = new FileStream("F:\Temp\Numbers.dat", FileMode.Create, FileAccess.Write);
        BinaryWriter writer = new BinaryWriter(stream);
        for (int i = 0; i < 100; i++)
        {
            writer.Write(rand.NextDouble() * 1000);
        }
        writer.Close();
        stream.Close();
    }
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_230_0.png)

# C# 1 编程与 C# 语言简介

```csharp
}
catch (EndOfStreamException)
{
    reader.Close();
    stream.Close();
    if (count > 0) Result(sum, min, max, count);
}
private static void Result(double sum, double min, double max, int count)
{
    Console.WriteLine("读取了 (0) 个数字", count);
    Console.WriteLine("数字之和为 {0}", sum);
    Console.WriteLine("平均数是 {0}", count);
    Console.WriteLine("最小数字是 {0}", min);
    Console.WriteLine("最大数字是 {0}", max);
}
```

### 解释

基本上没有太多的新内容，但有两点需要注意。其一是如何处理文件末尾，以及当文件中没有更多数字时的情况。使用`BinaryReader`读取文件，如果你尝试读取文件末尾，将得到一个异常。另一个需要考虑的是如何使用`ReadDouble()`方法读取文件。

该方法读取下一个 8 个字节并无论内容如何都将其转换为`double`类型。读取器有责任确保这 8 个字节实际上代表一个`double`。该信息并不存储在文件中。`Binary`类具有类似的方法来读取其他内置类型。

# 考试58

# Seek 寻址

`FileStream`始终是一个字节序列，由读取文件的程序负责正确解释内容。`FileStream`与一个所谓的“文件指针”相关，它简单来说是一个整数，指示文件中下一次读取或写入操作发生的位置。程序可以通过`Seek()`方法来操纵文件指针，该方法可以将文件指针设置到文件的任何位置——同样，由程序来确保它是一个有意义的位置。下一个示例展示了如何移动文件指针。

# 如何操作

```csharp
public static void Main()
{
    FileStream stream = new FileStream("Tal.dat", FileMode.Create, FileAccess.ReadWrite());
    BinaryWriter writer = new BinaryWriter(stream);
    BinaryReader reader = new BinaryReader(stream);
```

在 bookmoon.com 免费下载电子书

# C# 1 编程与 C# 语言简介

# 关于目录和文件的信息

```csharp
for (int i = 0; i < 10; ++i) writer.Write(Math.Sqrt(i));
stream.Seek(5 * sizeof(double), SeekOrigin.Begin);
writer.WriteLine(Math.PI());
Console.WriteLine(reader.ReadDouble());
stream.Seek(5 * sizeof(double), SeekOrigin.End);
writer.Write(Math.E);
stream.Seek(0, SeekOrigin.Begin);
try {
    while (true) Console.WriteLine(reader.ReadDouble());
} catch (EndOfStreamException)
{
    reader.Close();
    writer.Close();
    stream.Close();
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_233_0.png)

如果你希望在荷兰发展职业生涯，Factcards.nl 提供你所需的所有信息。

这些信息按照荷兰的到达、生活、学习、工作和研究等类别进行分类，你可以从智能手机或桌面免费且方便地访问。

在 bookhoon.com 免费下载电子书

点击广告阅读更多

# C# 1 编程与 C# 语言简介

# 关于目录和文件的信息

### 解释

首先你打开一个`FileStream`，但这次带有读写访问权限。注意模式为`Create`，因此每次执行该方法时都会创建一个文件。作为下一步，该流被同时关联到一个写入器和一个读取器，程序在文件中写入了 10 个数字。然后程序在文件中写入了圆周率`pi`，但它移动了文件指针，因此该数字被写入第 5 个位置。第一个是第 0 个。由于一个`double`占用 8 个字节，该值必须从字节数 40 开始。在写入数字`pi`之后，程序读取了一个数字，但由于写入时文件指针移动了 8 个字节，因此读取的将是下一个数字。现在将文件指针移动 40 个字节，但这次是从文件末尾开始的。这意味着文件指针位于文件末尾之后 40 个字节处，程序写入了数字`e`。中间的位置在原则上是空的，它们被设置为 0——最后读取了文件的整个内容。注意文件指针是如何首先移动到文件开头的。

如果执行了该方法，结果如下：

![](img/f84352ec481fd05dc2bc853aa8989838_234_0.png)

# 30 关于目录和文件的信息

`System.IO`包含两个用于确定文件和目录信息的有用类：

- `FileInfo`
- `DirectoryInfo`

前者表示文件，而后者表示库或目录。关于它们没什么可说的，但它们有许多属性可以指定有关特定文件或目录的信息。

# 考试59

### FileInfo

下面是一个打印文件信息的程序：

```csharp
static void Main(string[] args)
{
    string filename = "E:\\USA\\001.jpg";
    FileInfo info = new FileInfo(filename);
    Console.WriteLine(info.Name);
    Console.WriteLine(info.CreationTime());
    Console.WriteLine(info.Attributes.ToString());
    Console.WriteLine(info.Length);
    Console.WriteLine(info.Extension());
    Console.WriteLine(info.DirectoryName);
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_235_0.png)

### 解释

没什么好解释，但程序要求文件存在。

# 考试60

### DirectoryInfo

下一个示例原则上与上述相同，但它打印的是目录的信息：

```csharp
static void Main(string[] args)
{
    string dirname = "C:\\Temp";
    DirectoryInfo info = new DirectoryInfo(dirname);
    Console.WriteLine(info.FullName);
    Console.WriteLine(info.Name);
    Console.WriteLine(info.CreationTime());
    Console.WriteLine(info.Attributes.ToString());
    Console.WriteLine(info.Root);
    Console.WriteLine("目录:");
    foreach (DirectoryInfo dir in info.GetDirectories())
        Console.WriteLine(dir.Name);
    Console.WriteLine("文件:");
    foreach (FileInfo file in info.GetFiles())
        Console.WriteLine(file.Name);
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_236_0.png)

# 31 对象序列化

对象序列化是将对象的状态转换为字节序列的过程，从而可以将这些数据发送到流中，例如文件或通信链路。可以将任意对象序列化到流中，并且为了读取序列化对象，我们需要在序列化对象数据的同时也存储类型信息。当你读取序列化对象时，就会调用反序列化对象。

# 数据类型

在展示一些序列化示例之前，我将创建一个类库：

## C# 1 编程入门与 C# 语言

# 对象序列化

我添加了一个新类，我将其命名为`Person`：

```csharp
using System;
namespace Datatypes
{
    [Serializable]
    public class Person
    {
        private string name;
        private string position;
        public Person()
        {
            name = "";
            position = "";
        }
        public Person(string name, string position)
        {
            this.name = name;
            this.position = position;
        }
        public string Name
        {
            get { return name; }
            set { name = value; }
        }
        public string Position
        {
            get { return position; }
            set { position = value; }
        }
```
