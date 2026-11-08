
### FileStream 类

FileStream 类用作缓冲区，以便对文件执行打开、读取和写入等操作。每当我们要以文件模式（例如读取或写入）打开文件时，都需要先声明 FileStream 对象来存储文件流。这有助于稍后操作文件内容，从而提高文件系统的性能。在 C# 中，可以按如下方式声明 FileStream 类的实例：

```csharp
FileStream fileStream = new FileStream(@"C:\Document & Settings\Book\",
    FileAccess.ReadWrite);

or,

FileStream fileStream = new FileStream(@"c:\Document & Settings\Book\", FileMode.Open,
    FileAccess.ReadWrite);
```

C# 提供了 15 个重载构造函数来创建 FileStream 类的实例。

FileStream 类允许同步和异步读写操作。此外，它还允许通过其方法自由读取文件的特定部分。FileStream 类是公共类，其所有方法也都是公共的。

表21.1列出了 FileStream 类的重要方法：

**表21.1：FileStream 类的重要方法**

| 方法 | 描述 |
| --- | --- |
| `BeginRead(byte[] bytes, int offset, int numByte, AsyncCallback callBack, Object stateObject)` | 指开始异步读取的方法。 |
| `BeginWrite(byte[] bytes, int offset, int numByte, AsyncCallback callBack, Object stateObject)` | 指开始异步写入的方法。 |
| `Close()` | 关闭 FileStream 对象并释放该对象使用的所有资源。它还会关闭底层已打开的流。 |
| `Dispose()` | 释放 FileStream 对象持有的所有系统资源。 |
| `EndRead(IAsyncResult asyncResult)` | 等待挂起的异步读取进程完成其读取操作。 |
| `EndWrite(IAsyncResult asyncResult)` | 结束写入操作，并在 I/O 操作完成后释放 I/O 资源。 |
| `Flush()` | 刷新当前 FileStream 对象已使用的缓冲区。此方法还会将缓冲的数据写入文件系统。 |
| `Lock(long position, long lengthToRead)` | 在文件具有读取访问权限时锁定其他 I/O 操作。通过指定位置和长度，用户可以限制文件的重要部分不被修改。 |
| `Read(char[] buffer, int index, int count)` | 从输入 FileStream 中读取指定数量的字符，并将它们从索引位置开始存储到缓冲区中。此方法还以整数形式返回下一个字符位置。 |
| `ReadByte()` | 从 FileStream 对象读取字节，并将位置索引增加一个字节。 |
| `Seek(long offset, SeekOrigin seekOrigin)` | 在文件中查找确定的位置。它将文件指针的当前位置设置为给定值。 |
| `Unlock(long position, long lengthToRead)` | 解锁之前锁定的所有 I/O 操作。 |
| `Write(char[] buffer, int index, int count)` | 将字符缓冲区中存储的字符写入，并从指定索引点开始统计字符数。 |
| `WriteByte(byte byteValue)` | 将作为参数传递的字节写入当前文件位置。 |

下面我们来了解 StreamReader 类。

### StreamReader 类

StreamReader 类用于从文本文件或使用指定编码的文档中读取文本。默认情况下，StreamReader 类使用 UTF-8 编码读取文本。不过，它也可以使用自定义编码读取文本。

可以按如下方式声明 StreamReader 对象：

```csharp
StreamReader streamReader = new StreamReader(stream);
StreamReader streamReader = new StreamReader(stream, System.Text.Encoding.UTF8);
StreamReader streamReader = new StreamReader(path);
StreamReader streamReader = new StreamReader(path, System.Text.Encoding.UTF8);
```

在上述声明中，path 是字符串变量，包含将要读取文本的文件的路径；而 stream 是 Stream 类的对象，读取操作将在其中进行。C# 为 StreamReader 类提供了 10 个重载构造函数；不过，上述四个构造函数在编程中广泛使用。

表21.2显示了 StreamReader 类的重要方法：

**表21.2：StreamReader 类的重要方法**

| 方法 | 描述 |
| --- | --- |
| `Close()` | 关闭 StreamReader 对象并释放该对象使用的所有资源。 |
| `Dispose()` | 释放 StreamReader 对象持有的所有系统资源。 |
| `Peek()` | 检索下一个可用字符的位置。它仅以整数形式返回下一个字符的位置。 |
| `Read()` | 从流中读取下一个字符，并将字符位置指针增加 1。下一个字符的位置已以整数形式返回。**重载：** `Read(char[] buffer, int index, int count)` 从输入流中读取指定数量的字符，并将它们从索引位置开始存储到缓冲区中。此方法还以整数形式返回下一个字符位置。 |
| `ReadBlock(char[] buffer, int index, int count)` | 从输入流中读取指定数量的字符，并将它们从索引位置开始存储到缓冲区中。此方法还以整数形式返回下一个字符位置。 |

表21.4列出了 Directory 类的重要方法：

**表21.4：Directory 类的重要方法**

| 方法 | 描述 |
| --- | --- |
| `CreateDirectory(string path)` | 在用户指定位置创建具有已定义 Windows 安全性的目录。<br>它返回 *DirectoryInfo* 类的对象。它只接受用户定义的路径作为参数。<br>**重载：**<br>• `CreateDirectory(string path, System.Security.AccessControl.DirectorySecurity directorySecurity)` → 在指定位置创建目录，并使用 DirectorySecurity 对象中指定的已定义 Windows 安全属性。 |
| `Delete(string path)` | 从指定位置删除目录；如果指定，还会删除该目录下的子目录。<br>它只接受用户定义的路径作为参数。<br>**重载：**<br>• `Delete(string path, bool IsRecursive)` → 如果 IsRecursive 设置为 true，则删除该目录内的所有子目录。 |
| `Exists()` | 检查用户指定路径中是否存在目录。如果存在，则返回 true；否则，返回 false。<br>它只接受用户定义的路径作为参数。 |
| `GetCurrentDirectory()` | 返回包含当前工作目录列表的字符串列表。 |
| `GetDirectories(string path)` | 返回包含指定路径中目录列表的字符串列表。<br>它只接受用户定义的路径作为参数。<br>**重载：**<br>• `GetDirectories(string path, string searchPattern)` → 从指定位置返回具有特定 searchPattern（例如 Root 或 Personal）的目录列表。<br>• `GetDirectories(string path, string searchPattern, SearchOptions searchOptions)` → 如果 searchOptions 设置为 AllDirectory 选项，则返回当前目录及其子目录中的所有目录。对于 TopDirectoryOnly 选项，它从 path 变量中提到的目录路径返回文件列表。 |
| `GetFiles(string path)` | 返回指定路径中存在的文件列表。<br>它只接受用户定义的路径作为参数。<br>**重载：**<br>• `GetFiles(string path, string searchPattern)` → 从指定位置返回具有特定 searchPattern（例如 .doc 或 .txt）的文件列表。<br>• `GetFiles(string path, string searchPattern, SearchOptions searchOptions)` → 如果 searchOptions 设置为 AllDirectory 选项，则返回当前目录及其子目录中的所有文件。对于 TopDirectoryOnly 选项，它从 path 变量中提到的目录路径返回文件列表。 |

