

某些流仅允许写入，某些流仅允许读取，而某些流允许随机访问。随机访问使你能够在流中随机定位光标——例如，从流的开头开始读取，然后移动到流的末尾，并在流的中间位置继续。

在这些示例中，Microsoft 提供了用于向内存写入或从内存读取的 .NET 类：`System.IO.MemoryStream` 对象。`System.Net.Sockets.NetworkStream` 对象处理网络数据。Stream 类不对数据源的性质做任何假设。它可以是文件流、内存流、网络流，或你能想到的任何数据源。

某些流也可以被链接。例如，`DeflateStream` 可用于压缩数据。该流反过来可以写入 `FileStream`、`MemoryStream` 或 `NetworkStream`。`CryptoStream` 使你能够加密数据。也可以将 `DeflateStream` 链接到 `CryptoStream`，然后再写入 `FileStream`。

> **NOTE** 第 24 章“Security”解释了如何使用 `CryptoStream`。

使用流时，外部源甚至可能是你自己代码中的一个变量。这听起来可能很矛盾，但使用流在变量之间传输数据的技术可以成为在数据类型之间转换数据的有用技巧。C 语言使用了类似的东西——`sprintf` 函数——在整数数据类型和字符串之间转换，或格式化字符串。

拥有一个用于数据传输的单独对象，而不是使用 `FileInfo` 或 `DirectoryInfo` 类来执行此操作的优点在于，将数据传输的概念与特定数据源分离，使得更容易交换数据源。流对象本身包含大量关于在外部源和代码中的变量之间移动数据的通用代码。通过将此代码与任何特定数据源的概念分离，你使此代码更容易在不同情况下重用。

虽然直接读取和写入流并不容易，但你可以使用读取器和写入器。这又是关注点的分离。读取器和写入器可以读取和写入流。例如，`StringReader` 和 `StringWriter` 类与稍后用于读取和写入文本文件的两个类的继承树相同。这些类在幕后几乎肯定会共享大量代码。图 23.3 说明了 `System.IO` 命名空间中流相关类的层次结构。

![](img/3d365b72b289213a91ade7eb366b8f35_829_0.png)

*Figure 23.3*

就读取和写入文件而言，我们最关心的类如下：

- `FileStream`—此类用于在文件中读取和写入二进制数据。
- `StreamReader` 和 `StreamWriter`—这些类专门设计用于从流中读取和写入，提供文本格式的 API。
- `BinaryReader` 和 `BinaryWriter`—这些类设计用于读取和写入流，提供二进制数据的 API。

使用这些类与直接使用底层流对象之间的区别在于，基本流以字节为单位工作。例如，假设作为保存某文档过程的一部分，你想将一个类型为 `long` 的变量的内容写入二进制文件。每个 `long` 占用 8 个字节，如果你使用普通的二进制流，你必须显式写入那 8 个字节的内存。

在 C# 代码中，你必须执行一些按位操作来从 `long` 值中提取那 8 个字节。使用 `BinaryWriter` 实例，你可以将整个操作封装在 `BinaryWriter.Write` 方法的重载中，该方法接受一个 `long` 作为参数，并将那 8 个字节放入流中（如果流指向文件，则放入文件）。相应的 `BinaryReader.Read` 方法从流中提取 8 个字节并恢复 `long` 的值。

## Working with File Streams

让我们开始编程流读取和写入文件。`FileStream` 实例用于从文件读取或向文件写入数据。要构造一个 `FileStream`，你需要四条信息：

1. 你想要访问的 *file*。
2. *mode*，指示你想要如何打开文件。例如，你是打算创建新文件还是打开现有文件？如果你打开现有文件，写入操作应解释为覆盖文件内容还是追加到文件？
3. *access*，指示你想要如何访问文件。例如，你想要从文件中读取、写入文件还是同时进行？
4. *share* 访问，指定你是否想要独占访问文件。或者，你是否愿意让其他流同时访问文件？如果是，是否应允许其他流读取文件、写入文件或同时进行？

第一条信息通常由包含文件完整路径名的字符串表示，本章仅考虑需要此处的字符串的构造函数。除此之外，还有一些额外的构造函数接受对文件的原生 Windows 句柄。其余三条信息由三个 .NET 枚举 `FileMode`、`FileAccess` 和 `FileShare` 表示。这些枚举的值在下表中列出，并且不言自明：

| Enumeration | Values |
|---|---|
| `FileMode` | `Append`, `Create`, `CreateNew`, `Open`, `OpenOrCreate`, or `Truncate` |
| `FileAccess` | `Read`, `ReadWrite`, or `Write` |
| `FileShare` | `Delete`, `Inheritable`, `None`, `Read`, `ReadWrite`, or `Write` |

请注意，在 `FileMode` 的情况下，如果你请求与文件现有状态不一致的模式，则可能会抛出异常。`Append`、`Open` 和 `Truncate` 如果文件尚不存在则抛出异常，而 `CreateNew` 如果文件存在则抛出异常。`Create` 和 `OpenOrCreate` 可以处理两种情况，但 `Create` 会删除任何现有文件以替换为新的、初始为空的文件。`FileAccess` 和 `FileShare` 枚举是按位标志，因此值可以用 C# 按位或运算符 `|` 组合。

### Creating a FileStream

StreamSamples 的示例代码使用了以下依赖项和命名空间：

**Dependencies**
- `NETStandard.Library`
- `System.IO.FileSystem`

**Namespaces**
- `System`
- `System.Collections.Generic`
- `System.Globalization`
- `System.IO`
- `System.Linq`
- `System.Text`
- `System.Threading.Tasks`
- `static System.Console`

`FileStream` 有大量构造函数。以下示例使用一个具有四个参数的构造函数（代码文件 StreamSamples/Program.cs）：

- 文件名
- 具有 Open 值的 FileMode 枚举以打开现有文件
- 具有 Read 值的 FileAccess 枚举以读取文件
- 具有 Read 值的 FileShare 枚举以允许其他程序同时读取但不更改文件

```csharp
private void ReadFileUsingFileStream(string fileName)
{
    const int bufferSize = 4096;
    using (var stream = new FileStream(fileName, FileMode.Open,
        FileAccess.Read, FileShare.Read))
    {
        ShowStreamInformation(stream);
        Encoding encoding = GetEncoding(stream);
        //...
```

代替使用 FileStream 类的构造函数创建 FileStream 对象，你也可以使用 File 类的 OpenRead 方法直接创建 FileStream。OpenRead 方法打开文件（类似于 FileMode.Open），返回可读取的流（FileAccess.Read），并且还允许其他进程读取访问（FileShare.Read）：

```csharp
using (FileStream stream = File.OpenRead(filename))
{
    //...
```

### Getting Stream Information

Stream 类定义了 CanRead、CanWrite、CanSeek 和 CanTimeout 属性，你可以读取它们以获取有关流可以执行的操作的信息。对于读写流，超时值 ReadTimeout 和 WriteTimeout 指定以毫秒为单位的超时。设置这些值在网络场景中可能很重要，以确保用户在读取或写入流失败时不必等待太久。Position 属性返回流中光标的当前位置。每次从流读取一些数据时，位置都会移动到下一个将被读取的字节。示例代码将有关流的信息写入控制台（代码文件 StreamSamples/Program.cs）：

