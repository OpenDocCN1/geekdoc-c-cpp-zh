

## 2.2 读写二进制数据

文本格式便于测试和调试，因为它具有人类可读性，但在传输数据时其效率不如二进制格式。在以下各节中，你将学习如何执行二进制数据的输入和输出。

### 2.2.1 DataInput 和 DataOutput 接口

`DataOutput` 接口定义了以下方法，用于以二进制格式写入数字、字符、布尔值或字符串：

```
writeChars       writeFloat
writeByte        writeDouble
writeInt         writeChar
writeShort       writeBoolean
writeLong        writeUTF
```

例如，`writeInt` 始终将整数写为 4 字节的二进制量，无论其位数多少；`writeDouble` 始终将双精度浮点数写为 8 字节的二进制量。生成的输出不具备人类可读性，但给定类型的每个值都会占用相同的空间，而且读回数据的速度会比解析文本更快。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_100_0.png)

> **注意：** 根据你所使用的处理器，在内存中存储整数和浮点数有两种不同的方法。例如，假设你正在处理一个 4 字节的 int，如十进制数 1234，或十六进制的 4D2（1234 = 4 × 256 + 13 × 16 + 2）。该值可以这样存储：内存中四个字节的第一个字节保存该值的最高有效字节（MSB）：`00 00 04 D2`。这就是所谓的大端法。或者，我们可以先存放最低有效字节（LSB）：`D2 04 00 00`。这自然被称为小端法。例如，SPARC 使用大端法；Pentium 使用小端法。这可能会导致问题。当文件从 C 或 C++ 文件保存时，数据会按照处理器存储它们的方式原样保存。这使得即使是最简单的数据文件也难以从一个平台迁移到另一个平台。在 Java 中，所有值都以大端方式写入，无论处理器是什么。这使得 Java 数据文件与平台无关。

`writeUTF` 方法使用 8 位 Unicode 转换格式的修改版本写入字符串数据。它不是简单地使用标准的 UTF-8 编码，而是先将 Unicode 代码单元序列表示为 UTF-16，然后使用 UTF-8 规则对结果进行编码。对于代码高于 0xFFFF 的字符，这种修改后的编码是不同的。它是为了与 Unicode 尚未超过 16 位时构建的虚拟机向后兼容而使用的。

由于没有其他人使用这种修改后的 UTF-8，因此你只应使用 `writeUTF` 方法为 Java 虚拟机编写字符串——例如，在生成字节码的程序中。对于其他用途，请使用 `writeChars` 方法。

要将数据读回，请使用 `DataInput` 接口中定义的以下方法：

```
readInt        readDouble
readShort      readChar
readLong       readBoolean
readFloat      readUTF
```

`DataInputStream` 类实现了 `DataInput` 接口。要从文件读取二进制数据，请将 `DataInputStream` 与字节源（如 `FileInputStream`）结合使用：

```java
var in = new DataInputStream(new FileInputStream("employee.dat"));
```

类似地，要写入二进制数据，请使用实现了 `DataOutput` 接口的 `DataOutputStream` 类：

```java
var out = new DataOutputStream(new FileOutputStream("employee.dat"));
```

**java.io.DataInput 1.0**

| 方法 | 描述 |
|---|---|
| boolean readBoolean() | |
| byte readByte() | |
| char readChar() | |
| double readDouble() | |
| float readFloat() | |
| int readInt() | |
| long readLong() | |
| short readShort() | 读取给定类型的值。 |
| void readFully(byte[] b) | 将字节读入数组 b，阻塞直到所有字节都被读取。 |
| void readFully(byte[] b, int off, int len) | 从 off 开始，将最多 len 个字节放入数组 b，阻塞直到所有字节都被读取。 |

**java.io.DataInput 1.0（续）**

- `String readUTF()`
  以“修改后的 UTF-8”格式读取字符串。
- `int skipBytes(int n)`
  跳过 n 个字节，阻塞直到所有字节都被跳过。

**java.io.DataOutput 1.0**

- `void writeBoolean(boolean b)`
- `void writeByte(int b)`
- `void writeChar(int c)`
- `void writeDouble(double d)`
- `void writeFloat(float f)`
- `void writeInt(int i)`
- `void writeLong(long l)`
- `void writeShort(int s)`
  写入给定类型的值。
