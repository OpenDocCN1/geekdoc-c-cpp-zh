
StandardCharsets 类包含类型为 Charset 的静态变量，用于表示每个 Java 虚拟机都必须支持的字符编码：

- `StandardCharsets.UTF_8`
- `StandardCharsets.UTF_16`
- `StandardCharsets.UTF_16BE`
- `StandardCharsets.UTF_16LE`
- `StandardCharsets.ISO_8859_1`
- `StandardCharsets.US_ASCII`

要获取另一种编码的 Charset，请使用静态 forName 方法：

```java
Charset shiftJIS = Charset.forName("Shift-JIS");
```

在读取或写入文本时使用 Charset 对象。例如，可以按如下方式将字节数组转换为字符串：

```java
String str = new String(bytes, StandardCharsets.UTF_8);
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_89_0.png)

> **提示：** 有些方法允许使用 Charset 对象或字符串指定字符编码。请选择 StandardCharsets 常量，这样就不必担心拼写是否正确。例如，`new String(bytes, "UTF 8")` 是不可接受的，会导致运行时错误。

![](img/7dd923a566750151a3aab0dacd0cdaa5_89_1.png)

> **注意：** 有些方法（例如 String(byte[]) 构造函数）在未指定编码时使用默认平台编码；其他方法（例如 Files.readAllLines）使用 UTF-8。

## 2.3 读写二进制数据

文本格式便于测试和调试，因为它是人类可读的，但它在传输数据时不如二进制格式高效。在以下各节中，你将学习如何对二进制数据执行输入和输出。

### 2.3.1 DataInput 和 DataOutput 接口

DataOutput 接口定义了以下方法，用于以二进制格式写入数字、字符、布尔值或字符串：

- `writeChars`
- `writeByte`
- `writeInt`
- `writeShort`
- `writeLong`
- `writeFloat`
- `writeDouble`
- `writeChar`
- `writeBoolean`
- `writeUTF`

例如，`writeInt` 始终将整数写为 4 字节的二进制量，无论数字有多少位；`writeDouble` 始终将 double 写为 8 字节的二进制量。生成的输出不是人类可读的，但给定类型的每个值所需空间相同，并且将其读回比解析文本更快。

> **注意：** 在内存中存储整数和浮点数有两种不同的方法，具体取决于你使用的处理器。例如，假设你正在处理一个 4 字节的 `int`，比如十进制数 1234，或十六进制数 4D2（1234 = 4 × 256 + 13 × 16 + 2）。这个值可以这样存储：内存中四个字节的第一个字节保存该值的最高有效字节（MSB）：`00 00 04 D2`。这就是所谓的大端序方法。或者，我们也可以从最低有效字节（LSB）开始：`D2 04 00 00`。这顺理成章地称为小端序方法。例如，SPARC 使用大端序；Pentium 使用小端序。这可能导致问题。当从 C 或 C++ 文件保存文件时，数据完全按照处理器存储它们的方式保存。这使得即使是最简单的数据文件也很难从一个平台迁移到另一个平台。在 Java 中，无论使用哪种处理器，所有值都以大端序方式写入。这使得 Java 数据文件与平台无关。

`writeUTF` 方法使用 8 位 Unicode 转换格式的修改版本来写入字符串数据。它并不直接使用标准 UTF-8 编码，而是先用 UTF-16 表示 Unicode 代码单元序列，然后使用 UTF-8 规则对结果进行编码。对于编码值高于 `0xFFFF` 的字符，这种修改后的编码有所不同。它用于与在 Unicode 尚未超出 16 位时构建的虚拟机保持向后兼容。

由于其他任何地方都不使用这种 UTF-8 修改版，因此只应使用 `writeUTF` 方法写入供 Java 虚拟机使用的字符串——例如，在生成字节码的程序中。其他用途请使用 `writeChars` 方法。

要将数据读回，请使用 `DataInput` 接口中定义的以下方法：

- `readInt`
- `readShort`
- `readLong`
- `readFloat`
- `readDouble`
- `readChar`
- `readBoolean`
- `readUTF`

DataInputStream 类实现 DataInput 接口。要从文件读取二进制数据，请将 DataInputStream 与字节源（例如 FileInputStream）组合使用：

```java
DataInputStream in = new DataInputStream(new FileInputStream("employee.dat"));
```

类似地，要写入二进制数据，请使用实现 DataOutput 接口的 DataOutputStream 类：

```java
DataOutputStream out = new DataOutputStream(new FileOutputStream("employee.dat"));
```

**java.io.DataInput** 1.0

- `boolean readBoolean()`
- `byte readByte()`
- `char readChar()`
- `double readDouble()`
- `float readFloat()`
- `int readInt()`
- `long readLong()`
- `short readShort()`

  读取给定类型的值。

- `void readFully(byte[] b)`

  将字节读入数组 b，并阻塞直到读取所有字节。

  *参数：* `b` —— 读入数据的缓冲区

- `void readFully(byte[] b, int off, int len)`

  将字节读入数组 b，并阻塞直到读取所有字节。

  *参数：*
  - `b` —— 读入数据的缓冲区
  - `off` —— 数据的起始偏移量
  - `len` —— 要读取的最大字节数

- `String readUTF()`

  读取采用“修改后的 UTF-8”格式的字符串。

- `int skipBytes(int n)`

  跳过 n 个字节，并阻塞直到跳过所有字节。

  *参数：* `n` —— 要跳过的字节数

| `java.io.DataOutput` 1.0 |
|---|
| • `void writeBoolean(boolean b)`<br>• `void writeByte(int b)`<br>• `void writeChar(int c)`<br>• `void writeDouble(double d)`<br>• `void writeFloat(float f)`<br>• `void writeInt(int i)`<br>• `void writeLong(long l)`<br>• `void writeShort(int s)`<br>&nbsp;&nbsp;&nbsp;写入给定类型的值。<br><br>• `void writeChars(String s)`<br>&nbsp;&nbsp;&nbsp;写入字符串中的所有字符。<br><br>• `void writeUTF(String s)`<br>&nbsp;&nbsp;&nbsp;写入采用“修改后的 UTF-8”格式的字符串。 |

### 2.3.2 随机访问文件

`RandomAccessFile` 类允许在文件中的任意位置读取或写入数据。磁盘文件是随机访问的，但与网络套接字通信的输入/输出流不是。你可以以只读方式或读写方式打开随机访问文件；在构造函数中，将字符串 "r"（表示读访问）或 "rw"（表示读/写访问）作为第二个参数来指定该选项。

```java
RandomAccessFile in = new RandomAccessFile("employee.dat", "r");
RandomAccessFile inout = new RandomAccessFile("employee.dat", "rw");
```

当以 `RandomAccessFile` 打开现有文件时，该文件不会被删除。

随机访问文件有一个*文件指针*，指示下一个要读取或写入的字节的位置。可以使用 `seek` 方法将文件指针设置到文件内的任意字节位置。seek 的参数是一个长整数，介于零和文件长度（以字节为单位）之间。

`getFilePointer` 方法返回文件指针的当前位置。

`RandomAccessFile` 类同时实现 `DataInput` 和 `DataOutput` 接口。要从随机访问文件读写数据，请使用我们在上一节讨论的方法，例如 `readInt`/`writeInt` 和 `readChar`/`writeChar`。

让我们通过一个示例程序来了解如何将员工记录存储在随机访问文件中。每条记录的大小都相同。这使得读取任意记录变得容易。假设你想将文件指针定位到第三条记录。只需将文件指针设置到相应的字节位置并开始读取即可。

```java
long n = 3;
in.seek((n - 1) * RECORD_SIZE);
Employee e = new Employee();
e.readData(in);
```

如果你想修改该记录并将其保存回同一位置，请记得将文件指针重新设置到该记录的开头：

```java
in.seek((n - 1) * RECORD_SIZE);
e.writeData(out);
```

要确定文件中的总字节数，请使用 length 方法。记录总数等于文件长度除以每条记录的大小。

```java
long nbytes = in.length(); // length in bytes
int nrecords = (int) (nbytes / RECORD_SIZE);
```

整数和浮点数在二进制格式中具有固定大小，但对于字符串，我们需要做更多工作。我们提供了两个辅助方法来写入和读取固定大小的字符串。

writeFixedString 从字符串开头开始，写入指定数量的代码单元。如果代码单元不足，该方法会使用零值填充字符串。

```java
public static void writeFixedString(String s, int size, DataOutput out)
      throws IOException
{
   for (int i = 0; i < size; i++)
   {
      char ch = 0;
      if (i < s.length()) ch = s.charAt(i);
      out.writeChar(ch);
   }
}
```

readFixedString 方法从输入流中读取字符，直到已消耗 size 个代码单元，或遇到值为零的字符。然后，它跳过输入字段中剩余的零值。为了提高效率，该方法使用 StringBuilder 类读入字符串。

```java
public static String readFixedString(int size, DataInput in)
      throws IOException
{
   StringBuilder b = new StringBuilder(size);
   int i = 0;
   boolean more = true;
```
