
```csharp
public class TextReaderWriter
{
    public static void Main()
    {
        string tempPath = Path.GetTempFileName();
        string tempPath2 = Path.GetTempFileName();

        if (File.Exists(tempPath))
        {
            using (StreamReader reader = File.OpenText(tempPath))
            {
                string buffer = null;

                using (StreamWriter writer = new StreamWriter(tempPath2))
                {
                    while ((buffer = reader.ReadLine()) != null)
                    {
                        writer.WriteLine(buffer);
                    }
                }
            }
        }
    }
}
```

## 动手试一试

### 缓冲读取和写入

若要使用 `File`、`StreamReader` 和 `StreamWriter` 类执行文本读取和写入，请遵循以下步骤：

1. 在 Visual Studio 中打开 `TextReadWrite` 项目。

2. 双击该文件打开 `Program.cs`。

3. `Main` 方法中已包含部分代码，其中包括一个与列表 13.3 中所示类似的 `if` 语句。修改该 `if` 语句的语句块，以读取并写入 `fileName` 字段中指示的文件。请参考列表 13.7 中的代码作为指南。

4. 修改 `while` 语句，在每次 `Write` 之后递增 `bufferCounter` 字段。

5. 使用 `Ctrl+F5` 运行应用程序。输出结果应与图 13.4 中所示的内容相似。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_325_0.png)

**图 13.4** 执行缓冲读取和写入的结果

## 使用 File 类读取和写入数据

由于从文件读取和写入数据（无论是文本还是二进制）是一项常见任务，`File` 类提供了几个使此过程比直接处理流更便捷的方法。

要读取或写入二进制数据，可以分别使用 `ReadAllBytes` 和 `WriteAllBytes` 方法。这些方法打开文件，读取或写入字节，然后关闭文件。列表 13.8 中所示的代码使用 `ReadAllBytes` 和 `WriteAllBytes` 方法执行与列表 13.5 相同的操作。

**列表 13.8 使用 File 类进行二进制读取和写入**

```csharp
public class BinaryReaderWriterFile
{
    public static void Main()
    {
        string tempPath = Path.GetTempFileName();
        string tempPath2 = Path.GetTempFileName();

        if (File.Exists(tempPath))
        {
            byte[] data = File.ReadAllBytes(tempPath);
            File.WriteAllBytes(tempPath2, data);
        }
    }
}
```

使用 `ReadAllLines` 和 `ReadAllText` 方法读取以及 `WriteAllLines` 和 `WriteAllText` 方法写入，读取和写入文本数据同样简单。`ReadAllLines` 方法将文件中的所有行读取到一个字符串数组中，其中每一行都是数组中的一个新元素，而 `ReadAllText` 将所有行读取到一个单个字符串中。

`WriteAllLines` 方法将字符串数组的每个元素写入文件，而 `WriteAllText` 方法将字符串的内容写入文件。这两种方法都会创建一个新文件，或者如果文件已存在则覆盖该文件。要向现有文件追加文本，你可以使用 `AppendAllLines` 或 `AppendAllText` 方法。如果需要打开一个流，你可以使用 `AppendText` 方法。

列表 13.9 中所示的代码使用 `ReadAllLines` 和 `WriteAllLines` 方法执行与列表 13.7 相同的操作。

**列表 13.9 使用 ReadAllLines 和 WriteAllLines**

```csharp
public class TextReaderWriterFile
{
    public static void Main()
    {
        string tempPath = Path.GetTempFileName();
        string tempPath2 = Path.GetTempFileName();

        if (File.Exists(tempPath))
        {
            string[] data = File.ReadAllLines(tempPath);
            File.WriteAllLines(tempPath2, data);
        }
    }
}
```

使用 `ReadAllLines` 甚至 `ReadAllText` 的一个缺点是，整个文件必须首先被读入内存。为了解决这个问题并返回一个 `IEnumerable<string>` 集合，您可以使用 `ReadLines` 方法。由于该方法返回一个 `IEnumerable<string>`，您可以立即开始遍历返回的集合，而无需等待整个集合返回。清单 13.10 中显示的代码使用 `File.ReadLines` 方法执行与清单 13.9 相同的操作。

## 清单 13.10 使用 WriteAllLines 和 ReadLines

```csharp
public class TextReaderWriterFile
{
    public static void Main()
    {
        string tempPath = Path.GetTempFileName();
        string tempPath2 = Path.GetTempFileName();

        if (File.Exists(tempPath))
        {
            File.WriteAllLines(tempPath, File.ReadAllLines(tempPath2));
        }
    }
}
```

