

```csharp
checked {
    a = 2;
    b = 7;
    result = checked((byte)(a * b)); // this is OK
    Console.WriteLine("Checked result: " + result);
    a = 127;
    b = 127;
    result = checked((byte)(a * b)); // this causes exception
    Console.WriteLine("Checked result: " + result); // won't execute
}
catch (OverflowException exc) {
    Console.WriteLine(exc);
}
}
```

程序的输出如下所示：

```
Unchecked result: 1
Unchecked result: 113
Checked result: 14
System.OverflowException: Arithmetic operation resulted in an overflow.
at CheckedBlocks.Main()
```

如你所见，unchecked 块会导致溢出被截断。当 checked 块中发生溢出时，会引发异常。

你可能需要使用 checked 或 unchecked 的一个原因是，溢出的默认 checked/unchecked 状态由编译器选项的设置和执行环境本身决定。因此，对于某些类型的程序，最好显式指定溢出检查状态。

## 第14章 使用 I/O

本书前面的章节已经使用了 C# I/O 系统的部分内容，例如 Console.WriteLine()，但并没有做太多正式解释。由于 I/O 系统建立在类的层次结构之上，如果不先讨论类、继承和异常，就不可能介绍其理论和细节。现在是详细研究 I/O 的时候了。由于 C# 使用 .NET Framework 定义的 I/O 系统和类，因此讨论 C# 下的 I/O 通常也是在讨论 .NET I/O 系统。

本章将讨论控制台 I/O 和文件 I/O。请注意，I/O 系统相当庞大。本章介绍最重要和最常用的功能。

## C# 的 I/O 建立在流之上

C# 程序通过流执行 I/O。流是一种抽象，它要么产生信息，要么消费信息。流由 I/O 系统链接到物理设备。所有流的行为方式都相同，即使它们所链接的实际物理设备不同。因此，I/O 类和方法可以应用于许多类型的设备。例如，用于写入控制台的相同方法也可以用于写入磁盘文件。

## 字节流和字符流

在最底层，所有 C# I/O 都基于字节进行操作。这是合理的，因为许多设备在进行 I/O 操作时是面向字节的。不过，我们人类常常更喜欢使用字符进行交流。回想一下，在 C# 中，char 是 16 位类型，而 byte 是 8 位类型。如果使用的是 ASCII 字符集，那么在 char 和 byte 之间转换很容易；只需忽略 char 值的高位字节即可。但这对于其余 Unicode 字符并不适用，这些字符需要两个字节（甚至可能更多）。因此，字节流并不完全适合处理基于字符的 I/O。为了解决这个问题，.NET Framework 定义了若干类，将字节流转换为字符流，并自动处理字节到字符以及字符到字节的转换。

## 预定义流

所有使用 System 命名空间的程序都可以使用三个预定义流，它们由名为 Console.In、Console.Out 和 Console.Error 的属性公开。Console.Out 指标准输出流。默认情况下，这就是控制台。例如，当你调用 Console.WriteLine() 时，它会自动将信息发送到 Console.Out。Console.In 指标准输入，默认情况下是键盘。Console.Error 指标准错误流，默认情况下也是控制台。但是，这些流可以重定向到任何兼容的 I/O 设备。标准流是字符流。因此，这些流读取和写入字符。

## 流类

.NET Framework 同时定义了字节流类和字符流类。不过，字符流类实际上只是包装器，它们将底层字节流转换为字符流，并自动处理任何转换。因此，字符流虽然在逻辑上是独立的，但建立在字节流之上。

核心流类定义在 System.IO 命名空间中。要使用这些类，通常需要在程序顶部附近包含以下语句：

```
using System.IO;
```

不必为控制台输入和输出指定 System.IO 的原因是，Console 类定义在 System 命名空间中。

## Stream 类

核心流类是 System.IO.Stream。Stream 表示字节流，是所有其他流类的基类。它也是抽象的，这意味着不能实例化 Stream 对象。Stream 定义了一组标准流操作。表14-1列出了 Stream 定义的几个常用方法。

表14-1中显示的若干方法在发生 I/O 错误时会抛出 IOException。如果尝试了无效操作，例如尝试写入只读流，则会抛出 NotSupportedException。根据具体方法的不同，还可能发生其他异常。

| 方法 | 描述 |
|---|---|
| void Close() | 关闭流。 |
| void Flush() | 将流的内容写入物理设备。 |
| int ReadByte() | 返回下一个可用输入字节的整数表示。遇到文件末尾时返回 -1。 |
| int Read(byte[] buf, int offset, int numBytes) | 尝试从 buf[offset] 开始，最多将 numBytes 个字节读入 buf，并返回成功读取的字节数。 |
| long Seek(long offset, SeekOrigin origin) | 将流中的当前位置设置为距指定 origin 的指定 offset。它返回新位置。 |
| void WriteByte(byte b) | 向输出流写入单个字节。 |
| int Write(byte[] buf, int offset, int numBytes) | 从数组 buf 中从 buf[offset] 开始，写入 numBytes 个字节的子范围。返回写入的字节数。 |

请注意，Stream 定义了读取和写入数据的方法。然而，并非所有流都支持这两种操作，因为可以打开只读流或只写流。此外，并非所有流都支持通过 Seek() 进行位置请求。要确定某个流的能力，需要使用 Stream 的一个或多个属性。这些属性如表14-2所示。表中还显示了 Length 和 Position 属性，它们包含流的长度及其当前位置。

## 字节流类

若干具体字节流派生自 Stream。System.IO 命名空间中定义的那些流如下所示：

| 流类 | 描述 |
|---|---|
| BufferedStream | 包装字节流并添加缓冲。缓冲在许多情况下可提升性能。 |
| FileStream | 专用于文件 I/O 的字节流。 |
| MemoryStream | 使用内存进行存储的字节流。 |
| UnmanagedMemoryStream | 使用非托管内存进行存储的字节流。 |

.NET Framework 还支持其他若干具体流类，它们提供对压缩文件、套接字和管道等的支持。也可以派生自己的流类。不过，对于绝大多数应用程序而言，内置流已经足够。

## 字符流包装类

要创建字符流，请将字节流包装在某个字符流包装器中。字符流层次结构的顶部是抽象类 TextReader 和 TextWriter。TextReader 处理输入，TextWriter 处理输出。这两个抽象类定义的方法可供其所有子类使用。因此，它们构成了所有字符流都会具备的一组最小 I/O 功能。

| 方法 | 描述 |
|---|---|
| bool CanRead | 如果流可读，则此属性为 true。此属性为只读。 |
| bool CanSeek | 如果流支持位置请求，则此属性为 true。此属性为只读。 |
| bool CanTimeout | 如果流可以超时，则此属性为 true。此属性为只读。 |
| bool CanWrite | 如果流可写，则此属性为 true。此属性为只读。 |
| long Length | 此属性包含流的长度。此属性为只读。 |
| long Position | 此属性表示流的当前位置。此属性为读/写。 |
| int ReadTimeout | 此属性表示读取操作发生超时之前的时间长度。此属性为读/写。 |
| int WriteTimeout | 此属性表示写入操作发生超时之前的时间长度。此属性为读/写。 |

