
其中 `k` 是取决于弹簧的常数（在此模拟中使用 `10 N/m`）。从给定的位移 `x` 开始（例如 `0.5` 米）。将初始速度 `v` 设为 `0`。计算。

# 316 第 6 章 数组与数组列表

```java
While (i < j)
  If (a[i] is odd)
    Swap elements at positions i and j
  Else
    i++
```
32. 这是一个解决方案。其思路是移除所有元素并将它们移动到末尾。技巧在于知道何时停止。通过将奇数元素移动到已经包含移动元素的区域是没有任何意义的，因此我们想用另一个回形针标记该区域。

`i = 0`
`moved = size`
`While (i < moved)`
  `If (a[i] is odd)`
    `Remove the element at position i and add it at the end.`
    `moved;`

```java
36. String[][] board = new String[3][3];
37. board[0][2] = "x";
38. board[0][0], board[1][1], board[2]
```

```java
39. ArrayList<Integer> primes =
new ArrayList<Integer>();
primes.add(2);
primes.add(5);
primes.add(5);
primes.add(7);
primes.add(11);
```

```java
40. for (int i = primes.size() - 1; i >= 0; i--)
  System.out.println(primes.get(i));
```
41. "Ann", "Cal",
42. 变量 `names` 未初始化。
43. `names` 包含 "Emily", "Bob", "Cindy", "Dave"; `names2` 包含 "Dave",
44. 因为工作日的数量不会改变，所以使用数组没有缺点，而且更容易初始化：
33. 当你一次读取一个输入且无法预先查看时，从牌牌中一次一次地抽取牌牌，比查看一个全部展示的元素序列更能模拟这一过程。
45. 将输入读取到数组列表中更简单。

```java
String[] weekdayNames = { "Monday", "Tuesday", "Wednesday", "Friday", "Saturday", "Sunday" };
```
34. 你得到了我们比赛中金牌、银牌和铜牌的总数。每种各有四个。

```java
35. for (int i = 0; i < 8; i++)
  for (int j = 0; j < 8; j++)
    board[i][j] = (i + j) % 2;
```

# 第 7 章
输入/输出与异常处理

## 章节目标

- 读取和写入文本文件
- 处理命令行参数
- 抛出和捕获异常
- 实现传播检查异常的程序

## 章节目录

7.1 读取和写入文件 318
常见错误 7.1：文件名中的反斜杠 321
常见错误 7.2：使用字符串构造 Scanner 321n
特殊专题 7.1: 读取网页 321
特殊专题 7.2: 文件对话框 321
特殊专题 7.3: 读取和写入二进制数据 322
7.2 输入与输出 323
特殊专题 7.4: 正则表达式 330
视频示例 7.1: 计算文档的可读性

7.4 异常处理 337
语法 7.1: 抛出异常 338
语法 7.2: 捕获异常 341
语法 7.3: throws 子句 343
语法 7.4: finally 子句 344
编程 7.1: 尽抛出，晚捕获 345
编程 7.2: 不要吞掉异常 345
编程 7.3: 在同一个 try 语句中使用 catch 和 finally 3346
特殊专题 7.5: Java 7 中的自动资源管理 346
随机逸闻 7.2: 阿里阿德纳火箭事件 347

7.3 命令行参数 330
方法 7.1: 处理文件 333
随机逸闻 7.1: 加密算法 336
实例示例 7.1: 分析婴儿名字

7.5 应用：处理输入错误 347
视频示例 7.2: 检测财务欺诈

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_352_0.png)

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_353_0.png)

在本章中，你将学习如何读取和写入文件——这是处理真实数据的一种非常有用的技能。作为一个应用，你将学习如何加密数据（左侧所示恩格玛机是二世界大战期间德国使用的加密设备。英国的先驱科学家们破解了密码并能够解读信息，这对赢得战争提供了巨大的帮助）。本章的其余部分将告诉你如何使用 Java 语言的异常处理机制从问题（如文件丢失或格式错误的内容）中恢复。

## 7.1 读取和写入文本文件

我们本章开始讨论读取和写入包含文本文件的常见任务。文本文件不仅包括使用简单文本编辑器（如 Windows 记本）创建的文件，还包括 Java 源代码和 HTML 文件。在 Java 中，读取最方便的机制是使用 `Scanner`。为了从磁盘文件读取，`Scanner` 类扩展了一个描述磁盘文件和目录的类。`File` 类有许多方法，例如删除或重命名文件。

首先，使用输入文件名构造 `File` 对象：

