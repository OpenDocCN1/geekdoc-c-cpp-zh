
![](img/36e48639a06772bcb0fa1ea2525b33a3_876_0.png)

## 第 13 章

## 使用文件

本章将学习：

- 了解 `System.IO` 命名空间
- 探索 `File` 和 `Directory` 类
- 对比 `FileInfo` 和 `DirectoryInfo` 类与 `File` 和 `Directory` 类
- 了解如何使用流类
- 从文本文件读取数据
- 将数据写入文本文件
- 探索向文本文件追加数据
- 使用异常处理技术处理文本文件
- 读取和写入二进制文件

本章将介绍如何为应用程序使用来自键盘以外数据源的数据。你将了解用于处理文件和目录系统的主要类。你将编写访问存储数据的程序，以及将结果存储到文件中的程序。你还将扩展处理输入和输出相关异常的知识。本章将向你介绍创建、打开、关闭、读取和写入文件的基础知识。

## System.IO 命名空间

数据文件是一种计算机文件，可由计算机程序处理、操作或用作输入。计算机程序也会创建数据文件作为输出。数据文件被视为具有持久或长期存储的命名字节集合。处理数据文件时，你会从目录路径、磁盘存储以及文件和目录名称的角度来考虑。.NET Framework 包含 System.IO 命名空间，它提供基本的文件和目录支持类。它还包含使你能够读取和写入文件及数据流的类型。

提到流时，你会想到沿单一方向流动的东西。数据流是数据从源到单个接收器的流动。C# 与许多其他编程语言一样，使用流来向后备介质（如磁盘存储）写入字节或从中读取字节。作为 System.IO 命名空间一部分定义的许多类类型都是围绕流设计的。表 13-1 列出了本章探讨的类型。

### 表 13-1 System.IO 类

| 类 | 描述 |
|---|---|
| BinaryReader | 将基元数据类型作为二进制值读取 |
| BinaryWriter | 将基元类型以二进制形式写入流 |
| Directory | 公开用于创建和遍历目录及子目录的静态方法 |
| DirectoryInfo | 公开用于创建和遍历目录及子目录的实例方法 |
| DirectoryNotFoundException | 当找不到文件或目录的一部分时引发的异常 |
| EndOfStreamException | 当尝试读取超过流末尾时引发的异常 |
| File | 提供用于创建、复制、删除、移动和打开文件的静态方法，并协助创建 FileStream 对象 |
| FileInfo | 提供用于创建、复制、删除、移动和打开文件的实例方法，并协助创建 FileStream 对象 |
| FileLoadException | 当找到文件但无法加载时引发的异常 |
| FileNotFoundException | 当尝试访问磁盘上不存在的文件失败时引发的异常 |
| FileStream | 公开围绕文件的流，支持同步和异步读写操作 |
| InvalidDataException | 当数据流格式无效时引发的异常 |
| IOException | 当发生 I/O 错误时引发的异常 |
| Stream | 提供字节序列的通用视图 |
| StreamReader | 实现从字节流读取字符的 TextReader |
| StreamWriter | 实现用于将字符写入流的 TextWriter |
| TextReader | 表示可读取顺序字符序列的读取器；此类为抽象类 |
| TextWriter | 表示可写入顺序字符序列的写入器；此类为抽象类 |

如表 13-1 所示，许多 System.IO 类型都是异常类，在使用流、文件和目录访问信息时可能会引发这些异常。其他类型则涉及创建和访问 FileStream 对象。表 13-1 中所示的四个类提供了用于复制、删除、移动和打开文件和目录的方法。首先讨论这些类。

## File 和 Directory 类

File、FileInfo、Directory 和 DirectoryInfo 类被视为实用工具类。它们通常与流对象一起工作，使你能够操作文件和目录结构。File 和 Directory 类仅公开静态成员。图 13-1 展示了 System.IO 命名空间中的一些类。

![](img/36e48639a06772bcb0fa1ea2525b33a3_879_0.png)

图 13-1 .NET 文件类层次结构

