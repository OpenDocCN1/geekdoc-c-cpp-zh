
```
int i;
FileStream fin;

if(args.Length != 1) {
    Console.WriteLine("Usage: ShowFile File");
    return;
}

try {
    fin = new FileStream(args[0], FileMode.Open);
} catch (IOException exc) {
    Console.WriteLine("Cannot Open File");
    Console.WriteLine(exc.Message);
    return;
}

// Read bytes until EOF is encountered.
do {
    try {
        i = fin.ReadByte();
    } catch (IOException exc) {
        Console.WriteLine("Error Reading File");
        Console.WriteLine(exc.Message);
        break;
    }
    if(i != -1) Console.Write((char) i);
} while(i != -1);

fin.Close();
}
```

## 写入文件

要将一个字节写入文件，请使用 `WriteByte()` 方法。其最简单的形式如下所示：

```
void WriteByte(byte val)
```

此方法将由 val 指定的字节写入文件。如果基础流未以输出方式打开，则抛出 NotSupportedException。如果流已关闭，则抛出 ObjectDisposedException。

```
void Write(byte[] buf, int offset, int numBytes)
```

你可以通过调用 `Write()` 将字节数组写入文件。其形式如下所示：

Write() 从数组 buf 的 buf[offset] 开始，将 numBytes 个字节写入文件。返回写入的字节数。如果在写入期间发生错误，则抛出 IOException。如果基础流未以输出方式打开，则抛出 NotSupportedException。还可能发生其他几种异常。

你可能知道，执行文件输出时，输出通常不会立即写入实际的物理设备。相反，输出会由操作系统缓冲，直到可以一次性写入相当大的数据块。这提高了系统的效率。例如，磁盘文件按扇区组织，扇区长度可能从 128 字节起不等。输出通常会被缓冲，直到可以一次性写入整个扇区。

但是，如果你希望无论缓冲区是否已满都将数据写入物理设备，可以调用 `Flush()`，如下所示：

```
void Flush()
```

失败时会抛出 IOException。如果流已关闭，则抛出 ObjectDisposedException。

处理完输出文件后，必须记得使用 `Close()` 将其关闭。这样做可以确保磁盘缓冲区中剩余的任何输出都实际写入磁盘。因此，在关闭文件之前没有理由调用 `Flush()`。

下面是一个写入文件的简单示例：

```
// Write to a file.
using System;
using System.IO;

class WriteToFile {
    static void Main(string[] args) {
        FileStream fout;

        // Open output file.
        try {
            fout = new FileStream("test.txt", FileMode.Create);
        } catch (IOException exc) {
            Console.WriteLine("Cannot Open File");
            Console.WriteLine(exc.Message);
            return;
        }

        // Write the alphabet to the file.
        try {
            for(char c = 'A'; c <= 'Z'; c++)
                fout.WriteByte((byte) c);
        } catch (IOException exc) {
            Console.WriteLine("Error Writing File");
            Console.WriteLine(exc.Message);
        }

        fout.Close();
    }
}
```

该程序首先打开一个名为 test.txt 的文件用于输出。然后它将大写字母表写入该文件。最后，它关闭文件。请注意 try/catch 块如何处理可能发生的 I/O 错误。此程序执行后，test.txt 将包含以下输出：

ABCDEFGHIJKLMNOPQRSTUVWXYZ

## 使用 FileStream 复制文件

FileStream 使用的面向字节的 I/O 的一个优点是，你可以将它用于任何类型的文件——而不仅仅是包含文本的文件。例如，以下程序可以复制任何类型的文件，包括可执行文件。源文件和目标文件的名称在命令行中指定。

```
fout.Close();
}
```

## 基于字符的文件 I/O

尽管面向字节的文件处理非常常见，但为此使用基于字符的流也是可行的。字符流的优点是它们直接操作 Unicode 字符。因此，如果你想存储 Unicode 文本，字符流无疑是最佳选择。一般来说，要执行基于字符的文件操作，你会将 FileStream 包装在 StreamReader 或 StreamWriter 中。这些类会自动将字节流转换为字符流，反之亦然。

请记住，在操作系统层面，文件由一组字节组成。使用 StreamReader 或 StreamWriter 并不会改变这一事实。

StreamWriter 派生自 TextWriter。StreamReader 派生自 TextReader。因此，StreamWriter 和 StreamReader 可以访问其基类定义的方法和属性。

