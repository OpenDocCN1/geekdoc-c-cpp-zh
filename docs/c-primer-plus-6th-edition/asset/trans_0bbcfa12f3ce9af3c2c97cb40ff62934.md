

## 3.2 C++ 转义序列代码

| 字符名称 | ASCII 符号 | C++ 代码 | ASCII 代码 | ASCII 十六进制代码 |
|---|---|---|---|---|
| 换行 | NL (LF) | \n | 10 | 0xA |
| 水平制表符 | HT | \t | 9 | 0x9 |
| 垂直制表符 | VT | \v | 11 | 0xB |
| 退格 | BS | \b | 8 | 0x8 |
| 回车 | CR | \r | 13 | 0xD |
| 警报 | BEL | \a | 7 | 0x7 |
| 反斜杠 | \ | \\ | 92 | 0x5C |
| 问号 | ? | \? | 63 | 0x3F |
| 单引号 | ' | \' | 39 | 0x27 |
| 双引号 | " | \" | 34 | 0x22 |

```
char alarm = '\a';
cout << alarm << "Don't do that again!\a\n";
cout << "Ben\\Buggsie\nwas here!\n";
```

最后一行产生以下输出：

Ben "Buggsie" Hacker
was here!

> 注意你将转义序列，如 \n，就像一个普通字符，如 Q 一样对待。也就是说，你用单引号将其包含起来以创建字符常量，并在将其作为字符串的一部分包含时不使用引号。
转义序列可以追溯到人们使用电传打字机，即机电式打字机-打印机与计算机通信的时代，而现代系统并不总是记住完整的转义序列集合。例如，一些系统对警报字符保持沉默。
换行提供了一种替代 endl 用于在输出中插入新行的替代方法。你可以在字符常量 ('\n') 中使用换行符或作为字符串中的字符 ("\n")。以下三种方法都会将屏幕光标移动到下一行的开头：

```
cout << endl; // using the endl manipulator
cout << '\n'; // using a character constant
cout << "\n"; // using a string
```

你可以在更长的字符串中嵌入换行符；这通常比使用 endl 更方便。例如，以下 cout << endl 产生相同的输出：

```
cout << endl << endl << "What next?" << endl << "Enter a number:" << endl;
cout << "\n\nWhat next?\n\nEnter a number:\n";
```

## 第 3 章 处理数据

当你显示一个数字时，endl 比 "\n" 或 '\n' 更容易输入，当你显示一个字符串时，以换行字符结束字符串需要更少的输入：

```
cout << x << endl;           // easier than cout << x << "\n"
cout << "Dr. X.\n";      // easier than cout << "The Dr. X." << endl;
```

最后，你可以通过字符的八进制或十六进制代码使用转义序列。例如，Ctrl+Z 的 ASCII 代码为 26，即八进制为 032，十六进制为 0xa。你可以用以下任一转义序列表示该字符：\032 或 \xa。你可以通过将其括在单引号中来创建这些常数，如 '\032'，并将其用作字符串的一部分，如 "hi\xa there"。

### 提示

当你选择使用数字转义序列或符号转义序列，如 \x8 与 \b 时，使用符号代码。数字表示与特定的代码（如 ASCII）绑定，但符号表示适用于所有代码并且更易读。

列表 3.7 演示了一些转义序列。它使用警报字符来引起你的注意，使用换行字符来推进光标（光标的一小步，光标的巨步），并使用退格字符将光标向左退回一个空格（Houdini 一次使用只有转义序列的哈德逊河的图片；他当然是一位伟大的艺术家。）

### 列表 3.7 bondini.cpp

```
// bondini.cpp -- using escape sequences
#include <iostream>
int main()
{
    using namespace std;
    cout << "\aHyperType\" is now activated!\n";
    cout << "\aEnter your agent code: \b\b\b\b\b\b";
    long code;
    cin >> code;
    cout << "\aYou entered " << code << "...\n";
    cout << "\aCode verified: Proceed with Plan Z!\n";
    return 0;
}
```

### 注意

某些系统可能会表现不同，例如将 \b 显示为小矩形而不是退格，或在退格时擦除，也许忽略 \a。

### 简单变量

当你在列表 3.7 中启动程序时，它会在屏幕上显示以下文本：