如图 13-1 所示，System.IO 命名空间的类层次结构很有意思。File 和 Directory 类都是 object 类的直接后代，而其他类则是 MarshalByRefObject 类的后代。正如 MSDN 文档所述，MarshalByRefObject 是通过使用代理交换消息跨应用程序域边界通信的对象的基类。不从 MarshalByRefObject 继承的对象隐式按值封送。包含三个点的框表示派生其他类的位置。

FileInfo 和 DirectoryInfo 扩展 FileSystemInfo 类。StreamReader 和 StreamWriter 扩展 TextReader 和 TextWriter 类。

## File 类

图 13-1 所示的 IO.File 类提供静态方法，帮助复制、移动、重命名、创建、打开、删除和追加文件。由于它们只公开静态成员，因此无法从该类实例化对象。表 13-2 列出了关键静态成员并提供了简要描述。

### 表 13-2 File 类静态成员

| 静态成员 | 描述 |
|---|---|
| AppendAllText ( ) | 将指定字符串追加到文件；如果文件尚不存在，则创建该文件 |
| AppendText ( ) | 创建一个将 UTF-8 编码文本追加到现有文件的 StreamWriter |
| Copy ( ) | 将现有文件复制到新文件 |
| Create ( ) | 在指定路径中创建文件 |
| Delete ( ) | 删除指定文件 |
| Exists ( ) | 确定指定文件是否存在 |
| GetCreationTime ( ) | 返回指定文件的创建日期和时间 |
| GetLastAccessTime ( ) | 获取指定文件最后被访问的日期和时间 |
| GetLastWriteTime ( ) | 获取指定文件最后被写入的日期和时间 |
| Move ( ) | 将指定文件移动到新位置 |

**注意** 静态方法也可用于 SetAccessControl、SetAttributes、SetCreationTime、SetLastAccessTime 和 SetLastWriteTime。

IO.File 类的每个成员都是具有 public static 访问修饰符的方法。回想一下，当方法使用 static 修饰符时，该方法属于类本身，而不属于类的特定对象。调用该方法不需要实例化类的对象。要调用方法，方法名前面要加上类名（而不是对象名）。例如，要调用 Copy ( ) 方法复制 sourceFile 并将新文件命名为 targetFile，你会这样写：

```csharp
File.Copy("sourceFile", "targetFile");
```

这假定已包含 using System.IO 命名空间。否则，你需要完全限定名称。

**注意** 如前面几章所述，创建应用程序时，Visual Studio 会自动在源代码顶部插入一些 `using` 语句。`System.IO` 不在其中。你必须手动添加 `using System.IO;`。本章所示示例中已删除不需要的多余 `using` 语句。

如果使用 Visual Studio 创建应用程序并包含对 `System.IO` 命名空间的引用，则 IntelliSense 功能会在你开发应用程序时提供有用的信息。图 13–2 说明了当你选择 `File` 类的方法时，它如何显示 IO 异常类的列表。

![](img/36e48639a06772bcb0fa1ea2525b33a3_881_0.png)

**图 13–2** IntelliSense 显示

`File` 类的 `static` 方法之一是 `Exists()`。在编写访问文件中数据的程序语句之前，你应始终检查以确保文件可用。示例 13–1 演示了调用此方法以及其他几个返回文件信息的方法。

### 示例 13.1

```csharp
/* DirectoryStructure.cs
 * Illustrates using File and Directory utilities.
 */
using System;
using System.IO;       // Added for File Access

class DirectoryStructure
{
    public static void Main( )
    {
        string fileName = "BirdOfParadise.jpg";

        if (File.Exists(fileName))
        {
            Console.WriteLine("FileName: {0}", fileName);
            Console.WriteLine("Attributes: {0}",
                File.GetAttributes(fileName));
            Console.WriteLine("Created: {0}",
                File.GetCreationTime(fileName) );
            Console.WriteLine("Last Accessed: {0}",
                File.GetLastAccessTime(fileName));
        }
```
