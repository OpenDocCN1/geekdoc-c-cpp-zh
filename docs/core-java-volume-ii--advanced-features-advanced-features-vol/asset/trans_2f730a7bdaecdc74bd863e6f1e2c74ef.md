
## 2.1.4 文本输入与输出

保存数据时，你可以在二进制格式和文本格式之间选择。例如，如果整数 1234 以二进制保存，它会写成字节序列 `00 00 04 D2`（十六进制表示法）。在文本格式中，它保存为字符串 "1234"。尽管二进制 I/O 快速高效，但人类不易阅读。我们首先讨论文本 I/O，并在第 78 页的 2.2 节“读写二进制数据”中介绍二进制 I/O。

保存文本字符串时，你需要考虑*字符编码*。在 Java 内部使用的 UTF-16 编码中，字符串 "José" 被编码为 `00 4A 00 6F 00 73 00 E9`（十六进制）。然而，许多程序期望文本文件使用不同的编码。在互联网上最常用的 UTF-8 编码中，该字符串会写成 `4A 6F 73 C3 A9`，前三个字母没有零字节，而 é 字符占两个字节。

`OutputStreamWriter` 类使用选定的字符编码，将 Unicode 码元输出流转换为字节流。相反，`InputStreamReader` 类将包含字节（按某种字符编码表示字符）的输入流转换为发出 Unicode 码元的读取器。

例如，下面展示了如何创建一个从控制台读取按键并将其转换为 Unicode 的输入读取器：

```
var in = new InputStreamReader(System.in);
```

这个输入流读取器假定使用宿主系统的默认字符编码。在桌面操作系统上，这可能是 Windows 1252 或 MacRoman 之类的陈旧编码。你应该始终在 InputStreamReader 的构造函数中选择特定编码，例如：

```
var in = new InputStreamReader(new FileInputStream("data.txt"), StandardCharsets.UTF_8);
```

有关字符编码的更多信息，请参见第 75 页的 2.1.8 节“字符编码”。

Reader 和 Writer 类只有读写单个字符的基本方法。与流一样，你使用子类来处理字符串和数字。

## 2.1.5 如何写出文本输出

对于文本输出，请使用 PrintWriter。该类具有以文本格式打印字符串和数字的方法。为了打印到文件，请用文件名和字符编码构造 PrintWriter：

```
var out = new PrintWriter("employee.txt", StandardCharsets.UTF_8);
```

要写入打印写入器，请使用与 System.out 相同的 print、println 和 printf 方法。你可以使用这些方法打印数字（int、short、long、float、double）、字符、布尔值、字符串和对象。

例如，考虑以下代码：

```
    String name = "Harry Hacker";
    double salary = 75000;
    out.print(name);
    out.print(' ');
    out.println(salary);
```

这会写出字符

```
    Harry Hacker 75000.0
```

到写入器 out。然后这些字符被转换为字节，并最终进入文件 employee.txt。

println 方法会为目标系统（Windows 上为 "\r\n"，UNIX 上为 "\n"）向该行添加正确的行尾字符。该字符串通过调用 System.getProperty("line.separator") 获得。

如果写入器设置为自动刷新模式，则每当调用 println 时，缓冲区中的所有字符都会发送到其目的地。（打印写入器始终是缓冲的。）默认情况下，未启用自动刷新。你可以使用 PrintWriter(Writer writer, boolean autoFlush) 构造函数启用或禁用自动刷新：

```
    var out = new PrintWriter(
        new OutputStreamWriter(
            new FileOutputStream("employee.txt"), StandardCharsets.UTF_8),
        true); // autoflush
```

print 方法不会抛出异常。你可以调用 checkError 方法查看输出流是否出了问题。

