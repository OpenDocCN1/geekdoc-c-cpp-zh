
## java.util.Scanner 5

- `Scanner(InputStream in)`  
  从给定的输入流构造一个扫描器对象。
- `String nextLine()`  
  读取下一行输入。
- `String next()`  
  读取下一个单词输入（以空白字符分隔）。
- `int nextInt()`
- `double nextDouble()`  
  读取并转换下一个表示整数或浮点数的字符序列。
- `boolean hasNext()`  
  测试输入中是否还有另一个单词。
- `boolean hasNextInt()`
- `boolean hasNextDouble()`  
  测试下一个字符序列是否表示整数或浮点数。

## java.lang.System 1.0

- `static Console console()` 6  
  如果可以通过控制台窗口与用户交互，则返回一个用于通过控制台窗口与用户交互的 Console 对象，否则返回 null。任何在控制台窗口中启动的程序都可以使用 Console 对象。否则，可用性取决于系统。

## java.io.Console 6

- `static char[] readPassword(String prompt, Object... args)`
- `static String readLine(String prompt, Object... args)`

显示提示符并读取用户输入，直到输入行末尾。可选的 `args` 参数用于提供格式化参数，如下一节所述。

### 3.7.2 格式化输出

可以使用语句 `System.out.print(x)` 将数字 `x` 打印到控制台。该命令会以该类型最大数量的非零数字打印 `x`。例如，

```java
double x = 10000.0 / 3.0;
System.out.print(x);
```

打印

```
3333.3333333333335
```

例如，如果你想显示美元和美分，这就是个问题。

补救方法是 `printf` 方法，它遵循 C 库中由来已久的约定。例如，调用

```java
System.out.printf("%8.2f", x);
```

会以 8 个字符的*字段宽度*和 2 个字符的*精度*打印 `x`。也就是说，输出包含一个前导空格和以下七个字符

```
 3333.33
```

可以向 `printf` 提供多个参数。例如：

```java
System.out.printf("Hello, %s. Next year, you'll be %d", name,
age);
```

