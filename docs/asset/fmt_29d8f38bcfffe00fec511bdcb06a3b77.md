
编译器确定 `grade` 的类型（假设 `grade` 已正确声明）并选择流插入运算符。

预定义对象 `cerr` 是一个 `ostream` 对象，被认为“连接到”标准错误设备（通常是屏幕）。`cerr` 输出是不过滤的，意味着每次插入 `cerr` 立即输出——这适用于通知用户错误。

预定义对象 `clog` 是一个 `ostream` 类，被认为“连接到”标准错误设备。`clog` 输出是缓冲的，意味着每次插入 `clog` 将输出到缓冲区（即内存中的一个区域），直到缓冲区满或刷新。缓冲是操作系统课程中讨论的 I/O 性能增强技术。

## 13.3 流输出

格式化和未格式化输出由 `ostream` 提供。能力包括使用流插入运算符 `<<` 输出标准类型；通过 `put` 函数输出字符；通过 `write` 成员函数进行未格式化输出；以十进制、八进制和十六进制格式输出整数；以可变精度、科学计数（例如 `1.234567e-03`）和固定计数（例如 `0.00123457`）输出浮点值；在指定宽度字段中输出数据；使用指定字符填充字段；在科学计数和十六进制法中输出大写字母。我们将在本章演示所有这些能力。

### 13.3.1 char* 变量的输出

C++ 自动确定类型——这是一种改进，但此功能有时会产生干扰。例如，我们想要输出 `char*` 指针存储的地址。`<<` 运算符已重载为将 `char*` 作为空结尾 C 风格字符串输出。要输出地址，可以将 `char*` 转换为 `void*`（可以转换为任何指针）。图 13 展示了如何以字符串和地址格式打印 `char*` 变量。地址以十六进制（十二进制）数字打印——通常情况下，地址打印取决于实现。要了解更多关于十六进制

* 1. 本章仅讨论 iostream 库针对 char I/O 的模板特化。
* 2. （此处原文截断，未完整显示）

关于数字，请参见附录 D，“数系统”。我们在第 13.6.1 节和 13.7.4 节中详细介绍了如何控制数字进制。

```cpp
// Fig. 13.1: Fig13_01.cpp
// 打印存储在 char 变量中的地址。
#include <iostream>
using namespace std;
int main() {
    const char* word("again\n");
    // 显示 char* 变量的值，然后显示
    // 转换为 void* 后 word 的值
    cout << "Value of word: " << word
         << static_cast<const void*>(word) << endl;
}
```

Value of word is:
Value of static_cast<const void*>(word) is: 00E8BE30

**图 13.1** 打印存储在 char 变量中的地址。

### 13.3.2 使用成员函数输出字符

`basic_ostream` 成员函数一次输出一个字符。例如，语句语句

```cpp
cout.put('A');
```

显示单个字符 A。对 `put` 的调用可以级联，如语句

```cpp
cout.put('A').put('\n');
```

输出字母 A 后紧跟一个换行符。与 `<<` 一样，前面的状态按这种方式执行，点运算符（.）从左到右关联，并且 `put` 函数返回接收 `put` 值的 ostream 对象（cout）的引用。`put` 函数也可以用表示 ASCII 值的数值表达式调用，如下语句所示，它也会输出 A：

```cpp
cout.put(65);
```

## 13.4 流输入

`istream` 提供了格式化和非格式化的输入能力。流提取运算符（`>>`）通常会跳过输入流中的空白字符（如制表符和换行符）；稍后我们将看到如何更改这种行为。

*将流提取的结果作为条件使用*

在每次输入后，流提取运算符都会返回接收提取消息的流对象的引用（例如 `cin >> grade`）。如果该引用被用作条件（例如在 `while` 语句的循环继续条件中），流的重载 `bool` 运算符函数（在 C++11 中添加）会被隐式调用，根据最后一次输入操作的成功或失败分别将引用转换为 `true` 或 `false` 值。当尝试读取流的结尾时，流的重载 `bool` 运算符返回 `false` 表示文件结束。我们在图 5.11 的第 24 行使用了这一功能。

### 13.4.1 get 和 getLine 成员函数

不带参数的 `get` 函数从指定的流中读取一个字符（包括空白字符和其他非图形字符，作为返回文件结束的键序列），并将其作为函数调的值返回。此版本的 `get` 在流上遇到 `EOF` 时返回 `EOF`。`EOF` 通常值为 -1，定义在通过流头文件（如 `<iostream>`）间接包含在代码中的头文件中。

使用成员函数 eof, get 和 put