## 本章小结

在本小时的学习中，您学习了如何使用流来读写文本和二进制文件。虽然您只专注于使用 `FileStream` 和 `StreamWriter` 类，但使用 `FileStream` 进行读写的机制对于任何 `Stream` 派生类来说本质上是相同的。

您还学习了 .NET Framework 如何通过 `File`、`Directory`、`FileInfo`、`DirectoryInfo` 和 `Path` 类简化对文件、目录和字符串路径的操作。

## 问答

- **问。** *什么是流？*

  - **答。** 流是表示为字节的数据包的顺序流动。数据流具有底层存储介质，通常称为后备存储，它为流提供来源。

- **问。** 相对路径和绝对路径之间有什么区别？

  - **答。** 绝对路径完全指定了一个位置，而相对路径指定了一个部分位置。使用相对路径时，当前位置是定位指定文件的起点。

- **问。** `FileSystemInfo` 类用于什么？

  - **答。** `FileSystemInfo` 类包含文件和目录操作共用的方法，可以表示文件也可以表示目录。它是 `DirectoryInfo` 和 `FileInfo` 类的基类。

- **问。** `Directory` 类与 `DirectoryInfo` 类有什么不同？

  - **答。** `Directory` 类仅提供静态方法，而 `DirectoryInfo` 类仅提供实例方法，并缓存指定目录的信息。

- **问。** 二进制文件和文本文件之间有什么区别？

  - **答。** 二进制文件只是字节的流，而文本文件则已知仅包含文本数据。

## 练习室

### 测验

1. `Path` 类的成员如何与文件系统直接交互？

2. 应该在 `FileSystemInfo` 实例上使用什么方法来更新其中包含的缓存信息？

3. `DirectoryInfo` 和 `Directory` 类上的 `EnumerateDirectories` 方法之间有什么区别？

4. `File.OpenRead` 方法的返回类型是什么？

5. `File.OpenText` 方法的返回类型是什么？

6. `File.ReadAllLines` 方法和 `File.ReadLines` 方法之间有什么区别？

### 答案

1. 大多数 `Path` 类成员不与文件系统交互；不过，它们确实会验证指定的路径字符串是否包含有效字符。

2. `FileSystemInfo` 类包含一个 `Refresh` 方法，应使用该方法来更新缓存的文件或目录信息。

3. `DirectoryInfo.EnumerateDirectories` 返回 `IEnumerable<DirectoryInfo>`，而 `Directory.EnumerateDirectories` 返回 `IEnumerable<string>`。

4. `File.OpenRead` 方法返回一个仅用于读取指定文件的 `FileStream`。

5. `File.OpenText` 方法返回一个打开指定文本文件的 `StreamReader`。

6. `File.ReadAllLines` 必须将整个文件读入内存并返回包含行的字符串数组，而 `File.ReadLines` 返回 `IEnumerable<string>`，使您能够在读取整个文件之前开始遍历集合。

### 练习

1. 修改 `PhotoCollection` 类，将 `directory` 字段替换为名为 `directoryInfo` 的字段，其数据类型为 `DirectoryInfo` 类。修改 `Path` 属性，使 `get` 访问器返回 `FullName` 属性的值，而 `set` 访问器在验证 `value` 不为 `null` 或空字符串后，从 `value` 创建一个新的 `DirectoryInfo` 实例。

2. 添加一个名为 `Update` 的私有方法，该方法执行以下操作：

   - a. 清空集合。

   - b. 如果 `DirectoryInfo.Exists` 为 `true`，则遍历目录中所有扩展名为“.jpg”的文件，并将一个新的 `Photo` 实例添加到集合中。此代码应放在一个捕获 `DirectoryNotFoundException` 的 `try-catch` 块中。`catch` 处理程序应包含以下代码：

```csharp
System.Windows.MessageBox.Show("No Such Directory");
```

## 第 14 小时

## 处理 XML

**您将在本小时学到的内容：**

- 理解 XML DOM

- 使用 LINQ to XML

- 选择和查询 XML

- 修改 XML

虽然处理文本文件很常见，并且通过 `System.IO` 命名空间提供的类变得更加容易，但这些类并不便于您轻松地以 XML 形式处理和操作结构化文本。XML 代表可扩展标记语言（Extensible Markup Language），是一种简单且灵活的文本文本格式，能够以平台无关的方式交换数据。

