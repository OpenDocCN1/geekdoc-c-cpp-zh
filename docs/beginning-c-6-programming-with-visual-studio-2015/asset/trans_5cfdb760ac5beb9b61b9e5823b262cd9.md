

4. 运行应用程序。结果如图18-1所示。

![](img/cf72ea860016d2d680fc085fc06f265a_599_0.png)

图18-1

## 工作原理

这个应用程序打开自己的 .cs 文件进行读取。它通过下面这行代码中的 `..` 字符串在文件结构中向上导航两个目录：

```
FileStream aFile = new FileStream("../../Program.cs", FileMode.Open);
```

实际执行从文件特定位置进行定位和读取的两行代码如下：

```
aFile.Seek(174, SeekOrigin.Begin);
aFile.Read(byteData, 0, 200);
```

第一行将文件指针移到文件中的第174个字节处。这是 Program.cs 文件中 `namespace` 的 `n`；它前面的174个字符是 using 指令。第二行将接下来的200个字节读入字节数组 `byteData`。

请注意，这两行被包含在 try...catch 块中，以处理可能抛出的任何异常：

```
try
{
    aFile.Seek(113, SeekOrigin.Begin);
    aFile.Read(byteData, 0, 100);
}
catch (IOException e)
{
    WriteLine("An IO exception has been thrown!");
    WriteLine(e.ToString());
    ReadKey();
    return;
}
```

几乎所有涉及文件 I/O 的操作都可能抛出类型为 IOException 的异常。所有生产环境代码都应包含错误处理，尤其是在处理文件系统时。本章中的所有示例都包含基本的错误处理形式。

一旦你从文件中获取了字节数组，就需要将其转换为字符数组，以便可以将其显示到控制台。为此，请使用 System.Text 命名空间中的 Decoder 类。该类旨在将原始字节转换为更有用的项，例如字符：

```
Decoder d = Encoding.UTF8.GetDecoder();
d.GetChars(byteData, 0, byteData.Length, charData, 0);
```

与 Read() 方法一样，Write() 方法也有三个参数：一个包含要写入文件流的数据的字节数组、数组中开始写入的索引，以及要写入的字节数。

## StreamWriter 对象

操作字节数组并不是大多数人认为有趣的事情——在使用过 FileStream 对象之后，你可能想知道是否有更简单的方法。不必担心，因为一旦有了 FileStream 对象，你通常会创建一个 StreamWriter 或 StreamReader，并使用其方法来操作文件。如果你不需要将文件指针更改到任意位置的功能，这些类会使文件操作变得容易得多。

StreamWriter 类使你能够将字符和字符串写入文件，该类会为你处理底层转换并写入到 FileStream 对象。

创建 StreamWriter 对象的方法有很多种。如果已有 FileStream 对象，则可以使用它来创建 StreamWriter：

```
FileStream aFile = new FileStream("Log.txt", FileMode.CreateNew);
StreamWriter sw = new StreamWriter(aFile);
```

也可以直接从文件创建 StreamWriter 对象：

```
StreamWriter sw = new StreamWriter("Log.txt", true);
```

此构造函数接受文件名和一个布尔值，该布尔值指定是追加到文件还是创建新文件：

- 如果此值设置为 false，则创建新文件，或截断现有文件然后将其打开。
- 如果它设置为 true，则打开文件并保留数据。如果文件不存在，则创建新文件。

与创建 FileStream 对象不同，创建 StreamWriter 时不会提供类似的选项范围——除了用于追加或创建新文件的布尔值之外，你没有像使用 FileStream 类那样指定 FileMode 属性的选项。也没有设置 FileAccess 属性的选项，因此你始终拥有对该文件的读/写权限。要使用任何高级参数，你必须先在 FileStream 构造函数中指定它们，然后根据 FileStream 对象创建 StreamWriter，就像你在下面的“试一试”中所做的那样。

## 试一试：将数据写入输出流：StreamWrite\Program.cs

