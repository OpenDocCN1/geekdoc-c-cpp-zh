
## ArrayList

第 16 章介绍了数组。这是不错的内容，但在任何编程语言中，数组都有其局限性。例如，假设有一个大小为 100 的数组。如果突然需要存储第 101 个值，你就完全没辙了。在不重写一些代码的情况下，你无法改变数组的大小。将值插入数组是另一个问题。为了让 "Tim" 按字母顺序挤在 "Thom" 和 "Tom" 之间，你可能不得不通过移动成千上万个 "Tyler"、"Uriah" 和 "Victor" 名字来腾出空间。

但 Java 有一个 ArrayList 类。ArrayList 就像数组，只是 ArrayList 对象会根据需要增长和缩小。你也可以使用 ArrayList 类的 add 方法轻松插入新值。ArrayList 对象非常有用，因为它们能做各种数组做不到的好事。

## File

谈谈你有用的 Java 类吧！File 类做了很多本书示例中未包含的事情。方法 canRead 告诉你是否可以从文件中读取。方法 canWrite 告诉你是否可以向文件写入。调用方法 setReadOnly 可确保你不会意外写入文件。方法 deleteOnExit 会擦除文件，但要等到你的程序停止运行后才执行。方法 exists 检查你是否拥有特定文件。方法 isHidden、lastModified 和 length 能为你提供有关文件的更多信息。你甚至可以通过调用 mkdir 方法创建新目录。承认吧，这个 File 类功能强大！

## Integer

第 18 章描述了 Integer 类及其 parseInt 方法。Integer 类还有许多其他特性，在处理 int 值时非常有用。例如，Integer.MAX_VALUE 代表数字 2147483647。那是 int 变量可以存储的最大值。（参见第 7 章。）表达式 Integer.MIN_VALUE 代表数字 -2147483648（int 变量可以存储的最小值）。对 Integer.toBinaryString 的调用接受一个 int 并返回其基数为 2（二进制）的表示。而 Integer.toBinaryString 对基数 2 所做的，Integer.toHexString 对基数 16（十六进制）做同样的事。

## Math

你有要计算的数字吗？你用电脑做奇特的计算吗？如果是这样，试试 Java 的 Math 类。（它是一段代码，不是坐下来听代数讲座的地方。）Math 类处理 π、e、对数、三角函数、平方根，以及所有那些让大多数人感到毛骨悚然的数学事物。

## NumberFormat

第 18 章有一节关于 NumberFormat.getCurrencyInstance 方法的内容。使用此方法，你可以将 20.338500000000003 转换为 $20.34。如果美国不是你的家乡，或者你的公司在全球销售产品，你可以用 Java Locale 增强你的货币实例。例如，使用 euro = NumberFormat.getCurrencyInstance(Locale.FRANCE)，对 euro.format(3) 的调用会返回 3,00 € 而不是 $3.00。

NumberFormat 类还具有用于显示非货币金额的方法。例如，你可以带或不带逗号显示数字，带或不带前导零，并包含你想要的任意多位小数。

## Scanner

Java 的 Scanner 类能做的比本书示例中的更多。与 NumberFormat 类一样，Scanner 可以处理来自各种区域设置的数字。例如，要输入 3,5 并使其表示“three and half”，你可以输入 myScanner.useLocale(Locale.FRANCE)。你还可以告诉 Scanner 跳过某些输入字符串或使用 10 以外的数字基数。总的来说，Scanner 类非常多才多艺。

## String

第 18 章研究了 Java 的 String 类。该章节详细（血淋淋地）描述了一个名为 equals 的方法。String 类还有许多其他有用的方法。例如，使用 length 方法，你可以找到字符串中的字符数。使用 replaceAll，你可以轻松地将短语 "my fault" 更改为 "your fault"，无论 "my fault" 在字符串中出现在哪里。而使用 compareTo，你可以按字母顺序对字符串进行排序。

## StringTokenizer

我经常需要把字符串切成块。例如，我有一个 fullName 变量，存储了我自恋的 "Barry A. Burd" 字符串。从这个 fullName 值，我需要创建 firstName、middleInitial 和 lastName 值。我有一个大字符串（"Barry A. Burd"），需要三个小字符串——"Barry"、"A." 和 "Burd"。

幸运的是，StringTokenizer 类完成了这种繁重的工作。使用此类，你可以将 "Barry A. Burd" 或 "Barry, A. , Burd" 甚至 "Barry<tab>A.<tab>Burd" 分成块。你也可以将每个分隔符视为有价值的数据，或者像垃圾一样忽略每个分隔符。要使用字符串进行大量有趣的处理，请查看 Java 的 StringTokenizer 类。

