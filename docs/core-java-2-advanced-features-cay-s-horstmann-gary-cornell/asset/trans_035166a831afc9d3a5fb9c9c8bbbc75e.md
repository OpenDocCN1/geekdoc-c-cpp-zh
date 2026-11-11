

`read` 和 `write` 方法都会*阻塞*，直到字节真正被读取或写入。这意味着如果输入流无法立即访问（通常是因为网络连接繁忙），当前线程将阻塞。这给了其他线程机会，在方法等待输入流再次可用时做一些有用的工作。

`available` 方法允许你检查当前可读取的字节数。这意味着像下面这样的代码片段不太可能阻塞：

```java
int bytesAvailable = in.available();
if (bytesAvailable > 0)
{
    byte[] data = new byte[bytesAvailable];
    in.read(data);
}
```

当你完成对输入/输出流的读取或写入后，通过调用 `close` 方法关闭它。这个调用释放了供应有限的操作系统资源。如果应用程序打开了太多输入/输出流而不关闭它们，系统资源可能会耗尽。关闭输出流也会*刷新*用于输出流的缓冲区：任何临时存放在缓冲区中以便作为更大数据包发送的字节都会被送出。特别是，如果你不关闭文件，最后一个字节包可能永远不会被发送。你也可以使用 `flush` 方法手动刷新输出。

即使输入/输出流类提供了处理原始 `read` 和 `write` 函数的具体方法，应用程序员也很少使用它们。你感兴趣的数据可能包含数字、字符串和对象，而不是原始字节。

与其处理字节，你可以使用从基本的 `InputStream` 和 `OutputStream` 类派生的众多输入/输出流类之一。

- **java.io.InputStream** 1.0
  - `abstract int read()` 读取一个字节的数据并返回读取的字节；在输入流末尾返回 -1。
  - `int read(byte[] b)` 读取到一个字节数组中，并返回实际读取的字节数，或在输入流末尾返回 -1；此方法最多读取 `b.length` 个字节。

（续）

- **java.io.OutputStream 1.0（续）**
  - `void write(byte[] b)`
  - `void write(byte[] b, int off, int len)`
    写入数组 `b` 中的所有字节或一部分字节。
    - 参数：
      - `b`：要写入数据的数组
      - `off`：`b` 中相对于第一个要写入字节的偏移量
      - `len`：要写入的字节数
  - `void close()` 刷新并关闭输出流。
  - `void flush()` 刷新输出流——也就是说，将任何缓冲的数据发送到其目的地。

### 2.1.2 完整的流动物园

与仅使用单一类型 `FILE` 就能很好运行的 C 语言不同，Java 拥有一个包含超过 60 种（！）不同输入/输出流类型的完整动物园（见图 2.1 和图 2.2）。

让我们根据使用方式来划分输入/输出流动物园中的“动物”。处理字节和字符的类有各自独立的层次结构。如你所见，`InputStream` 和 `OutputStream` 类允许你读写单个字节和字节数组。这些类构成了图 2.1 所示层次结构的基础。要读写字符串和数字，你需要更强大的子类。例如，`DataInputStream` 和 `DataOutputStream` 允许你以二进制格式读写所有 Java 原始类型。最后，还有一些输入/输出流能执行有用的操作；例如，`ZipInputStream` 和 `ZipOutputStream` 允许你以熟悉的 ZIP 压缩格式读写文件。

另一方面，对于 Unicode 文本，你可以使用抽象类 `Reader` 和 `Writer` 的子类（见图 2.2）。`Reader` 和 `Writer` 类的基本方法与 `InputStream` 和 `OutputStream` 的类似。

```java
abstract int read()
abstract void write(int c)
```

`read` 方法返回一个 UTF-16 代码单元（作为 0 到 65535 之间的整数），或者当到达文件末尾时返回 -1。`write` 方法以一个 Unicode 代码单元作为参数调用。（关于 Unicode 代码单元的讨论，请参阅卷 I 第 3 章。）

![](img/7dd923a566750151a3aab0dacd0cdaa5_72_0.png)

图 2.1 输入和输出流层次结构

还有四个额外的接口：`Closeable`、`Flushable`、`Readable` 和 `Appendable`（见图 2.3）。前两个接口非常简单，具有方法

```java
void close() throws IOException
```

和

```java
void flush()
```

分别。类 `InputStream`、`OutputStream`、`Reader` 和 `Writer` 都实现了 `Closeable` 接口。

![](img/7dd923a566750151a3aab0dacd0cdaa5_73_0.png)

**图 2.2** Reader 和 Writer 层次结构