图 13.2 展示了输入流 `cin` 上的成员 `eof` 和 `get` 以及输出流 `cout` 上的成员函数。该程序使用 `get` 将字符读到 `int` 变量 `character` 中，以便我们可以测试每个字符是否是否为 `EOF`。我们使用它是因为许多 `plus char` 可以表示非负值，而 `EOF` 通常是 -1。程序首先打印 `cin.eof()` 的值——即在 0 处失败（在输出中），以显示 `cin` 尚未文件结束。用户输入一行文本并按下回车，然后在 Microsoft Windows 系统上按下文件结束 `<Ctrl+Z>`，在 Linux 和 Mac 系统上按下 `<Ctrl>d`。第 14 行读取每个字符，第 15 行使用成员函数输出到 `cout`。当遇到文件结束时，`while` 语句结束，第 20 行显示 `cin.eof()` 的值，现在为 `true`（输出为 1），以显示 `cin` 已设置文件结束。该程序使用了 `get` 成员函数。

```cpp
// Fig. 13.2: Fig13_02.cpp
// 使用 eof 和 get 成员函数。
#include <iostream>
using namespace std;
int main() {
    int character;
    cout << "cin.eof(): " << cin.eof() << endl;
    while ((character = cin.get()) != EOF) {
        cout << character;
    }
    cout << "\n.eof(): " << cin.eof() << endl;
}
```

# 第 13 章 流输入/输出：深入观察

输入一个句子：
使用 getline 成员函数
输入的句子是：
使用 getline 成员函数

图 13.4 | 使用 cin 成员函数 getline 输入字符。（2 份 2 部分中的第 2 部分）

### 13.4.2 istream 成员函数，putback 和 ignore

istream 成员函数 `ignore`（你曾在第 10.5 节中首次使用过）用于丢弃字符。它接收两个参数：

- 指定数量的字符——默认值为 1——以及
- 一个用于停止忽略字符的定界符——默认定界符为 EOF。

该函数丢弃指定数量的字符，或者在输入流中遇到定界符时丢弃较少数量字符。

`putback` 成员函数将之前通过 `get` 获取的上一个字符放入流中。该函数对于扫描输入流以查找以特定字符开头的字段的应用程序非常有用。当输入该字符时，应用程序将该字符返回给流，以便该字符能包含在输入数据中。

`peek` 成员函数返回输入流中的下一个字符，但不将其从流中移除。

### 13.4.3 类型安全的 I/O

C++ 提供了类型安全的 I/O。`<<` 和 `>>` 运算符被重载以接受特定类型的数据项。意外的数据位会被设置，用户可以据此判断 I/O 操作是成功还是失败。如果 `<<` 和 `>>` 没有为用户定义的类型进行重载，而你尝试使用它们输入或输出该用户类型对象的内容，编译器将报告错误。这使得程序能够“保持受控”。我们将在第 13.8 节中讨论这一点。

## 13.5 使用 read 和 gcount 进行非格式化 I/O

非格式化输入/输出分别通过 `istream` 的 `read` 函数和 `ostream` 的 `write` 函数执行：`read` 将字节读取内存中预建的字符数组；`write` 从预建的字符数组写入字节。这些字节不会经过任何形式的格式化。例如，以下情况：

```
char buffer[]="HAPPY BIRTHDAY";
cout.write(buffer, 10);
```

输出 buffer 的前 10 个字节（包括任何空字符，如果有的话，这会导致 `cout` 和 `<<` 的输出终止）。

```
cout.write("ABCDEFGHIJKLMNOPQRSTUVWXYZ", 10);
```

`read` 成员函数将指定数量的字符输入到预建的字符数组中。如果读取字符少于指定数量，则设置 `failbit`。

## 13.6 流操纵符：深入观察

第 13.8 节展示了如何确定 `failbit` 是否被设置。成员函数 `gcount` 报告上一次输入操作读取的字符数。

图 13.5 展示了 `istream` 成员函数 `read` 和 `gcount`，以及 `ostream` 成员函数 `write`。程序通过 `read`（第 12 行）将 20 个字符（来自较长的输入序列）输入到数组 `buffer`，通过 `gcount`（第 16 行）确定输入的字符数量，并通过 `write`（第 16 行）输出 buffer 中的字符。

```
// Fig. 13.5: Fig13_05.cpp
// 使用 read, gcount 和 write 进行非格式化 I/O。
#include <iostream>
using namespace std;
int main() {
    const int SIZE[80];
    char buffer[SIZE]; // 创建 80 个字符的数组
    // 使用函数将字符读取到 buffer
    cout << "Enter a sentence:\n";
    cin.read(buffer, 20);
    // 使用函数 write 和 gcount 显示 buffer 字符
    cout << "\nThe sentence entered was:\n";
    cout.write(buffer, cin.gcount());
    cout << endl;
}
```

使用句子：
使用 read, write 和 gcount 成员函数
输入的句子是：
使用 read, write

图 13.5 | 使用 read, gcount 和 write 进行非格式化 I/O。

## 13.6 流操纵符：深入观察

正如你所见的，C++ 提供了各种流操纵符来执行格式化任务。流操纵符提供了如下功能：

- 设置字段宽度
- 设置精度
- 设置和取消格式状态
- 在字段中设置填充字符
- 刷新流
- 向输出流插入换行符（并刷新流）
- 向输出流插入空字符
- 跳过输入流中的空白字符

