
![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_82_0.png)

**图 2.1** 输入流和输出流层次结构

以及

```java
void flush()
```

分别。InputStream、OutputStream、Reader 和 Writer 类都实现了 Closeable 接口。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_83_0.png)

**图 2.2** Reader 和 Writer 层次结构

> **注意：** java.io.Closeable 接口扩展了 java.lang.AutoCloseable 接口。因此，可以对任何 Closeable 使用 try-with-resources 语句。为什么有两个接口？Closeable 接口的 close 方法只抛出 IOException，而 AutoCloseable.close 方法可能抛出任何异常。

OutputStream 和 Writer 实现了 Flushable 接口。

Readable 接口只有一个方法

```java
int read(CharBuffer cb)
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_84_0.png)

**图 2.3** Closeable、Flushable、Readable 和 Appendable 接口

CharBuffer 类具有用于顺序和随机读/写访问的方法。它表示内存缓冲区或内存映射文件。（详见第 132 页的 2.5.2 节“缓冲区数据结构”。）

Appendable 接口有两个方法，用于追加单个字符和字符序列：

```java
Appendable append(char c)
Appendable append(CharSequence s)
```

CharSequence 接口描述 char 值序列的基本属性。它由 String、CharBuffer、StringBuilder 和 StringBuffer 实现。

在输入/输出流类中，只有 Writer 实现了 Appendable。

| `java.io.Closeable` | 5.0 |
|---|---|
| • `void close()` | 关闭此 Closeable。此方法可能抛出 IOException。 |

| `java.io.Flushable` | 5.0 |
|---|---|
| • `void flush()` | 刷新此 Flushable。 |

| `java.lang.Readable` | 5.0 |
|---|---|
| • `int read(CharBuffer cb)` | 尝试将尽可能多的 char 值读入 cb，直至达到其可容纳的数量。返回读取的值的数量；如果此 Readable 中没有更多可用值，则返回 -1。 |

| `java.lang.Appendable` | 5.0 |
|---|---|
| • `Appendable append(char c)`<br>• `Appendable append(CharSequence cs)` | 将给定代码单元，或给定序列中的所有代码单元，追加到此 Appendable；返回此对象。 |

| `java.lang.CharSequence` | 1.4 |
|---|---|
| • `char charAt(int index)` | 返回给定索引处的代码单元。 |
| • `int length()` | 返回此序列中的代码单元数量。 |
| • `CharSequence subSequence(int startIndex, int endIndex)` | 返回一个 CharSequence，由从索引 startIndex 到 endIndex - 1 存储的代码单元组成。 |
| • `String toString()` | 返回一个由此序列的代码单元组成的字符串。 |

## 2.1.3 组合输入/输出流过滤器

FileInputStream 和 FileOutputStream 为你提供附加到磁盘文件的输入流和输出流。需要将文件的文件名或完整路径名传递给构造函数。例如，

```java
var fin = new FileInputStream("employee.dat");
```

会在用户目录中查找名为 employee.dat 的文件。

> **提示：** java.io 中的所有类都将相对路径名解释为从用户的工作目录开始。可以通过调用 System.getProperty("user.dir") 获取此目录。

> **警告：** 由于反斜杠字符是 Java 字符串中的转义字符，请务必对 Windows 风格的路径名使用 `\\`（例如 `C:\\Windows\\win.ini`）。在 Windows 中，也可以使用单个正斜杠（`C:/Windows/win.ini`），因为大多数 Windows 文件处理系统调用会将正斜杠解释为文件分隔符。但是，不建议这样做——Windows 系统函数的行为可能会发生变化。对于可移植程序，应使用程序运行所在平台的文件分隔符字符。它可作为常量字符串 `java.io.File.separator` 使用。

与抽象 InputStream 和 OutputStream 类一样，这些类只支持在字节级别进行读写。也就是说，我们只能从对象 fin 中读取字节和字节数组。

```java
byte b = (byte) fin.read();
```

正如你将在下一节看到的，如果我们只有 DataInputStream，就可以读取数值类型：

```java
DataInputStream din = ...;
double x = din.readDouble();
```

但是，正如 FileInputStream 没有读取数值类型的方法一样，DataInputStream 也没有从文件获取数据的方法。

Java 使用一种巧妙的机制来分离两类职责。某些输入流（例如 FileInputStream 以及 URL 类的 openStream 方法返回的输入流）可以从文件和其他更奇特的位置获取字节。其他输入流（例如 DataInputStream）可以将字节组装成更有用的数据类型。Java 程序员必须将两者组合起来。例如，为了能够从文件读取数字，首先创建一个 FileInputStream，然后将其传递给 DataInputStream 的构造函数。

```java
var fin = new FileInputStream("employee.dat");
var din = new DataInputStream(fin);
double x = din.readDouble();
```

如果再次查看图 2.1，可以看到 FilterInputStream 和 FilterOutputStream 类。这些类的子类用于为处理字节的输入/输出流添加功能。

可以通过嵌套过滤器来添加多种功能。例如，默认情况下，输入流不带缓冲。也就是说，每次调用 read 都会要求操作系统再分配一个字节。更高效的做法是改为请求数据块并将其存储在缓冲区中。如果希望为文件同时提供缓冲*和*数据输入方法，请使用下面这个相当复杂的构造函数序列：

```java
var din = new DataInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
```

请注意，我们将 DataInputStream 放在构造函数链的*最后*，因为我们要使用 DataInputStream 的方法，并且希望*这些方法*使用带缓冲的读取方法。

有时在将中间输入流链接在一起时，需要跟踪它们。例如，读取输入时，通常需要查看下一个字节，以判断它是否是你期望的值。Java 为此提供了 PushbackInputStream。

```java
var pbin = new PushbackInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
```

现在可以试探性地读取下一个字节

```java
int b = pbin.read();
```

如果不是想要的值，就将其推回。

```java
if (b != '<') pbin.unread(b);
```

但是，读取和推回是适用于回推输入流的*唯一*方法。如果希望向前查看并同时读取数字，则需要同时拥有回推输入流和数据输入流引用。

```java
var pbin = new PushbackInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
var din = new DataInputStream(pbin);
```

当然，在其他编程语言的输入/输出库中，缓冲和前瞻等便利功能会自动处理——因此在 Java 中不得不组合流过滤器会有些麻烦。然而，混合和匹配过滤器类以构造有用的序列的能力

### java.io.FileOutputStream 1.0

- `FileOutputStream(String name)`
- `FileOutputStream(String name, boolean append)`
- `FileOutputStream(File file)`
- `FileOutputStream(File file, boolean append)`

创建一个由名称字符串或文件对象指定的新文件输出流。（`File` 类将在本章末尾描述。）如果 `append` 参数为 true，则不会删除具有相同名称的现有文件，并且数据将添加到文件末尾。否则，此方法会删除任何具有相同名称的现有文件。

### java.io.BufferedInputStream 1.0

- `BufferedInputStream(InputStream in)`

创建一个缓冲输入流。缓冲输入流从流中读取字节，而不会每次都引起设备访问。当缓冲区为空时，会将新的数据块读入缓冲区。

### java.io.BufferedOutputStream 1.0

- `BufferedOutputStream(OutputStream out)`

创建一个缓冲输出流。缓冲输出流收集要写入的字节，而不会每次都引起设备访问。当缓冲区填满或流被刷新时，数据会被写出。

### java.io.PushbackInputStream 1.0

- `PushbackInputStream(InputStream in)`
- `PushbackInputStream(InputStream in, int size)`

构造一个具有一字节前瞻或指定大小的回推缓冲区的输入流。

- `void unread(int b)`

推回一个字节，该字节将在下一次调用 `read` 时再次被取回。