```java
File inputFile = new File("input.txt");
```

然后使用 `File` 对象构造 `Scanner` 对象：

```java
Scanner in = new Scanner(inputFile);
```

此 `Scanner` 对象从 `input.txt` 读取文本。你可以使用 `Scanner` 方法（如 `next()`,`nextDouble()`）从输入文件中读取数据。例如，你可以使用以下循环处理输入文件中的数字：

```java
while (in.hasNextDouble()) {
  double value = in.nextDouble();
  printWriter.println(value);
}
```

要输出到文件，使用所需的文件构造 `PrintWriter` 对象：

```java
PrintWriter printWriter = new PrintWriter("output.txt");
```

如果输出文件已存在，在写入之前会被编辑。如果文件不存在，则创建一个空文件。`PrintWriter` 是 `PrintStream` 类的增强——你可以对 `PrintWriter` 对象使用熟悉的 `print`、`println` 和 `printf` 方法：

```java
out.println("Hello, World!");
out.printf("Total: %.2f%n", total);
```

写入文本文件时使用 `PrintWriter` 类和 `print/println/printf` 方法。当你完成文件处理时，确保关闭 `Scanner` 或 `PrintWriter`，输出可能不会写入磁盘。以下程序将这些概念结合起来。它读取包含数字的文件，并将数字写入另一个文件，并按列对齐，最后是总数。例如，如果输入文件的内容如下：

```
32 54
67.5 29
35 80
115 44.5 65
```

那么输出文件为：

```
32.00
54.00
67.50
29.00
35.00
80.00
115.00
44.50
100.00
65.00
```

如果输入或输出文件不存在，构造对象时会发生 `FileNotFoundException`。编译器要求我们指定发生这种情况时程序应该做什么。同样，如果 `PrintWriter` 无法打开写入的文件，就会产生此异常（这可能是路径非法或用户没有权限在该位置创建文件）。在我们的示例程序中，如果发生异常，我们终止 `main` 方法。为了实现这一点，我们为方法标记：

```java
public static void main(String[] args) throws FileNotFoundException
```

你将在 7.4 节看到如何以更专业的方式处理异常。`File`、`PrintWriter` 和 `FileNotFoundException` 类位于 `java.io` 包中。

### section_1/Total.java

```java
1 import java.io.File;
2 import java.io.FileNotFoundException;
3 import java.io.PrintWriter;
4 import java.util.Scanner;

/**
此程序读取一个包含数字的文件，并将数字写入另一个
按列对齐，最后是总数。
*/
public class Total
{
public static void main(String[] args) throws FileNotFoundException
{
```

# 第 7 章 输入/输出与异常处理

