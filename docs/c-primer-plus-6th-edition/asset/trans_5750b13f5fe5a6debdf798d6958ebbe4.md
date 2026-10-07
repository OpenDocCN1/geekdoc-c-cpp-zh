

## 第3章 处理数据

程序将一个短变量（sam）和一个无符号短变量（sue）都设置为最大的 short 值，在我们的系统上该值为 32,767。它对每个值加 1。这对 sue 来说会出问题，因为新值仍然远小于无符号整数的最大值。但 sam 从 32,767 变为 -32,768。同样，从 0 减 1 对 sam 来说不会有问题，但会使无符号变量从 0 变为 65,535。正如你所见，这些整数的行为就像一个里程表。如果你超过了限制，值就会从范围的另一端重新开始（见图 3.1）。C++ 保证无符号类型以这种方式表现。然而，C++ 并不能保证有符号整数类型在超出其限制（溢出和下溢）时不会抱怨，但这是实现中最常见的行为。

![](img/cd111a87c1db9aff4db4b18834327463_90_0.png)

图 3.1 整数的典型溢出行为。

### 选择整数类型

在 C++ 丰富的整数类型中，你应该使用哪一种？通常，int 被设置为目标计算机最“自然”的整数大小。自然大小指的是计算机处理最有效率的整数形式。如果没有令人信服的理由选择其他类型，你应该使用 int。

现在来看你可能想要使用其他类型的理由。如果一个变量表示永远不会为负的东西，例如文档中的单词数，你可以使用无符号类型；这样变量可以表示更大的值。

如果你知道变量可能需要表示的值对于 16 位整数来说太大，你应该使用 long。这即使在你的系统上 int 为 32 位时也成立。这样，如果你将程序转移到一个 int 为 16 位的系统上，你的程序就不会因为突然无法正常工作而让你尴尬（见图 3.2）。而且如果仅仅十亿对你的需求来说不够，你可以升级到 long long。

```
// myprofit.cpp
...
int receipts = 560334;
long also = 560334;
cout << receipts << "\n";
out << also << "\n";
...
```

```
// myprofit.cpp
...
int receipts = 560334;
long also = 560334;
cout << receipts << "\n";
out << also << "\n";
...
```

![](img/cd111a87c1db9aff4db4b18834327463_91_0.png)

Type int worked on this computer. Type int failed on this computer.

图 3.2 为了可移植性，请对大整数使用 long。

使用 short 可以在 short 比 int 小时节省内存。最典型的是，这只有在你有一个很大的整数数组时才重要。（数组是一种数据结构，它按顺序在内存中存储多个相同类型的值。）如果节省空间很重要，你应该使用 short 而不是 int，即使它们大小相同。举例来说，假设你将程序从 16 位系统移动到 32 位 int 系统。这会使保存 int 数组所需的内存量翻倍，但不会影响 short 数组的需求。记住，节省一位就是赚到。

如果你只需要一个字节，可以使用 char。我们很快就会研究这种可能性。

### 整数字面量

整数字面量或常量是你明确写出的，例如 212 或 1776。C++，像 C 一样，让你用三种不同的数字进制书写整数：基数 10（公众最爱）、基数 8（Unix 最爱）和基数 16（硬件黑客的最爱）。附录 A“数字进制”描述了这些进制；在这里我们将看 C++ 的表示法。C++ 使用数字常量的第一个或前两个数字来识别其进制。如果第一个数字在 1–9 范围内，数字为 10（十进制）；因此 9 为 10。如果第一个数字为 0 或 0A，数字在 1–7 范围内（八进制）；因此 8 为八进制。042 为八进制和 0xA（十六进制）；因此前两个字符为 0x 或 0X，基数为 16。字符 a–f 和 A–F 表示对应值 10–15 的十六进制数字。01F 为 15 而 0xA5 为 65（十六加五）。列表 3.3 特意用来展示三种进制。

### 列表 3.3 hexoct1.cpp

```
// hexoct1.cpp -- shows hex and octal literals
#include <iostream>
int main() {
    using namespace std;
    int chest = 42; // decimal integer literal
    int waist = 0xa2; // hexadecimal integer literal
    int inseam = 042; // octal integer literal

    cout << "Monsieur cuts a striking figure!\n";
    cout << "chest = " << chest << " (42 in decimal)\
";
    cout << "waist = " << waist << " (0xa2 in hex)\
";
    cout << "inseam = " << inseam << " (042 in octal)\
";
    return 0;
}
```