Operation "HyperType" is now activated!
Enter your agent code: _________

打印下划线字符后，程序使用退格字符将光标退回到第一个下划线。你可以输入你的秘密代码并继续。以下是完整运行：

Operation "HyperType" is now activated!
Enter your agent code:42007007
You entered 42007007...
Code verified! Proceed with Plan Z!

### 通用字符名

C++ 实现支持基本源字符集——即你可以使用标准美国键盘编写的字符集，C 语言中的符号，如 { 和 =，以及空格字符等一些其他字符。有基本执行字符集，其中包括程序执行期间可以处理的字符（例如，从文件读取或在屏幕上显示的字符）。这增加了一些字符，如退格和警报。C++ 标准还允许实现扩展源字符集和扩展执行字符集。此外，可以将作为字母的额外字符用作标识符名称的一部分。德国实现可能允许你使用带变音符号的元音，法国实现可能允许你使用带重音的元音。C++ 有一种独立于任何特定键盘的表示国际字符的机制：使用通用字符名。

使用通用字符名类似于使用序列。通用字符名以 \u 或 \U 开头。\u 形式后跟 4 个十六进制数字，\U 形式后跟 8 个十六进制数字。这些数字表示该字符的 ISO 10646 代码点。 （ISO 10646 是一个正在开发的国际标准，为各种字符提供数字代码。使用“Unicode 和 ISO 10646”，在本章中。）

如果你的实现支持扩展字符，你可以在标识符中、作为字符常量以及在字符串中使用通用字符名。例如，考虑以下代码：

```
int k\u00F6rper;
cout << "Let eat g\u00E2teau.\\n";
```

ISO 10646 代码点 ö 为 00F6，å 的代码点为 00E2。因此，此 C++ 代码将变量名设置为 Körper 并显示以下输出：

Let them eat gâteau.

## 第 3 章 处理数据

如果你的系统不支持 ISO 10646，它可能会为 á 显示其他字符，也许只是简单地显示单词 gu00E2teau。

实际上，从可读性的角度来看，使用 ö 作为变量名的一部分并没有什么意义，但如果实现包含扩展字符集中的 δ 字符，也会允许你从键盘输入该字符。

请注意，C++ 使用术语“通用代码名”，而不是“通用代码”。这是因为构造如 ö 应被视为标签，意思是“Unicode 代码点是 U-00F6”。符合标准的 C++ 编译器将识别此 00F6，就像字符 '´ 字符一样，没有要求内部编码为 ASCII，在一台计算机上和在另一台计算机上使用不同的编码系统，ö 字符可以在不同系统上具有不同的编码。你的源代码可以在所有系统上使用通用代码名，并且编译器将以特定系统使用的适当代码表示它。

### Unicode 和 ISO 10646

Unicode 通过为大量字符和符号提供标准编号来解决各种字符集的表示问题，按类型分组它们。例如，ASCII 代码被并入 Unicode 的子集，因此 U. 拉丁字符如 A 和 Z 在两种系统下的表示相同。但 Unicode 还包含其他拉丁字符，如欧洲语言中使用的字符；来自其他字母表的字符，包括希腊语、西里尔语、希伯来语、切罗基语、阿拉伯语、泰语和孟加拉语；表意文字，如中文和日文。Unicode 表示超过 109,000 个符号和超过 90 种脚本，并且仍在开发中。如果你想知道，你可以查看 Unicode 联盟的网站，网址为 www.unicode.org。

Unicode 为其每个字符分配一个数字，称为代码点。Unicode 代码点的典型表示如下：U-222B。U 标识为 Unicode 字符，222B 是该字符的十六进制数字——在本例中为积分符号。

国际标准化组织（ISO）成立了一个工作组来开发 ISO 10646，作为多语言文本的标准。ISO 10646 小组和 Unicode 小组自 1991 年以来一直共同努力，使他们的标准保持同步。

### signed char 和 unsigned char

与 int 不同，char 默认不是有符号的。也不是默认无符号的。选择留给 C++ 实现，以便编译器最好地适应硬件属性。如果必须知道 char 有特定的行为，你可以显式地使用 signed char 或 unsigned char 作为类型：

```
char fodo; // may be signed
unsigned char bar; // definitely unsigned
signed char snark; // definitely signed
```
