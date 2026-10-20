

| Operator | Description | Associativity |
|---|---|---|
| | | 位包含或 |
| 布尔逻辑包含或 | 从左到右 |
| && | 条件 AND | 从左到右 |
| || | 条件 OR | 从左到右 |
| ?: | 条件 | 从右到左 |
| = | 赋值 | 从右到左 |
| += | 加法赋值 |  |
| -= | 减法赋值 |  |
| *= | 乘法赋值 |  |
| /= | 除法赋值 |  |
| %= | 余数赋值 |  |
| &= | 位 AND 赋值 |  |
| ^= | 位异或赋值 |  |
| |= | 位包含或赋值 |  |
| <<= | 位左移赋值 |  |
| >>= | 位有符号右移赋值 |  |
| >>>= | 位无符号右移赋值 |  |

图 A.1 | 运算符优先级表。 （第 2 部分，共 2 部分。）

## ASCII 字符集

|  | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | nul | soh | stx | etx | eot | enq | ack | bel | bs | ht |
| 1 | nl | vt | ff | cr | so | si | dle | dc1 | dc2 | dc3 |
| 2 | dc4 | nak | syn | etb | can | em | sub | esc | fs | gs |
| 3 | rs | us | sp | ! | " | # | $ | % | & | ' |
| 4 | ( | ) | * | + | , | - | . | / | 0 | 1 |
| 5 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; |
| 6 | < | = | > | ? | @ | A | B | C | D | E |
| 7 | F | G | H | I | J | K | L | M | N | O |
| 8 | P | Q | R | S | T | U | V | W | X | Y |
| 9 | Z | [ | \ | ] | ^ | _ | ` | a | b | c |
| 10 | d | e | f | g | h | i | j | k | l | m |
| 11 | n | o | p | q | r | s | t | u | v | w |
| 12 | x | y | z | { | | | } | ~ | del |  |

图 B.1 | ASCII 字符集。

表左侧的数字是字符代码的十进制等价物（0–127）的左位数字，表顶部的数字是字符代码的右位数字。例如，字符 "F" 的字符代码为 70，而字符 "&" 的字符代码为 38。

本书的大多数用户对用于在许多计算机上表示英文字符的 ASCII 字符集感兴趣。ASCII 字符集是 Java 用于表示世界大多数语言字符的 Unicode 字符集的子集。有关 Unicode 字符集的更多信息，请参阅网页附录 N。

## 关键字和保留字

| Java 关键字 |
|---|---|
| abstract | assert | boolean | break | byte |
| case | catch | char | class | continue |
| default | do | double | else | enum |
| extends | final | finally | float | for |
| if | implements | import | instanceof | int |
| interface | long | native | new | package |
| private | protected | public | return | short |
| static | strictfp | super | switch | synchronized |
| this | throw | throws | transient | try |
| void | volatile | while |  |  |
| *当前未使用的关键字* |
| const | goto |  |  |  |

图 C.1 | Java 关键字。

Java 还包含保留字 true 和 false，它们是布尔字面量，以及 null，它是表示对无物的引用的字面量。与关键字一样，这些保留字不能用作标识符。

## 原始类型

| Type | Size in bits | Values | Standard |
|---|---|---|---|
| boolean |  | true or false
[Note: A boolean's representation is specific to the Java Virtual Machine on each platform.] |  |
| char | 16 | '\u0000' to '\uFFFF' (0 to 65535) | (ISO Unicode character set) |
| byte | 8 | -128 to +127 (-2^7 to 2^7 - 1) |  |
| short | 16 | -32,768 to +32,767 (-2^15 to 2^15 - 1) |  |
| int | 32 | -2,147,483,648 to +2,147,483,647 (-2^31 to 2^31 - 1) |  |
| long | 64 | -9,223,372,036,854,775,808 to +9,223,372,036,854,775,807 (-2^63 to 2^63 - 1) |  |
| float | 32 | Negative range:
-3.4028234663852886E+38 to
-1.4012984643248170e-45
Positive range:
1.4012984643248170e-45 to
3.4028234663852886E+38 | (IEEE 754 floating point) |
| double | 64 | Negative range:
-1.7976931348623157E+308 to
-4.94065645841246544e-324
Positive range:
4.94065645841246544e-324 to
1.7976931348623157E+308 | (IEEE 754 floating point) |

图 D.1 | Java 原始类型。

有关 IEEE 754 的更多信息请访问 grouper.ieee.org/groups/754/。有关 Unicode 的更多信息，请参阅附录 N。

## 使用 Java API 文档

### E.1 引言

Java 类库包含数千个预定义类和接口，程序员可用于编写自己的应用程序。这些类根据其功能分组到包中。例如，用于文件处理的类和接口被分组到 java.io 包中，而用于网络应用程序的类和接口被分组到 java.net 包中。Java API 文档列出了 Java 类库中每个类的公共和受保护成员以及每个接口的公共成员。文档概述了所有类和接口，总结了它们的成员（即类的字段、构造器和方法，以及接口的字段和方法）并提供了每个成员的详细描述。大多数 Java 程序员在编写程序时依赖于此文档。通常，程序员会搜索 API 以查找以下内容：

- 1. 包含特定类或接口的包。
- 2. 特定类或接口与其他类和接口之间的关系。
- 3. 类或接口常量——通常声明为 public static final 字段。
- 4. 构造器以确定如何初始化该类的对象。
- 5. 类的方法以确定它们是静态还是非静态，需要传递的参数数量和类型、返回类型以及方法可能抛出的任何异常。

此外，程序员经常依赖文档来发现他们以前未使用过的类和接口。出于这个原因，我们用大家熟悉的类和可能尚未研究的类来演示文档。我们展示如何使用文档来定位使用类或接口有效所需的信息。

### E.2 浏览 Java API

Java API 文档可以下载到本地硬盘或在线查看。要下载 Java API 文档，请访问 www.oracle.com/technetwork/java/javase/downloads/index.html/ 向下滚动到 Additional Resources 部分并点击 Java SE 6 Documentation 右侧的 Download Zip 按钮。您将被要求接受许可协议。为此，请点击 Accept，然后点击 Continue。点击 ZIP 文件的链接开始下载。下载文件后，您可以使用 WinZip（www.winzip.com）等程序提取文件。如果您使用的是 Windows，请将内容提取到 JDK 的安装目录。要在 Microsoft Windows 上本地硬盘中查看 API 文档，请在浏览器中打开 C:\Program Files\Java\YourJDKVersion\docs\api\index.html 页面。要在线查看 API 文档，请访问 download.oracle.com/javase/6/docs/api/ （图 E.1）。

![](img/009e962758dcc71dbc43a493362e6dc0_1408_0.png)

图 E.1 | Java API 概览。 （Courtesy of Oracle Corporation）

# Frames in the API Documentation’s index.html Page

API 文档分为三个框架（见图 E.1）。左上框架按字母顺序列出所有 Java API 的包。左下框架最初按字母顺序列出 Java API 的类和接口。接口名称以斜体显示。当您在左上框架中点击特定包时，左下框架列出所选包的类和接口。右框架最初提供 Java API 规范每个包的简要描述——阅读此概述以熟悉 Java API 的一般功能。如果您在左下框架中选择一个类或接口，右框架将显示有关该类或接口的信息。

# Important Links in the index.html Page

右框架顶部（图 E.1）有四个链接——Tree、Deprecated、Index 和 Help。Tree 链接以树状结构显示所有包、类和接口的层次结构。Deprecated 链接显示不应再使用的接口、类、异常、字段、构造器和方法。Index 链接显示类、接口、