XML 作为数据交换格式的使用不仅流行于 .NET Framework，也流行于其他 Microsoft 产品中。.NET Framework 通过 SOAP 和 Windows 通信基础（WCF）将其用于 Web 服务，将其用作 Windows 呈现基础（WPF）和 Silverlight 可扩展应用程序标记语言（XAML）文件的文件格式，用作 Windows 工作流基础（WF）文件的文件格式，并且是 ADO.NET 的一部分。

尽管 XML 基于文本且人类可读，但必须有一种方法来以编程方式操作 XML。这是通过使用 XML 解析器实现的。.NET Framework 提供两种 XML 解析器。一种是基于流的解析器，它读取 XML 流时进行解析；另一种是基于树的解析器，必须在构建树之前将整个流读入内存。

在本小时中，您将了解 .NET Framework 提供的不同 XML 类，以及如何使用它们来创建和操作 XML 文件。

### 理解 XML DOM

为了以编程方式读取和操作 XML 文档，它必须通过 XML 文档对象模型（DOM）在内存中表示。DOM 提供了一种通用且结构化的方式来表示内存中的 XML 数据，最常用于将 XML 数据读入内存以更改其结构、添加或删除元素，或修改元素中包含的数据。

清单 14.1 显示了一个示例 XML 文档，图 14.1 显示了相应的 DOM 结构。

## 清单 14.1 XML 数据

```xml
<books>
   <book>
      <title>Sams Teach Yourself Visual C# 2010 in 24 Hours</title>
      <isbn-10>0-672-33101-2</isbn-10>
      <author>Dorman</author>
      <price currency="US">39.99</price>
      <publisher>
         <name>Sams Publishing</name>
         <state>IN</state>
      </publisher>
   </book>
</books>
```

**图 14.1** XML DOM 表示

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_332_0.png)

在图 14.1 中，每个圆圈代表 XML 数据中的一个元素。较浅的圆圈代表**文档根**，即起始元素。文档根节点是包含文档本身的顶级节点。除文档根以外的所有节点都有一个单一的父节点，即直接位于它们上方的节点。当节点具有相同的父节点时，例如 `author`、`isbn-10`、`publisher`、`price` 和 `title` 节点，它们是该父节点的子节点或后代节点。处于同一层级的节点是兄弟节点。

### 使用 LINQ to XML

LINQ to XML 通过 LINQ 扩展方法公开 XML DOM，使您能够操作和查询已加载到内存中的 XML 文档。使用 LINQ to XML 创建和操作 XML 文档所需的所有类都包含在 `System.Xml.Linq` 命名空间中。最常用类如图 14.2 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_333_0.png)

## XDocument

`XDocument` 类表示一个 XML 文档实例。除非您需要指定文档类型声明、处理指令（由 XML 解析器使用）或顶级注释，否则您很少与 `XDocument` 实例交互。相反，您应该使用 `XElement` 类。

## XElement 和 XAttribute

`XElement` 类表示一个 XML 元素，是最常用的类之一，提供了许多用于创建、修改和查询 XML 数据的有用方法和属性。XML 属性是与 XML 元素关联的名称-值对，由 `XAttribute` 类表示。与元素不同，它们

而不是 XML 树中的节点。因为属性只是与元素关联的名称-值对，所以它们必须拥有仅在该元素内唯一的名称。

`XElement` 类包含该元素的属性列表。`XAttribute` 类中最常用的属性是 `NextAttribute` 和 `PreviousAttribute`，它们对于浏览元素上的属性序列非常有用。

使用 `XElement` 实例创建列表 14.1 中 XML 的代码如列表 14.2 所示。

## 列表 14.2 使用 LINQ to XML 创建 XML

```csharp
XElement document = new XElement("books",
new XElement("book",
new XElement("title", "Sams Teach Yourself Visual C# 2010 in 24 Hours"),
new XElement("isbn-10", "0-672-33101-2"),
new XElement("author", "Dorman"),
new XElement("price", new XAttribute("currency", "US"), 39.99M),
new XElement("publisher",
new XElement("name", "Sams Publishing"),
new XElement("state", "IN")))));
```

相比之下，使用由 `System.Xml` 命名空间中的类支持的标准 DOM 方法，如列表 14.3 所示。

## 列表 14.3 使用 XML DOM 创建 XML