> **注意：** Java 老手可能会想，PrintStream 类和 System.out 到底发生了什么。在 Java 1.0 中，PrintStream 类只是通过丢弃最高字节将所有 Unicode 字符截断为 ASCII 字符。（当时，Unicode 仍是 16 位编码。）显然，这不是一种干净或可移植的方法，Java 1.1 引入读取器和写入器后修复了这个问题。为了与现有代码兼容，System.in、System.out 和 System.err 仍然是输入/输出流，而不是读取器和写入器。但现在 PrintStream 类会像 PrintWriter 那样在内部将 Unicode 字符转换为宿主默认编码。使用 print 和 println 方法时，PrintStream 类型的对象的行为与打印写入器完全相同，但与打印写入器不同的是，它们允许你用 write(int) 和 write(byte[]) 方法输出原始字节。

| `java.io.PrintWriter` | 1.1 |
|---|---|
| • `PrintWriter(OutputStream out)`<br>• `PrintWriter(Writer writer)` | 创建一个写入给定输出流或写入器的新 PrintWriter。 |
| • `PrintWriter(String filename, String encoding)`<br>• `PrintWriter(File file, String encoding)` | 创建一个使用给定字符编码写入给定文件的新 PrintWriter。 |
| • `void print(Object obj)` | 通过打印由 `toString` 产生的字符串来打印对象。 |
| • `void print(String s)` | 打印包含 Unicode 码元的字符串。 |
| • `void println(String s)` | 打印字符串后跟行终止符。如果处于自动刷新模式，则刷新输出流。 |
| • `void print(char[] s)` | 打印给定数组中的所有 Unicode 码元。 |
| • `void print(char c)` | 打印一个 Unicode 码元。 |
| • `void print(int i)`<br>• `void print(long l)`<br>• `void print(float f)`<br>• `void print(double d)`<br>• `void print(boolean b)` | 以文本格式打印给定值。 |
| • `void printf(String format, Object... args)` | 按格式字符串的指定打印给定值。有关格式字符串的规范，请参见第一卷第三章。 |
| • `boolean checkError()` | 如果发生格式化或输出错误，则返回 true。一旦输出流遇到错误，它就会受到污染，并且所有对 `checkError` 的调用都会返回 true。 |

## 2.1.6 如何读取文本输入

处理任意文本的最简单方法是使用我们在第一卷中大量使用的 Scanner 类。你可以从任何输入流构造 Scanner。

如今，`BufferedReader` 类还有一个 `lines` 方法，可生成一个 `Stream<String>`。然而，与 `Scanner` 不同，`BufferedReader` 没有读取数字的方法。

## 2.1.7 以文本格式保存对象

在本节中，我们将带你完成一个示例程序，该程序将 Employee 记录数组存储到文本文件中。每条记录存储在单独的一行中。实例字段之间用分隔符分隔。我们使用竖线（`|`）作为分隔符。冒号（`:`）是另一种常见选择。有趣的是，每个人都使用不同的分隔符。当然，我们回避了这样一个问题：如果我们要保存的某个字符串中实际出现了 `|`，可能会发生什么。

下面是一组示例记录：

```
Harry Hacker|35500|1989-10-01
Carl Cracker|75000|1987-12-15
Tony Tester|38000|1990-03-15
```

写入记录很简单。由于我们写入文本文件，因此使用 `PrintWriter` 类。我们只需写出所有字段，后面跟一个 `|`，或者对于最后一个字段，跟一个换行符。这项工作在下面添加到 Employee 类中的 `writeEmployee` 方法中完成：

```
public static void writeEmployee(PrintWriter out, Employee e)
{
    out.println(e.getName() + "|" + e.getSalary() + "|" + e.getHireDay());
}
```

要读取记录，我们一次读取一行并分隔字段。我们使用扫描器读取每一行，然后用 `String.split` 方法将该行拆分为标记。

```
public static Employee readEmployee(Scanner in)
{
    String line = in.nextLine();
    String[] tokens = line.split("\\|");
    String name = tokens[0];
    double salary = Double.parseDouble(tokens[1]);
    LocalDate hireDate = LocalDate.parse(tokens[2]);
    int year = hireDate.getYear();
    int month = hireDate.getMonthValue();
    int day = hireDate.getDayOfMonth();
    return new Employee(name, salary, year, month, day);
}
```

`split` 方法的参数是描述分隔符的正则表达式。我们将在本章末尾更详细地讨论正则表达式。碰巧的是，竖线字符在