> **注意：** `java.io.Closeable` 接口扩展了 `java.lang.AutoCloseable` 接口。因此，你可以对任何 `Closeable` 使用 try-with-resources 语句。为什么要有两个接口？`Closeable` 接口的 `close` 方法只抛出 `IOException`，而 `AutoCloseable.close` 方法可以抛出任何异常。

`OutputStream` 和 `Writer` 实现了 `Flushable` 接口。

`Readable` 接口只有一个方法

```java
int read(CharBuffer cb)
```

`CharBuffer` 类具有用于顺序和随机读/写访问的方法。它表示一个内存缓冲区或内存映射文件。（有关详细信息，请参阅第 124 页的 2.6.2 节“缓冲区数据结构”。）

![](img/7dd923a566750151a3aab0dacd0cdaa5_74_0.png)

**图 2.3** Closeable、Flushable、Readable 和 Appendable 接口

`Appendable` 接口有两个用于追加单个字符和字符序列的方法：

```java
Appendable append(char c)
Appendable append(CharSequence s)
```

`CharSequence` 接口描述了 char 值序列的基本属性。`String`、`CharBuffer`、`StringBuilder` 和 `StringBuffer` 实现了它。

在输入/输出流类中，只有 `Writer` 实现了 `Appendable`。

| java.io.Closeable 5.0 |
|---|
| • `void close()`<br>关闭此 Closeable。此方法可能抛出 IOException。 |

| java.io.Flushable 5.0 |
| --- |
| • `void flush()`<br>刷新此 Flushable。 |

| java.lang.Readable 5.0 |
| --- |
| • `int read(CharBuffer cb)`<br>尝试将尽可能多的 char 值读入 cb。返回读取的值数量，如果此 Readable 没有更多值可用，则返回 -1。 |

| java.lang.Appendable 5.0 |
| --- |
| • `Appendable append(char c)`<br>• `Appendable append(CharSequence cs)`<br>将给定的代码单元或给定序列中的所有代码单元追加到此 Appendable；返回 this。 |

| java.lang.CharSequence 1.4 |
| --- |
| • `char charAt(int index)`<br>返回给定索引处的代码单元。<br>• `int length()`<br>返回此序列中代码单元的数量。<br>• `CharSequence subSequence(int startIndex, int endIndex)`<br>返回一个 CharSequence，由从索引 startIndex 到 endIndex - 1 存储的代码单元组成。<br>• `String toString()`<br>返回一个由该序列的代码单元组成的字符串。 |

### 2.1.3 组合输入/输出流过滤器

`FileInputStream` 和 `FileOutputStream` 提供连接到磁盘文件的输入和输出流。你需要将文件名或文件的完整路径名传递给构造函数。例如，

```java
FileInputStream fin = new FileInputStream("employee.dat");
```

会在用户目录中查找名为 employee.dat 的文件。

> **提示：** `java.io` 中的所有类都将相对路径名解释为从用户的工作目录开始。你可以通过调用 `System.getProperty("user.dir")` 获取此目录。

> **警告：** 由于反斜杠字符是 Java 字符串中的转义字符，请务必对 Windows 风格的路径名使用 \\（例如，C:\\Windows\\win.ini）。在 Windows 中，你也可以使用单个正斜杠（C:/Windows/win.ini），因为大多数 Windows 文件处理系统调用会将正斜杠解释为文件分隔符。但是，不建议这样做——Windows 系统函数的行为可能会发生变化。对于可移植的程序，请使用程序运行所在平台的文件分隔符。它可作为常量字符串 `java.io.File.separator` 使用。

与抽象类 `InputStream` 和 `OutputStream` 类似，这些类仅支持字节级别的读取和写入。也就是说，我们只能从对象 `fin` 中读取字节和字节数组。

```java
byte b = (byte) fin.read();
```

正如你将在下一节中看到的，如果我们有一个 `DataInputStream`，我们就可以读取数值类型：

```java
DataInputStream din = . . . ;
double x = din.readDouble();
```

但是，正如 `FileInputStream` 没有读取数值类型的方法一样，`DataInputStream` 也没有从文件获取数据的方法。

Java 使用一种巧妙的机制来分离两类职责。一些输入流（如 `FileInputStream` 以及 URL 类的 `openStream` 方法返回的输入流）可以从文件和其他更特殊的位置检索字节。其他输入流（如 `DataInputStream`）可以将字节组装成更有用的数据类型。Java 程序员必须将两者结合起来。例如，为了能够从文件读取数字，首先创建一个 `FileInputStream`，然后将其传递给 `DataInputStream` 的构造函数。

```java
FileInputStream fin = new FileInputStream("employee.dat");
DataInputStream din = new DataInputStream(fin);
double x = din.readDouble();
```