## 使用 StreamWriter

要创建基于字符的输出流，请将 Stream 对象（例如 FileStream）包装在 StreamWriter 中。StreamWriter 定义了几个构造函数。其最常用的构造函数之一如下所示：

```
StreamWriter(Stream stream)
```

这里的 stream 是已打开流的名称。如果 stream 未以输出方式打开，此构造函数会抛出 ArgumentException；如果 stream 为 null，则抛出 ArgumentNullException。创建后，StreamWriter 会自动处理字符到字节的转换。

下面是一个简单的键盘到磁盘实用程序，它读取在键盘上输入的文本行，并将它们写入名为 "test.txt" 的文件。文本会被读取，直到用户输入单词 "stop"。它使用包装在 StreamWriter 中的 FileStream 输出到文件。

```csharp
// A simple key-to-disk utility that demonstrates a StreamWriter.
using System;
using System.IO;

class KtoD {
    static void Main() {
        string str;
        FileStream fout;

        try {
            fout = new FileStream("test.txt", FileMode.Create);
        }
        catch (IOException exc) {
            Console.WriteLine("Cannot Open File");
            Console.WriteLine(exc.Message);
            return;
        }
        StreamWriter fstr_out = new StreamWriter(fout);
        Console.WriteLine("Enter text ('stop' to quit).");
        do {
            Console.Write(": ");
            str = Console.ReadLine();

            if(str != "stop") {
                str = str + "\r\n"; // add newline
                try {
                    fstr_out.Write(str);
                } catch (IOException exc) {
                    Console.WriteLine("Error Writing File");
                    Console.WriteLine(exc.Message);
                    break;
                }
            }
        } while(str != "stop");
    }
    fstr_out.Close();
}
```

在某些情况下，直接使用 **StreamWriter** 打开文件可能更方便。

为此，请使用以下构造函数之一：

- `StreamWriter(string filename)`
- `StreamWriter(string filename, bool appendFlag)`

这里的 *filename* 指定要打开的文件名，可以包含完整路径说明。
在第二种形式中，如果 *appendFlag* 为 true，则输出会追加到现有文件的末尾。否则，输出会覆盖指定的文件。在两种情况下，如果文件不存在，则会创建该文件。此外，如果发生 I/O 错误，两者都会抛出 **IOException**。还可能发生其他异常。

下面是重写后的键盘到磁盘程序，它使用 **StreamWriter** 打开输出文件：

```csharp
// Open a file using StreamWriter.

using System;
using System.IO;

class KtoD {
    static void Main() {
        string str;
        StreamWriter fstr_out;

        try {
            fstr_out = new StreamWriter("test.txt");
        }
        catch (IOException exc) {
            Console.WriteLine("Cannot Open File");
            Console.WriteLine(exc.Message);
            return ;
        }

        Console.WriteLine("Enter text ('stop' to quit).");
        do {
            Console.Write(": ");
            str = Console.ReadLine();
            if(str != "stop") {
                str = str + "\r\n"; // add newline
                try {
                    fstr_out.Write(str);
                } catch(IOException exc) {
                    Console.WriteLine("Error Writing File");
                    Console.WriteLine(exc.Message);
                    break;
                }
            } while(str != "stop");
            fstr_out.Close();
        }
```

## 使用 StreamReader

要创建基于字符的输入流，请将字节流包装在 StreamReader 中。

StreamReader 定义了几个构造函数。一个常用的构造函数如下所示：

StreamReader(Stream stream)

这里的 stream 是已打开流的名称。如果 stream 为 null，此构造函数会抛出 ArgumentNullException。如果 stream 未以输入方式打开，则抛出 ArgumentException。创建后，StreamReader 会自动处理字节到字符的转换。

以下程序创建了一个简单的磁盘到屏幕实用程序，它读取名为 "test.txt" 的文本文件，并在屏幕上显示其内容。因此，它是上一节中所示的键盘到磁盘实用程序的补充：

```csharp
// A simple disk-to-screen utility that demonstrates a StreamReader.
using System;
using System.IO;

class DtoS {
    static void Main() {
        FileStream fin;
        string s;

        try {
            fin = new FileStream("test.txt", FileMode.Open);
        }
        catch(IOException exc) {
            Console.WriteLine("Error Opening File");
            Console.WriteLine(exc.Message);
            return;
        }

        StreamReader fstr_in = new StreamReader(fin);
```
