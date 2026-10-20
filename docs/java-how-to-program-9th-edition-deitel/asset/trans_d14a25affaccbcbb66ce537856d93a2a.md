

## G.11 使用参数索引打印

参数索引是可选的整数后跟一个 $ 符号，用于指示参数在参数列表中的位置。例如，图 G.9 中的第 20–22 行和第 25–26 行使用参数索引 "1$" 来指示所有格式说明符都使用参数列表中的第一个参数。参数索引使程序员能够重新排序输出，使得参数列表中的参数不一定按其对应的格式说明符的顺序排列。参数索引还有助于避免重复参数。图 G.22 使用参数索引按相反顺序打印参数列表中的参数。

```
1  // Fig. G.22: ArgumentIndexTest
2  // Reordering output with argument indices.
3
4  public class ArgumentIndexTest
5  {
6      public static void main( String[] args )
7      {
8          System.out.printf(
9              "Parameter list without reordering: %s %s %s %s\n",
10             "first", "second", "third", "fourth" );
11          System.out.printf(
12              "Parameter list after reordering: %4$s %3$s %2$s %1$s\n",
13             "first", "second", "third", "fourth" );
14      } // end main
15  } // end class ArgumentIndexTest
```

Parameter list without reordering: first second third fourth
Parameter list after reordering: fourth third second first

Fig. G.22 | Reordering output with argument indices.

## G.12 使用转义序列打印字面量

大多数要在 printf 语句中打印的字面字符可以直接包含在格式字符串中。然而，存在一些“问题”字符，例如用于分隔格式字符串本身的引号（"）。各种控制字符，例如换行和制表符，必须由转义序列表示。转义序列由反斜杠（\）表示，后跟转义字符。图 G.23 列出了转义序列及其引起的作用。

| Escape sequence | Description |
|---|---|
| \' (single quote) | Output the single quote (') character. |
| \" (double quote) | Output the double quote (") character. |
| \\ (backslash) | Output the backslash (\) character. |
| \b (backspace) | Move the cursor back one position on the current line. |
| \f (new page or form feed) | Move the cursor to the start of the next logical page. |
| \n (newline) | Move the cursor to the beginning of the next line. |
| \r (carriage return) | Move the cursor to the beginning of the current line. |
| \t (horizontal tab) | Move the cursor to the next horizontal tab position. |

Fig. G.23 | Escape sequences. (Part 1 of 2.)
Fig. G.23 | Escape sequences. (Part 2 of 2.)

> Common Programming Error G.4
> Attempting to print as literal data in a printf statement a double quote or backslash character without preceding that character with a backslash to form a proper escape sequence might result in a syntax error.

## G.13 使用类 Formatter 格式化输出

到目前为止，我们讨论了如何将格式化的输出显示到标准输出流。如果我们想将格式化的输出发送到其他输出流或设备，例如 JTextArea 或文件，该怎么办？解决方案依赖于类 Formatter（位于包 java.util 中），它提供了与 printf 相同的格式化功能。Formatter 是一个实用类，使程序员能够将格式化数据输出到指定的目标，例如磁盘上的文件。默认情况下，Formatter 会在内存中创建一个字符串。图 G.24 演示了如何使用 Formatter 构建一个格式化的字符串，然后在消息对话框中显示。

第 11 行使用默认构造函数创建一个 Formatter 对象，因此该对象将在内存中构建一个字符串。提供了其他构造函数，允许您指定应输出格式数据的目标。详情请参阅 java.sun.com/javase/6/docs/api/java/util/Formatter.html。

```
1  // Fig. G.24: FormatterTest.java
2  // Formatting output with class Formatter.
3  import java.util.Formatter;
4  import javax.swing.JOptionPane;
5
6  public class FormatterTest
7  {
8      public static void main( String[] args )
9      {
10         // create Formatter and format output
11         Formatter formatter = new Formatter();
12         formatter.format( "%d = %o = %X", 10, 10, 10 );
13
14         // display output in JOptionPane
15         JOptionPane.showMessageDialog( null, formatter.toString() );
16     } // end main
17 } // end class FormatterTest
```

Fig. G.24 | Formatting output with class Formatter. (Part 1 of 2.)

![](img/009e962758dcc71dbc43a493362e6dc0_1450_0.png)

Fig. G.24 | Formatting output with class Formatter. (Part 2 of 2.)