## System

你可能熟悉 System.in 和 System.out。但 System.getProperty 呢？getProperty 方法揭示了有关你的计算机的各种信息。你可以找到的信息包括你的操作系统的名称、你的处理器的架构、你的 Java 虚拟机版本、你的类路径、你的用户名，以及你的系统使用反斜杠还是正斜杠来分隔文件夹名称。当然，你可能已经知道所有这些东西。但你的 Java 代码需要在运行时发现它吗？

## Index

### Symbols and Numerics

- + (加号)
- 用于加法，139，378
- 使用其连接字符串，378
- ++（前置递增运算符），144–145
- ()（括号）
- 调用方法，377
- 调用对象的方法，377
- 类型转换，144
- 使用条件，205–206
- 在 if 语句中，181
- 方法和，161
- .（点）
- 调用对象的方法，357
- 引用对象的部分，341
- 在正则表达式中，161
- ;（分号）
- for 语句之后，289
- 以此结束语句，93
- 在 if 语句中，181，182
- &&（与号），194
- *（星号），用于乘法，139
- {}（大括号）
- 像盒子一样作用，86
- 在块中，191，237
- 级联 if 语句和，212
- 在类中，95
- 缺失，在 if 语句中，182
- 语句在，235，237，238
- 太多，114–115
- 用法，85–86
- ""（花式引号），64
- ==（等于），166
- <（小于），166
- <=（小于或等于），166
- >（大于），166
- >=（大于或等于），166
- !=（不等于），166
- -（减号），139
- %（百分号），作为余数运算符，140
- []（方括号），85
- ""（直引号），引号，64
- _（下划线字符）
- 在类名中，62
- 与数字一起，作为字面量，85
- ?:（问号冒号）条件运算符，230
- && 运算符（与），194
- ! 运算符（非，负，或不行），194，195
- || 运算符（或），作为包含，194，195
- @ 符号，尝试从电子邮件地址获取用户名，246–250，276，279–283

### A

- 缩写，在 import 声明中，192
- 抽象方法，113
- abstract 修饰符，113
- Abstract Window Toolkit（AWT），394，395
- Account 类，373–376
- 操作，Eclipse，69
- 活动编辑器，72
- 活动视图，72
- Add Body 快速修复，113
- addInterest 方法，383–386
- 加法，加号，139
- All-in One 下载，409
- 全形字，173
- amount 变量，122–123
- double 关键字，127
- 第一个值，131
- 初始化，131
- anAccount.display 方法，377

级联 if 语句和，212
在类中，95
缺失，在 if 语句中，182
语句在，235，237，238
太多，114–115
用法，85–86
方括号，85，320
break 语句
定义，220
fall-through 和，224–229
断点，170
Breakpoints 视图，Eclipse IDE，170
按钮控件，412–422
byte 类型，151，152
字节码
定义，14，16
总体，17–19
Java 虚拟机和，18
● C ●
C++
Eclipse 用于编程的工具，39
总体，95
.cab 文件，26
调用
对象的 methods，357
一个方法，89–92，375–376
静态和非静态方法，358–359
canRead 方法，428
canWrite 方法，428
大小写
错误，116–118
toUpperCase 方法，154–156
Card Total，240–242，244
级联 if 语句，209–212
case 子句，switch 语句，219–220
大小写敏感
定义，64
错误，108–110
Java 语言，81
类型转换，144
摄氏度，将温度转换为华氏度的程序，166–169
char 类型
定义，154
使用列表，154
作为数字类型，173
char 变量，仅存储一个字符，157
字符
字母顺序，172
比较，172–173
比较运算符，166
定义，154
读取，162–163
Character.toUpperCase 方法，154–156，158
charAt 方法，162–163
速查表，6
Check 类，357，358，368，369
chevron（双箭头），Eclipse IDE，73
Chrome 浏览器，32
.class 文件，定义，14
class 关键字，81
类
组合和使用数据，357
概念，344
将你的代码转换为使用，336
创建，334–335
大括号 {} 在，95
在其中定义方法，371
与对象之间的差异，338
扩展，403–405
用于 GUI 应用程序，394
Abstract Window Toolkit（AWT），394
Eclipse 的 Standard Widget Toolkit（SWT），395
JavaFX 类，395，407–413，418
Swing 类，394–395，403
继承方法，405
JavaFX，395，407–413，418
JFrame
创建实例，400–401
描述，398–400
扩展，403–405
对象，338–340
问题和答案，345
引用类型和，335