1. 创建一个名为 StreamWrite 的新控制台应用程序，并将其保存在目录 C:\BegVCSharp\Chapter18 中。
2. 你将再次使用 System.IO 命名空间，因此请在 Program.cs 文件顶部附近添加以下 using 指令：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
```

3. 将以下代码添加到 Main() 方法中：

```
static void Main(string[] args)
{
    try
    {
        FileStream aFile = new FileStream("Log.txt", FileMode.OpenOrCreate);
        StreamWriter sw = new StreamWriter(aFile);
        bool truth = true;
        // Write data to file.
        sw.WriteLine("Hello to you.");
        sw.Write($"It is now {DateTime.Now.ToLongDateString()}");
        sw.Write("and things are looking good.");
        sw.Write("More than that,");
        sw.Write($" it's {truth} that C# is fun.");
        sw.Close();
    }
    catch (IOException e)
    {
        WriteLine("An IO exception has been thrown!");
        WriteLine(e.ToString());
        ReadLine();
        return;
    }
}
```

4. 生成并运行项目。如果找不到错误，它应该会快速运行并关闭。由于你没有在控制台上显示任何内容，因此这不是一个非常令人激动的程序。

5. 转到应用程序目录并找到 Log.txt 文件。由于你使用了相对路径，该文件位于 StreamWrite\bin\Debug 文件夹中。

6. 打开文件。你应该会看到如图18-3所示的文本。

![](img/cf72ea860016d2d680fc085fc06f265a_603_0.png)

图18-3

## 工作原理

这个简单的应用程序演示了 StreamWriter 类的两个最重要的方法：Write() 和 WriteLine()。它们都有许多重载版本，用于执行更高级的文件输出，但在此示例中你使用了基本的字符串输出。

WriteLine() 方法将传递给它的字符串写入文件，并紧跟一个换行符。在示例中可以看到，这会导致下一个写入操作在新的一行开始：

```
sw.WriteLine("Hello to you.");
```

Write() 方法将传递给它的字符串写入文件，而不附加换行符，从而可以使用多个 Write() 语句编写完整的句子或段落。就像你可以将格式化数据写入控制台一样，也可以将格式化数据写入文件。例如，你可以使用内插字符串参数将变量的值写入文件：

```
sw.Write($"It is now {DateTime.Now.ToLongDateString()}");
```

DateTime.Now 保存当前日期；ToLongDateString() 方法用于将此日期转换为易于阅读的形式。

```
sw.Write("More than that,");
sw.Write($"it's {truth} that C# is fun.");
```

同样，你使用内插字符串参数，这一次与 Write() 配合使用来显示布尔值 truth——你之前将此变量设置为 true，其值会自动转换为字符串“True”以进行格式化。

你可以使用 Write() 和格式参数写入逗号分隔的文件：

```
[StreamWriter object].Write($"{100}, {"A nice product"}, {10.50}");
```

在更复杂的示例中，这些数据可能来自数据库或其他数据源。

## StreamReader 对象

输入流用于从外部源读取数据。通常，这将是磁盘或网络位置上的文件，但请记住，该源几乎可以是任何可以发送数据的东西，例如网络应用程序，甚至控制台。

StreamReader 类是你将用于从文件读取数据的类。与 StreamWriter 类一样，这是一个通用类，可用于任何流。在下一个“试一试”中，你将再次围绕 FileStream 对象构造它，以便它指向正确的文件。

StreamReader 对象的创建方式与 StreamWriter 对象大致相同。创建它的最常用方法是使用先前创建的 FileStream 对象：

```
FileStream aFile = new FileStream("Log.txt", FileMode.Open);
StreamReader sr = new StreamReader(aFile);
```

与 StreamWriter 一样，StreamReader 类可以直接从包含特定文件路径的字符串创建：

```
StreamReader sr = new StreamReader("Log.txt");
```

## 试一试：从输入流读取数据：StreamRead\Program.cs

1. 创建一个名为 StreamRead 的新控制台应用程序，并将其保存在目录 C:\BegVCSharp\Chapter18 中。