第 12 行调用 format 方法来格式化输出。与 printf 类似，format 方法接受格式字符串和参数列表。不同之处在于 printf 将格式化的输出直接发送到标准输出流，而 format 将格式化的输出发送到其构造函数指定的目标（本程序中为内存中的字符串）。第 15 行调用 Formatter 的 toString 方法以获取格式化的字符串数据，然后在消息对话框中显示。

类 String 还提供了一个名为 format 的静态便捷方法，使您能够在无需先创建 Formatter 对象的情況下创建内存中的字符串。图 G.24 中的第 11–12 行和第 15 行可以被替换为

```
String s = String.format( "%d = %o = %x", 10, 10, 10 );
JOptionPane.showMessageDialog( null, s );
```

## G.14 总结

本附录总结了如何使用各种格式字符和标志显示格式化输出。我们使用格式字符 d、o、x 和 X 显示十进制数；使用格式字符 e、E、f、g 和 G 显示浮点数；以及使用格式字符 t 和 T 及其转换后缀字符以各种格式显示日期和时间。您学习了如何使用字段宽度和精度显示输出。我们介绍了与格式字符一起使用的标志 +、-、空格、#、0、逗号和 (，以产生输出。我们还演示了如何使用类 Formatter 格式化输出。

## Summary

### Section G.2 Streams
- 输入和输出通常使用流执行，流是字节序列。
- 通常，标准输入流连接到键盘，标准输出流连接到计算机屏幕。

### Section G.3 Formatting Output with printf
- printf 格式字符串描述输出值出现的格式。格式说明符由参数索引、标志、字段宽度、精度和转换字符组成。

### Section G.4 Printing Integers
- 整数使用转换字符 d 打印十进制整数，o 打印八进制形式的整数，x（或 X）打印十六进制形式的整数。X 显示大写字母。

### Section G.5 Printing Floating-Point Numbers
- 浮点值使用转换字符 e（或 E）打印指数记数法，f 打印常规浮点记数法，g（或 G）打印 e（或 E）记数法或 f 记数法。对于 g 转换说明符，如果值小于 10⁻³ 或大于或等于 10⁷，则使用 e 转换字符；否则使用 f 转换字符。

### Section G.6 Printing Strings and Characters
- 转换字符 c 打印一个字符。
- 转换字符 s（或 S）打印一个字符字符串。转换字符 S 以大写字母显示输出。

### Section G.7 Printing Dates and Times
- 转换字符 t（或 T）后跟转换后缀字符以各种形式打印日期和时间。转换字符 T 以大写字母显示输出。
- 转换字符 t（或 T）要求参数为 long、Long、Calendar 或 Date 类型。

### Section G.8 Other Conversion Characters
- 转换字符 b（或 B）输出布尔值或 Boolean 的字符串表示。这些转换字符还对非空引用输出 "true"，对空引用输出 "false"。转换字符 B 输出大写字母。
- 转换字符 h（或 H）对空引用返回 null，并返回对象的哈希码值（以 16 为底）的字符串表示。哈希码用于在 Hashtables 和 HashMaps 中存储和检索对象。转换字符 H 输出大写字母。
- 转换字符 n 打印平台特定的行分隔符。
- 转换字符 % 用于显示字面 %。

### Section G.9 Printing with Field Widths and Precisions
- 如果字段宽度大于正在打印的对象，则对象在字段中右对齐。
- 字段宽度可与除行分隔符转换之外的所有转换字符一起使用。
- 与浮点转换字符 e 和 f 一起使用时，精度表示小数点后出现的位数。与浮点转换字符 g 一起使用时，精度表示出现的有效位数。
- 与转换字符 s 一起使用时，精度表示要打印的字符数。
- 字段宽度和精度可以通过在百分号和转换字符之间放置字段宽度、后跟小数点、后跟精度来组合。

### Section G.10 Using Flags in the printf Format String
- - 标志在字段中左对齐其参数。
- + 标志为正值打印加号，为负值打印减号。
- 空格标志在正值前打印一个空格。空格标志和 + 标志不能在整数转换字符中一起使用。
- # 标志在八进制值前加上 0，在十六进制值前加上 0x。
- 0 标志为未占据整个字段的值打印前导零。
- 逗号（,）标志使用特定于区域设置的千位分隔符来显示整数和浮点数。
- ( 标志用括号括起负数。

