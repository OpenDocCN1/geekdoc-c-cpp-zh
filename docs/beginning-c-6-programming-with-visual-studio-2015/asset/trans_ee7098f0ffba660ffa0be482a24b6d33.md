
2. 通过在 Program.cs 顶部附近放置以下代码行导入 System.IO 和 System.Console 命名空间：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using static System.Console;
```

3. 将以下代码添加到 Main() 方法中：

```
static void Main(string[] args)
{
    string line;
    try
    {
        FileStream aFile = new FileStream("Log.txt", FileMode.Open);
        StreamReader sr = new StreamReader(aFile);
        line = sr.ReadLine();
        // Read data in line by line.
        while(line != null)
        {
            WriteLine(line);
            line = sr.ReadLine();
        }
        sr.Close();
    }
    catch(IOException e)
    {
        WriteLine("An IO exception has been thrown!");
        WriteLine(e.ToString());
        return;
    }
    ReadKey();
}
```

4. 将在前一个示例中创建的 Log.txt 文件复制到 StreamRead\bin\Debug 目录。如果没有名为 Log.txt 的文件，FileStream 构造函数在找不到它时会抛出异常。

5. 运行应用程序。你应该会看到文件文本写入控制台，如图 18-4 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_605_0.png)

图 18-4

另一种处理大文件的方法是在 .NET 4 中引入的，使用静态 File.ReadLines() 方法。事实上，File 有几个静态方法可用于简化读取和写入文件数据，但这个方法特别有趣，因为它返回一个 IEnumerable<string> 集合。你可以遍历此集合中的字符串，一次读取文件一行。使用此方法，你可以将前一个示例重写如下：

```
foreach (string alternativeLine in File.ReadLines("Log.txt"))
    WriteLine(alternativeLine);
```

正如你所见，在 .NET 中有几种方法可以实现相同的结果——即从文件读取数据。选择最适合你的技术。

## 异步文件访问

有时——例如，当你一次性执行大量文件访问操作或处理非常大的文件时——读写文件系统数据可能会很慢。如果是这种情况，你可能希望在等待时执行其他操作。对于桌面应用程序来说尤其重要，在后台工作时你希望应用程序对用户保持响应。

为此，.NET 4.5 引入了处理流的异步方式。这适用于 FileStream 类，以及 StreamReader 和 StreamWriter。如果你浏览过这些类的定义，你可能会注意到一些以 Async 后缀结尾的方法——例如，StreamReader 有一个名为 ReadLineAsync() 的方法，它是 ReadLine() 的异步版本。这些方法设计用于与基于任务的异步编程模型一起使用。

异步编程是一种高级技术，本书中未详细涵盖。然而，如果你有兴趣进行异步文件系统访问，那么这里就是开始的地方。你可能还想阅读 Christian Nagel、Jay Glynn 和 Morgan Skinner 所著的《Professional C# 5.0 and .NET 4.5.1》（Wrox，2014）以获取更多详细信息。

## 读取和写入压缩文件

在处理文件时，通常硬盘上会占用大量空间。这对于图形和声音文件尤其如此。你可能遇到过能够压缩和解压缩文件的实用程序，当你想移动它们或通过电子邮件发送它们时非常方便。System.IO.Compression 命名空间包含类，可让你使用 GZIP 或 Deflate 算法从代码中压缩文件——两者都是公开的，任何人都可以免费使用。

不过，压缩文件不仅仅是压缩它们。你可能已经看到商业应用程序如何将多个文件放在单个压缩文件中，通常称为存档。System.IO.Compression 命名空间中有类可实现类似功能。然而，为了本书的简单性，你只会查看一种场景：将文本数据保存到压缩文件中。你不太可能在外部实用程序中访问此文件，但该文件将比其未压缩的版本小得多！

这里要查看的 System.IO.Compression 命名空间中的两个压缩流类 DeflateStream 和 GzipStream 工作方式非常相似。在这两种情况下，你都用现有流初始化它们，对于文件而言，这将是 FileStream 对象。此后，你可以像使用任何其他流一样将它们与 StreamReader 和 StreamWriter 一起使用。你需要额外指定的只是流将用于压缩（保存文件）还是解压缩（加载文件），以便类知道如何处理流经的数据。这最好通过以下示例来说明。

## 试一试 读取和写入压缩数据：Compressor\Program.cs

-   1. 创建一个名为 Compressor 的新控制台应用程序并将其保存到目录 C:\BegVCSharp\Chapter18。
-   2. 在 Program.cs 顶部附近放置以下代码行。你需要导入 System.Console、System.IO 和 System.IO.Compression 命名空间以使用文件和压缩类：
-   3. 在 Main() 方法之前将以下方法添加到 Program.cs 的主体中：
-   4. 将以下代码添加到 Main() 方法中：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.IO.Compression;
using static System.Console;
```

```
static void SaveCompressedFile(string filename, string data)
{
    FileStream fileStream =
        new FileStream(filename, FileMode.Create, FileAccess.Write);
    GZipStream compressionStream =
        new GZipStream(fileStream, CompressionMode.Compress);
    StreamWriter writer = new StreamWriter(compressionStream);
    writer.Write(data);
    writer.Close();
}
static string LoadCompressedFile(string filename)
{
    FileStream fileStream =
        new FileStream(filename, FileMode.Open, FileAccess.Read);
    GZipStream compressionStream =
        new GZipStream(fileStream, CompressionMode.Decompress);
    StreamReader reader = new StreamReader(compressionStream);
    string data = reader.ReadToEnd();
    reader.Close();
    return data;
}
```

```
static void Main(string[] args)
{
    try
    {
        string filename = "compressedFile.txt";
```

9. 将以下代码添加到 Watch! 按钮的 Click 事件处理程序中，该处理程序启动 FileSystemWatcher：

```
private void WatchButton_Click(object sender, RoutedEventArgs e)
{
    watcher.Path = System.IO.Path.GetDirectoryName(LocationBox.Text);
    watcher.Filter = System.IO.Path.GetFileName(LocationBox.Text);
    watcher.NotifyFilter = NotifyFilters.LastWrite |
        NotifyFilters.FileName | NotifyFilters.Size;
    AddMessage("Watching " + LocationBox.Text);
    // Begin watching.
    watcher.EnableRaisingEvents = true;
}
```

10. 创建一个名为 C:\TempWatch 的目录，并在该目录中创建一个名为 temp.txt 的文件。

11. 运行应用程序。如果一切构建成功，请单击 Browse 按钮并选择 C:\TempWatch\temp.txt。

12. 单击 Watch! 按钮开始监视文件。你在应用程序中看到的唯一变化是确认文件正在被监视的消息。

13. 使用 Windows 资源管理器，导航到 C:\TempWatch。在记事本中打开 temp.txt，向文件中添加一些文本并保存。

14. 重命名文件。

15. 你应该会看到所选监视文件的更改描述，如图 18-8 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_614_0.png)

图 18-8

## 工作原理

此应用程序相当简单，但它演示了 FileSystemWatcher 的工作原理。尝试使用你放入监视文本框的字符串。如果你在一个目录中指定 *.*，它将监视该目录中的所有更改。

应用程序中的大部分代码与设置 FileSystemWatcher 对象以监视正确位置有关：

```
watcher.Path = System.IO.Path.GetDirectoryName(LocationBox.Text);
watcher.Filter = System.IO.Path.GetFileName(LocationBox.Text);
```