```java
// 输入输出文件名
Scanner console = new Scanner(System.in);
System.out.print("Input file: ");
String fileName = console.next();
System.out.print("Output file: ");
String outputFile = console.next();

// 构造用于读写的 Scanner 和 PrintWriter 对象
File inputFile = new File(fileName);
Scanner in = new Scanner(inputFile);
PrintWriter out = new PrintWriter(outputFile);

// 读取输入并写入输出
double total = 0;
while (in.hasNextDouble()) {
    double value = in.nextDouble();
    out.printf("%5.2f\n", value);
    total += value;
}
out.printf("Total: %.2f%n", total);
in.close();
out.close();
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_355_0.png)

- 1. 如果为 `Total` 程序提供相同的输入和输出文件名，会发生什么？如果不确定请尝试一下。
2. 如果为 `Total` 程序提供一个不存在的输入文件名为，会发生什么？如果不确定请尝试一下。
3. 假设你想将总数添加到现有文件中，而不是写入新文件。自检表明你不能简单地通过指定相同的输入和输出文件来实现。你如何完成此任务？提供解决方案的伪代码。
4. 你如何修改程序使其显示列的平均值而不是总数，如下所示：
5. 你如何修改 `Total` 程序使其以两列的形式写入值：

| 32.00 | 54.00 |
| 67.50 | 29.00 |
| 35.00 | 80.00 |
| 115.00 | 44.50 |
| 100.00 | 65.00 |
| Total: | 622.00 |

现在练习。你可以尝试章节末的练习：R7.1, R7.2, P7.1。

## 7.1 读取和写入文本文件 321

## 常见错误 7.1
### 文件名中的反斜杠

当你以字符串字面量的形式指定文件名时，如果该名称包含反斜杠字符（如 Windows 文件名所示），你必须每个反斜杠都提供两次：

```java
InputFile = new File("c:\\homework\\input.dat");
```

引号字符串内的单个反斜杠是一个转义字符，它会与后续字符结合形成一个特殊含义，例如 `\n` 表示换行。`\\` 则表示单个反斜杠。

然而，当用户向程序提供文件名时，用户不应该输入两次反斜杠。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_356_0.png)

## 常见错误 7.2
### 使用字符串构造 Scanner

当你用它构造 `PrintWriter` 时，它会将内容写入文件：

```java
PrintWriter out = new PrintWriter("output.txt");
```

这对于 `Scanner` 是不起作用的。以下语句

```java
Scanner in = new Scanner("input.txt"); // 错误？
```

并没有打开文件。相反，它会读取文件：`in.next()` 返回字符串 "input.txtn这有时很有用——参见第 7.2.4 节）。

你必须记住在 `Scanner` 构造函数中使用 `File` 对象：

```java
Scanner in = new Scanner(new File("input.txt")); // OK
```

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_356_1.png)

## 特殊课题 7.1
### 读取网页

你可以使用以下系列命令来读取网页的内容：

```java
String address = "http://mysite.com/index.html";
URL location = new URL(address);
Scanner in = new Scanner(location.openStream());
```

现在只需按通常方式使用 `Scanner` 读取网页内容即可。构造函数和 `openStream` 方法会抛出 `IOException`，因此你需要在 `main` 方法中声明 `throws IOException`。（有关该子句的更多信息请参见第 7.4.3 节。）

`URL` 类位于 `java.net` 包中。

> 在线示例：一个从网页读取数据的程序。

## 特殊课题 7.2
### 文件对话框

在带有图形用户界面的程序中，每当程序用户需要选择文件时，你都会希望使用文件对话框（如如下所示）。`JFileChooser` 为 Swing 用户界面工具包实现了一个文件对话框。

`JFileChooser` 类有许多选项可以精细调整对话框的显示，但在最基本的形式下它非常简单：构造一个对象选择器；然后使用 `showDialog` 或 `saveOpenDialog` 方法。这两个方法都显示同一个对话框，但根据你调用的方法不同，选择文件的按钮将标记为“打开”或“保存”。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_356_2.png)

## 第 7 章 输入/输出和位置处理

为了让对话框在屏幕上的位置更佳，你可以指定弹出对话框的用户界面组件。如果你不在乎对话框弹出的位置，可以简单传递 `null`。`openDialog` 和 `saveDialog` 方法返回 `JFileChooser.APPROVE_OPTION`（如果用户已选择文件）或 `JFileChooser.CANCEL`（如果用户取消选择）。如果选择了文件，你就可以使用 `getFile` 方法获取描述该文件的 `File` 对象。这里是一个完整的示例：

```java
JFileChooser chooser = new JFileChooser();
Scanner in = null;
if (chooser.showDialog(null) == JFileChooser.APPROVE_OPTION) {
    File selectedFile = chooser.getSelectedFile();
    in = new Scanner(selectedFile);
}
```

在线示例：
- 一个演示如何使用选择器的程序。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_357_0.png)

## 读取和写入数据

你使用 `Scanner` 和 `PrintWriter` 类来读取和写入文本文件。文本文件包含字符序列。其他文件（如图像）不是由字符组成的，而是由字节组成的。字节是计算机存储的基本单位——由八个二进制位组成的数字（一个字节可以表示 0 到 255 之间的无符号整数，或 -128 到 127 之间的符号整数）。Java 库有一组称为流的类，用于处理二进制文件。虽然修改二进制文件具有挑战性且超出了本书的范围，但我们为你提供了一个简单的示例，从网站拷贝二进制数据到文件。

你使用 `InputStream` 读取二进制数据。例如：

```java
URL location = new URL("http://horstmann.com/everyone/duke.gif");
InputStream in = location.openStream();
```

要向文件写入二进制数据，使用 `FileOutputStream`：
```java
FileOutputStream out = new FileOutputStream("duke.gif");
```

## 特殊课题 7.3
## 7.2 输入输入输出 323

输入流的 `read` 方法读取单个字节，并在流结束时返回 -1。输出流写入单个字节。

### 7.2.1 读取单词

在接下来的章节中，你将学习如何处理单词。`Scanner` 的 `next` 方法返回任何非空白字符序列。空白包括空格、制表符和换行符。例如，以下字符串是单词：

```java
while (in.hasNext()) {
    String input = in.next();
    System.out.println(input);
}
```