这些特征将在随后的章节中描述。

### 13.6.1 整数流基：dec, hex 和 setbase

整数被正常地解释为十进制（基 10）值。要更改流上解释整数的基数，插入 `hex` 操纵符将基数设置为十六进制（基 16），或插入 `oct` 操纵符将基数设置为八进制（基 8）。`dec` 操纵符将流重置为十进制。这些是“粘性”（sticky）操纵符。

流基也可以通过 `setbase` 操纵符（头文件 `<iomanip>`）更改，它接受一个整数参数 10、8或16，分别将基数设置为十进制、八进制或十六进制。这些设置是粘性的。图 13.6 展示了这一点。

```
// Fig. 13.6: Fig13_06.cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    int n = 25;
    cout << "Enter an integer: ";
    cin >> n;
    cout << hex << n << " (hexadecimal)" << endl;
    cout << oct << n << " (octal)" << endl;
    cout << dec << n << " (decimal)" << endl;
    return 0;
}
```

### 13.6.2 浮点精度：precision, setprecision

我们可以使用 `precision` 操纵符或 `setprecision` 来控制浮点数的精度（即小数点右侧的位数）。在下一次调用 `precision` 之前，`setprecision` 的设置一直有效。图 13.7 展示了这一点。

```cpp
// Fig. 13.7: Fig13_07.cpp
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;
int main() {
    double val;
    cout << "Enter a number: ";
    cin >> val;
    cout << setprecision(3) << val << endl;
    cout << setprecision(5) << val << endl;
    return 0;
}
```

### 13.6.3 字段宽度：width, setw

`width` 成员函数（属于 `istream` 和 `ostream` 类）设置字段宽度（即应输出的字符位置数或应输入的最大字符数），并返回之前的字段宽度。如果输出窄于字段，将插入填充字符。如果值大于指定的宽度，则不会被截断——完整的数字将被打印。不带参数的 `width` 函数返回当前设置。`setw` 操纵符也可用于设置字段宽度。

图 13.8 展示了用于输入和输出的 `width` 成员函数。输入到字符数组时，读取的字符最多少于宽度，因为为输入字符串中的空字符留了位置。记住，字符串提取在遇到非领先空白时终止。`setw` 操纵符也可以用于设置字段宽度。（注意：在图 13.8 中，我们是手动设置。）

```cpp
// Fig. 13.8: Fig13_08.cpp
#include <iostream>
using namespace std;
int main() {
    int widthValue{4};
    char sentence[10];
    cout << "Enter a sentence:\n";
    cin.width(5); // 从句子输入5个字符
    // 设置字段宽度，然后根据该宽度显示字符
    while (cin >> sentence) {
        cout.width(widthValue++);
        cout << sentence << "\n";
        cin.width(5); // 再从句子输入5个字符
    }
}
```

图 13.8 | istream 和 ostream 类的 width 成员函数。（2 份 2 部分中的第 1 部分。）

## 13.6 流操纵器：深入探究

```
Enter a sentence:
This is a test of the width function
This
is
a
test
of
the
widt
hh
memb
er
func
c
```

图 13.8 | width。类 istream 和 ostream 类的自定义输出流操纵器。（2 部分部分中的第 2 部分。）

### 13.6.4 自定义输出流操纵器

你可以创建自己的流操纵器。图 13.9 显示了如何创建和使用新的非参数流操纵器 `bell`（第8–10 行）、`carriageReturn`（第13–15 行）、`tab`（第18–20 行）和 `endl`（第24–26 行）。对于输出流操纵器，返回类型和参数必须是 `ostream&` 类型。当第 30 行将 `endl` 插入输出流时，会调用 `endLine`，第 25 行输出转义序列 `\n` 和 `flush` 操纵器（它会刷新缓冲区）到标准输出流。同样，当第 31–39 行在输出流中插入操纵器 `tab` 和 `carriageReturn` 时，它们对应的函数 `tab`、`bell` 和 `carriageReturn` 被调用，继而输出转义序列。

```cpp
// Fig.13.9: Fig13.cpp
// 创建并测试自定义的非参数化
// 流操纵器。
#include <iostream>
using namespace std;
// bell 操纵器（使用转义序列 \a）
stream& bell(ostream& output) {
    return output << '\a'; // 发出系统蜂声
}
// carriageReturn 操纵器（使用转义序列 \r）
stream& carriageReturn(ostream& output) {
    return output << '\r'; // 发出回车
}
// tab 操纵器（使用转义序列 \t）
stream& tab(ostream& output) {
    return output << '\t'; // 输出制表符
}
```

图 13.9 | 创建和测试自定义的非参数化流操纵器。（2 部分部分中的第 1 部分。）

## 第 13 章 流输入输出：深入探究

```cpp
22 // endLine 操纵器（使用转义序列 \n 和 flush 流
```