- `void writeChars(String s)`
  写入字符串中的所有字符。
- `void writeUTF(String s)`
  以“修改后的 UTF-8”格式写入字符串。

### 2.2.2 随机访问文件

`RandomAccessFile` 类允许你在文件中的任意位置读取或写入数据。磁盘文件是随机访问的，但与网络套接字通信的输入/输出流则不是。你可以以只读或读写模式打开随机访问文件；通过在构造函数的第二个参数中使用字符串 `"r"`（用于读访问）或 `"rw"`（用于读/写访问）来指定选项。

```java
var in = new RandomAccessFile("employee.dat", "r");
var inOut = new RandomAccessFile("employee.dat", "rw");
```

当你将现有文件打开为 `RandomAccessFile` 时，该文件不会被删除。

随机访问文件有一个文件指针，用于指示下一个要读取或写入的字节的位置。可以使用 `seek` 方法将文件指针设置为文件内的任意字节位置。`seek` 的参数是一个介于 0 和文件字节长度之间的 long 整数。`getFilePointer` 方法返回文件指针的当前位置。

`RandomAccessFile` 类同时实现了 `DataInput` 和 `DataOutput` 接口。要读写随机访问文件，请使用我们在前一节中讨论的方法，如 `readInt`/`writeInt` 和 `readChar`/`writeChar`。

让我们来看一个示例程序，它将员工记录存储在随机访问文件中。每条记录的大小相同。这使得读取任意记录变得容易。假设你想将文件指针定位到第三条记录。只需将文件指针设置为适当的字节位置并开始读取。

```java
long n = 3;
in.seek((n - 1) * RECORD_SIZE);
var e = new Employee();
e.readData(in);
```

如果你想修改记录并将其保存回相同位置，请记得将文件指针设置回记录的开头：

```java
in.seek((n - 1) * RECORD_SIZE);
e.writeData(out);
```

要确定文件的总字节数，请使用 `length` 方法。记录的总数是文件长度除以每条记录的大小。

```java
long nbytes = in.length(); // 以字节为单位的长度
int nrecords = (int) (nbytes / RECORD_SIZE);
```

整数和浮点值在二进制格式中具有固定大小，但对于字符串，我们需要做更多的工作。我们提供了两个辅助方法来写入和读取固定大小的字符串。

`writeFixedString` 方法从字符串开头开始写入指定数量的代码单元。如果代码单元不足，该方法将使用零值填充字符串。

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

`readFixedString` 方法从输入流中读取字符，直到它消耗了 `size` 个代码单元或遇到零值字符。然后，它跳过输入字段中剩余的零值。为了提高效率，此方法使用 `StringBuilder` 类来读取字符串。

```java
public static String readFixedString(int size, DataInput in)
    throws IOException
{
    var b = new StringBuilder(size);
    int i = 0;
    var done = false;
    while (!done && i < size)
    {
        char ch = in.readChar();
        i++;
        if (ch == 0) done = true;
        else b.append(ch);
    }
    in.skipBytes(2 * (size - i));
    return b.toString();
}
```

我们将 `writeFixedString` 和 `readFixedString` 方法放在 `DataIO` 辅助类中。

要写入固定大小的记录，我们只需以二进制形式写入所有字段。

```java
DataIO.writeFixedString(e.getName(), Employee.NAME_SIZE, out);
out.writeDouble(e.getSalary());
LocalDate hireDay = e.getHireDay();
out.writeInt(hireDay.getYear());
out.writeInt(hireDay.getMonthValue());
out.writeInt(hireDay.getDayOfMonth());
```

读回数据同样简单。

```java
String name = DataIO.readFixedString(Employee.NAME_SIZE, in);
double salary = in.readDouble();
int y = in.readInt();
int m = in.readInt();
int d = in.readInt();
```

让我们计算每条记录的大小。我们将使用 40 个字符作为姓名串。因此，每条记录将包含 100 个字节：

- 40 个字符 = 80 个字节用于姓名
- 1 个 double = 8 个字节用于薪水
- 3 个 int = 12 个字节用于日期

清单 2.2 中所示的程序将三条记录写入一个数据文件，然后按相反顺序从文件中读取它们。要高效地做到这一点，需要随机访问——我们需要首先到达最后一条记录。