默认情况下，cout 以十进制格式显示整数，而不论它们在程序中如何书写，如下输出所示：

Monsieur cuts a striking figure!
chest = 42 (42 in decimal)
waist = 66 (0xa2 in hex)
inseam = 34 (042 in octal)

请记住，这些记法只是名义上的便利。例如，如果你属于一个复古 PC 俱乐部并读到 CGA 内存系统是 B000 十六进制，你不必在程序中使用它之前将该值转换为基数 10 的 45,056。相反，你可以直接使用 0xB000。但无论你将值写成 10、012 还是 0xA，它在计算机中存储的方式都是二进制（基数 2）值。

顺便说一下

### 列表 3.4 hexoct2.cpp

```
// hexoct2.cpp -- display values in hex and octal
#include <iostream>
using namespace std;
int main() {
    using namespace std;
    int chest = 42;
    int waist = 42;
    int inseam = 42;

    cout << "Monsieur cuts a striking figure!" << endl;
    cout << "chest = " << chest << " (decimal for 42)" << endl;
    cout << hex << " // manipulator for changing number base
    cout << "waist = " << waist << " (hexadecimal for 42)" << endl;
    cout << oct << " // manipulator for changing number base
    cout << "inseam = " << inseam << " (octal for 42)" << endl;
}
```

列表 3.4 的程序输出如下：

Monsieur cuts a striking figure!
chest = 42 (decimal for 42)
waist = 2a (hexadecimal for 42)
inseam = 52 (octal for 42)

请注意，像下面这样的代码不会在屏幕上显示任何内容：

```
cout << hex;
```

相反，它会改变 cout 显示整数的方式。操纵符 hex 实际上是向 cout 发出的消息，告诉它如何行为。另外请注意，因为标识符 hex 是 std 命名空间的一部分并且程序使用了命名空间，因此该程序不能将 hex 用作变量名。但是，如果你省略了 using 指令而改用 std::cout、std::endl、std::hex 和 std::oct，你仍然可以用普通的 hex 作为变量名。

### C++ 如何决定常量的类型

程序的声明告诉 C++ 编译器编译特定整数变量的类型。但常量的情况如何呢？也就是说，假设你在程序中使用常量表示一个数字：

```
cout << "Year = " << 1492 << "\n";
```

程序将 1492 存储为 int、long 还是其他类型？答案是，除非有理由另行处理，否则 C++ 将整数常量存储为 int。有两个这样的理由是你使用特殊后缀来指示特定类型，或者如果一个值太大而无法作为 int。

首先，看后缀。这些是放在数字常量末尾的字母，以指示类型。整数上的 l 或 L 后缀表示该整数是 long 常量，u 或 U 后缀表示无符号 int，ul 或 UL（以任何大小写组合）表示无符号 long。（因为小写 l 可能看起来很像数字，所以你应该使用大写 L）。例如，在使用 16 位 int 和 32 位 long 的系统上，数字 22022 作为 int 存储在 16 位中。同样，22022LU 和 22022UL 是无符号 long。C++ 为 long long 提供 LL 和 U 后缀，以及 ULL 用于无符号 long long。

接下来，看大小。C++ 对十进制整数的规则与十六进制和八进制整数略有不同。（这里十进制基数 10，如十六进制基数 16；术语十进制并不一定意味着小数点。）没有后缀的十进制整数由能够容纳它的最小类型表示：int、long 或 long long。在使用 16 位 int 和 32 位 long 的计算机系统上，20000 表示为 int 类型，40000 表示为 long，而没有后缀的十六进制或八进制整数由能够容纳它的最小类型表示：unsigned int、unsigned long、unsigned long long 或 unsigned long long。同一计算机系统将 40000 表示为 long long，将十六进制值 0x9C40 表示为 unsigned int。十六进制经常用于表示内存地址，而内存地址本质上是无符号的。所以 unsigned int 比 long 更适合 16 位地址。

### char 类型：字符和小整数

是时候转向最后一个整数类型：char。正如你可能从其名称中知道的那样，char 类型设计用于存储字符，例如字母和数字字符。虽然存储数字对字符来说不是什么大问题，但存储字母是另一回事。编程语言通过使用数字代码来表示字母，采用了简单的方法。char 类型是另一种整数类型。它保证足够大以表示目标计算机系统的基本符号范围——所有字母、数字、标点等。在实践中，许多系统支持超过 128 种字符，因此一个字节可以表示整个范围。虽然 char 最常用在处理字符时，但你也可以将其用作通常小于 short 的整数类型。