每个以 % 字符开头的*格式说明符*都会被替换为相应的参数。结束格式说明符的*转换字符*表示要格式化的值的类型：f 是浮点数，s 是字符串，d 是十进制整数。[表 3.5](#table-3-5) 显示了所有转换字符。

大写变体会生成大写字母。例如，"%8.2E" 将 3333.33 格式化为 3.33E+03，其中 E 为大写。

**表 3.5** `printf` 的转换

| 转换字符 | 类型 | 示例 |
|---|---|---|
| `d` | 十进制整数 | `159` |
| `x` 或 `X` | 十六进制整数。若要对十六进制格式进行更多控制，请使用 HexFormat 类。 | `9f` |
| `o` | 八进制整数 | `237` |
| `f` 或 `F` | 定点浮点数 | `15.9` |
| `e` 或 `E` | 指数浮点数 | `1.59e+01` |
| `g` 或 `G` | 通用浮点数（e 和 f 中较短者） | — |
| `a` 或 `A` | 十六进制浮点数 | `0x1.fccd3` |
| `s` 或 `S` | 字符串 | `Hello` |
| `c` 或 `C` | 字符 | `H` |
| `b` 或 `B` | 布尔值 | `true` |
| `h` 或 `H` | 哈希码 | `42628b2` |
| `tx` 或 `Tx` | 旧式日期和时间格式化。请改用 java.time 类——参见第二卷第 6 章。 | — |
| `%` | 百分号 | `%` |
| `n` | 平台相关的行分隔符 | — |

**注意：**

可以使用 `s` 转换来格式化任意对象。如果任意对象实现了 `Formattable` 接口，则调用该对象的 `formatTo` 方法。否则，调用 `toString` 方法将对象转换为字符串。`toString` 方法在[第 5 章](#)中讨论，接口在[第 6 章](#)中讨论。

此外，可以指定控制格式化输出外观的*标志*。表 3.6 显示了所有标志。例如，逗号标志添加分组分隔符。即，

```java
System.out.printf("%,.2f", 10000.0 / 3.0);
```

打印

```
3,333.33
```

可以使用多个标志，例如 "%(,.2f" 以使用分组分隔符并将负数括在括号中。

**表 3.6** printf 的标志

| 标志 | 用途 | 示例 |
| --- | --- | --- |
| + | 为正数和负数打印符号。 | +3333.33 |
| space | 在正数前添加一个空格。 | \| 3333.33\| |
| 0 | 添加前导零。 | 003333.33 |
| - | 左对齐字段。 | \|3333.33 \| |
| ( | 将负数括在括号中。 | (3333.33) |
| , | 添加分组分隔符。 | 3,333.33 |
| #（用于 f 格式） | 始终包含小数点。 | 3,333. |
| #（用于 x 或 o 格式） | 添加 0x 或 0 前缀。 | 0xcafe |
| $ | 指定要格式化的参数索引；例如，%1$d %1$x 以十进制和十六进制打印第一个参数。 | 159 9F |
| < | 使用与上一个说明相同的值进行格式化；例如，%d %<x 以十进制和十六进制打印同一个数。 | 159 9F |

可以使用静态 `String.format` 方法创建格式化字符串而不打印它：

```java
String message = String.format("Hello, %s. Next year, you'll be %d", name, age + 1);
```

**注意：**

从 Java 15 开始，可以改用 `formatted` 方法，从而少写五个字符：

```java
String message = "Hello, %s. Next year, you'll be %d".formatted(name, age + 1);
```

现在你已经了解了 `printf` 方法的所有功能。[图 3.6](#) 显示了格式说明符的语法图。

![](img/0e7b74ef51a065c077b42cd87b362288_134_0.png)

**图 3.6** 格式说明符语法

> **注意：**
> 
> 格式化是*区域设置特定的*。例如，在德国，分组分隔符是句点，而不是逗号。第二卷的[第 7 章](#)展示了如何控制应用程序的国际化行为。

### 3.7.3 文件输入和输出

要从文件读取，请像这样构造一个 `Scanner` 对象：

```java
Scanner in = new Scanner(Path.of("myfile.txt"),
    StandardCharsets.UTF_8);
```

如果文件名包含反斜杠，请记得用额外的反斜杠对每个反斜杠进行转义：`"c:\\mydirectory\\myfile.txt"`。

现在可以使用你已经遇到的任何 Scanner 方法从文件读取。

![](img/0e7b74ef51a065c077b42cd87b362288_135_0.png)

**注意：**

此处，我们指定了 UTF-8 字符编码，这对于 Internet 上的文件很常见（但并非普遍）。读取文本文件时需要知道字符编码（更多信息参见第二卷第 2 章）。如果省略字符编码，则会使用运行 Java 程序的计算机的“默认编码”。这不是个好主意——程序的行为可能因运行位置而异。

![](img/0e7b74ef51a065c077b42cd87b362288_135_1.png)

**警告：**

可以使用字符串参数构造 Scanner，但扫描器会将字符串解释为数据，而不是文件名。例如，如果调用

```java
Scanner in = new Scanner("myfile.txt"); // ERROR?
```

那么扫描器将看到十个字符的数据：'m'、'y'、'f' 等。在此情况下，这很可能不是本意。

要写入文件，请构造一个 PrintWriter 对象。在构造函数中，提供文件名和字符编码：

```java
PrintWriter out = new PrintWriter("myfile.txt",
StandardCharsets.UTF_8);
```

如果文件不存在，则会创建它。可以像打印到 `System.out` 时那样使用 `print`、`println` 和 `printf` 命令。

![](img/0e7b74ef51a065c077b42cd87b362288_136_0.png)

**注意：**

当你指定相对文件名（例如 `"myfile.txt"`、`"mydirectory/myfile.txt"` 或 `"../myfile.txt"`）时，文件将相对于启动 Java 虚拟机的目录来定位。如果你从命令 shell 启动程序，通过执行

```java
java MyProg
```

那么起始目录就是命令 shell 的当前目录。但是，如果你使用集成开发环境，则由它控制起始目录。可以通过以下调用找到目录位置：

```java
String dir = System.getProperty("user.dir");
```

如果在定位文件时遇到麻烦，请考虑使用绝对路径名，例如 `"c:\\mydirectory\\myfile.txt"` 或 `"/home/me/mydirectory/myfile.txt"`。

如你所见，访问文件就像使用 `System.in` 和 `System.out` 一样容易。只有一个问题：如果用一个不存在的文件构造 `Scanner`，或者用一个无法创建的文件名构造 `PrintWriter`，就会发生异常。例如，Java 编译器认为这些异常比“除以零”异常更严重。在第 7 章中，你将学习处理异常的各种方式。目前，你只需告诉编译器你已意识到可能发生“输入/输出”异常。为此，用 `throws` 子句标记 `main` 方法，如下所示：
