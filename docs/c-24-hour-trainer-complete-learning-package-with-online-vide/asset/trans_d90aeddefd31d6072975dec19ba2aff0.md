
## 表 29-7

| 方法 | 用途 |
|---|---|
| AppendAllText | 将字符串追加到文件末尾。 |
| Copy | 将文件复制到新文件。 |
| Create | 创建文件。 |
| Decrypt | 解密由 Encrypt 方法加密的文件。 |
| Delete | 删除文件。 |
| Encrypt | 加密文件，使其只能由用于加密它的账户读取。 |
| Exists | 如果文件存在，则返回 true。 |
| GetAttributes | 返回文件的属性，如 ReadOnly、System 或 Hidden。 |
| GetCreationTime | 返回文件的创建时间。 |
| GetLastAccessTime | 返回文件的上次访问时间。 |
| GetLastWriteTime | 返回文件的上次写入时间。 |
| Move | 将文件移动到新位置。 |
| ReadAllBytes | 以字节数组形式返回文件内容。 |
| ReadAllLines | 以字符串数组形式返回文本文件中的各行。 |
| ReadAllText | 以字符串形式返回文本文件的内容。 |
| SetAttributes | 设置文件的属性。 |
| SetCreationTime | 设置文件的创建时间。 |
| SetLastAccessTime | 设置文件的上次访问时间。 |
| SetLastWriteTime | 设置文件的上次写入时间。 |
| WriteAllBytes | 从字节数组写入文件内容。 |
| WriteAllLines | 从字符串数组写入文本文件内容。 |
| WriteAllText | 从字符串写入文本文件内容。 |

## PATH

Path 类提供对文件路径执行字符串操作的静态方法。例如，可以使用 ChangeExtension 方法更改文件名的扩展名部分。表 29-8 总结了 Path 类最有用的方法。

## 表 29-8

| 方法 | 用途 |
|---|---|
| ChangeExtension | 更改文件名的扩展名。 |
| Combine | 合并两个路径字符串，如有需要则在它们之间添加反斜杠。 |
| GetDirectoryName | 返回路径中的目录名部分。 |
| GetExtension | 返回文件名的扩展名部分。 |
| GetFileName | 返回文件路径中的文件名部分。 |
| GetFileNameWithoutExtension | 返回文件路径中不带扩展名的文件名部分。 |
| GetTempFileName | 返回临时文件的名称。 |
| GetTempPath | 返回系统临时文件夹的路径。 |

## 流

计算机可以包含多种类型的文件：网页、视频、音频、可执行文件以及许多其他文件。然而，在某个层面上，文件都是相同的。它们只是存储在某个文件系统上的一系列字节。

在这种非常低的层面上考虑文件，可以让你统一地处理它们。它让你能够定义可用于操作任何类型文件的通用类和方法。

包括 C# 在内的许多编程语言通过定义流的概念，使在低层面上处理文件变得更加容易。流只是一个有序的字节序列。

> 注意 流也可以表示文件以外的事物。例如，流可以表示从一个程序发送到另一个程序的数据、从网站下载的一系列字节，或数据在加密或压缩等复杂过程中流动时的数据流。本节重点介绍文件流。

流对象提供在低层面操作数据的方法。例如，Stream 类提供 Read 和 Write 方法，用于在流和程序中的字节数组之间移动数据字节。

对某些程序而言，在这种低层面上使用流很方便，但它使日常的文件处理变得困难。你可能并不想从文本文件中读取字节，然后再将它们重新组合成字符。

StreamReader 和 StreamWriter 类使读写文本流变得容易得多。正如你可能从名称中猜到的那样，StreamReader 让你从流中读取文本，StreamWriter 让你将文本写入流。如果该流恰好表示文件，那么你就是在读写文件。

> **注意** *`StreamReader` 和 `StreamWriter` 类位于 `System.IO` 命名空间中。为了更方便地使用这些类，可以在代码中添加以下 using 指令：*
> 
> `using System.IO;`

### 写入文件

`StreamWriter` 类提供若干构造函数来构建与不同类型流关联的 `StreamWriter`。其中一个最简单的构造函数将文件名作为参数。它打开文件以供写入，并将新的 `StreamWriter` 与其关联。

> **注意** *请注意，`StreamWriter` 实现了 `IDisposable`，因此应在 `using` 块中使用它，以便自动调用其 `Dispose` 方法。*

以下代码展示了程序如何打开文件 Memo.txt 以供写入。如果该文件已存在，则会被覆盖。

```csharp
// Write into the file, overwriting it if it exists.
using (StreamWriter memoWriter = new StreamWriter("Memo.txt"))
{
    // Write into the file.
    ...
}
```

> **注意** *如果向构造函数传递一个不带路径的文件名（如 `Memo.txt`），程序会在其当前目录中创建该文件。你可以使用完全限定的文件名（如 `C:\Temp\Memo.txt`）在特定目录中创建文件。*

该类构造函数的另一个版本接受第二个 bool 参数，用于指示是否要打开文件以进行追加。如果将此参数设置为 true，`StreamWriter` 会打开现有文件并准备在末尾添加文本。如果文件不存在，该对象会静默创建新文件并准备追加。

StreamWriter 类提供 Write 方法向文件添加文本。WriteLine 方法添加文本并后跟一个换行符。Write 和 WriteLine 都有重载版本，可将各种数据类型写入文件：bool、char、string、int、decimal 等。它们还提供接受格式字符串和参数的版本，与 string.Format 方法非常相似。

StreamWriter 还提供了另一个我想在这里介绍的重要方法：Close。Close 方法关闭 StreamWriter 及其关联的文件。当你使用 Write 和 WriteLine 方法时，StreamWriter 实际上可能会在内存中缓冲其输出，并且只有在存储了足够的数据时才写入文件。Close 方法强制 StreamWriter 将其缓冲区刷新到文件中；在调用 Close 之前，数据可能实际上并不在文件中。如果你的程序崩溃或结束前没有调用 Close，那么你的部分或全部文本很可能会丢失。

以下代码展示了程序如何将 TextBox 的内容保存到文件中：

```csharp
// Write the file, overwriting it if it exists.
using (StreamWriter memoWriter = new StreamWriter("Memo.txt"))
{
    // Write the file.
    memoWriter.Write(memoTextBox.Text);
    memoWriter.Close();
}
```

### 读取文件

StreamReader 类让你能够轻松地从文件中读取文本。与 StreamWriter 类一样，StreamReader 提供一个构造函数，该构造函数接受一个给出要打开的文件名的参数。

如果文件不存在，StreamReader 构造函数会引发异常，因此程序应在尝试打开文件之前确认文件存在。例如，可以使用 File 类的静态 Exists 方法查看文件是否存在。

StreamReader 类提供 Read 方法，让你一次从文件中读取一个或多个字节，但通常你会想使用其 ReadLine 和 ReadToEnd 方法。

你或许能猜到，ReadLine 从文件中读取下一行并以字符串形式返回。ReadToEnd 从当前位置开始读取文件的其余部分，并以字符串形式返回。

以下代码读取文件 Memo.txt 并在 TextBox 中显示其内容：

```csharp
// Read the file.
using (StreamReader memoReader = new StreamReader("Memo.txt"))
{
    memoTextBox.Text = memoReader.ReadToEnd();
    memoReader.Close();
}
```

如果读取器位于流的末尾，StreamReader 的 EndOfStream 属性会返回 true。当读取长度未知的流时，这特别有用。例如，程序可以进入一个 while 循环，使用 ReadLine 读取各行，并在 EndOfStream 为 false 时继续。

