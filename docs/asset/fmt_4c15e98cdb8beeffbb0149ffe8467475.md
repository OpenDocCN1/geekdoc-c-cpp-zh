
`typedef char *CardPtr;`

使用 `typedef` 定义了别名 `Card`，作为类型 `Card*` 的同义词。使用 `typedef` 创建新类型并不会创建一个数据类型；它只创建一个新名称。第 10.6 节详细讨论了 `typedef`。同样，`typedef iostream` 代表 `basic_istream<char>`，它启用 `char` 输出。实际上，`typedef iostream` 代表 `basic_iostream<char>`，它同时启用 `char` 输入和输出。我们在整个章节中都会使用这些 `typedef`。

## 流-I/O 模板层次结构和运算符重载

模板 `basic_istream` 和 `basic_ostream` 通过单继承派自基类 `basic_ios`。模板 `basic_iostream` 通过多继承派自模板 `basic_istream` 和 `basic_ostream`。图 21.1 的 UML 类图总结了这些继承关系。

![](img/fa81e30d8bce030c9060826ba9997d7b_848_0.png)

图 21.1 | 流-I/O 模板层次结构部分。

运算符重载为执行输入/输出提供了方便的表示法。左移运算符 (`<<`) 被重载用于指定流输出，被称为流插入操作符。右移运算符 (`>>`) 被重载用于指定流输入，被称为流提取操作符。这些运算符与标准流对象 `cin`、`cout`、`cerr` 和 `clog` 一起使用，通常用于在你自己的代码中创建的流对象。

## 标准流对象 cin, cout, cerr 和 clog

预定义对象 `cin` 是一个流实例，被认为“连接到”（或附加到）标准输入设备（通常是键盘）。在以下语句中使用的流提取操作符 (`>>`) 将整数变量 `grade` 的值（假设 `grade` 已被声明为 `int`）从 `cin` 输入到内存：

```cpp
cin >> grade; // 数据沿箭头方向“流动”
```

编译器确定 `grade` 的数据类型并选择合适的重载流提取操作符。假设 `grade` 已正确声明，流提取操作符不需要额外的类型信息（例如在 C 风格的 I/O 中所示）。`>>` 运算符重载用于输入基本类型的数据项、字符串和指针值。

预定义对象 `cout` 是一个流实例，被认为“连接到”标准输出设备（通常是显示器）。在以下语句中使用的流插入操作符 (`<<`) 将变量 `grade` 的值输出到标准输出设备：

```cpp
cout << grade; // 数据沿箭头方向“流动”
```

编译器确定 `grade` 的数据类型（假设 `grade` 已正确声明）并选择合适的流插入操作符。`<<` 运算符重载用于输出基本类型的数据项、字符串和指针值。

- 预定义对象 `cerr` 是一个流实例，被认为“连接到”标准错误设备（通常是屏幕）。`cerr` 的输出是不缓冲的，这意味着每次流插入 `cerr` 都会导致输出立即——这适用于通知用户。
- 预定义对象 `clog` 是一个流实例，被认为“连接到”标准错误设备。`clog` 的输出是缓冲的。这意味着每次流插入 `clog` 都会导致输出保持，直到缓冲区刷新。

## 文件处理 (File-Processing)

C++ 使用类模板。例如，`basic_istream` 类支持流输入操作，`basic_iostream` 类支持流输入和流输出操作。每个模板都有一个定义的模板特化版本，用于启用 `char` I/O。此外，iostream 库提供了一组 `typedef`，为这些模板特化版本提供了别名。`typedef` 指定了数据类型的别名。你将使用 `typedef` 创建更短或更具读性的类型名称。例如：

```cpp
typedef char *CardPtr;
```

使用 `typedef` 定义了别名 `Card`，作为类型 `Card*` 的同义词。使用 `typedef` 创建新类型不会创建一个数据类型；它只创建一个新名称。第 10.6 节详细讨论了 `typedef`。同样，`typedef iostream` 代表 `basic_istream<char>`，它启用 `char` 输出。实际上，`typedef iostream` 代表 `basic_iostream<char>`，它同时启用 `char` 输入和输出。我们在整个章节中都会使用这些 `typedef`。

## 21.3 输出 (Stream Output)

`ostream` 提供了格式化和非格式化的输出能力。能力包括：
- 使用流插入操作符 (`<<`) 输出标准类型；
- 通过 `put` 函数输出字符；
- 通过 `write` 函数输出非格式化；
- 以进制、八进制和十六进制输出整数；
- 以各种精度、强制小数点、科学计数法和固定格式输出浮点值；
- 在指定宽度的字段中输出数据；
- 输出大写字母。

### 21.3.1 char* 变量输出

C++ 自动确定数据类型——这是对 C 的改进。例如，假设我们想要打印存储在 `char` 指针中的地址。`<<` 运算符被重载用于将 `char*` 输出为 `void`。要输出地址，可以将 `char*` 强制转换为 `void`。图 21.3 展示了如何以字符串和地址格式打印 `char*`。

```cpp
// fig21_03.cpp
// 在 char* 变量中存储地址。
#include <iostream>
using namespace std;
int main() {
    const char *const word = "again";
    // 在强制转换为 void 后
    // 显示 char* 的值
    cout << "Value of word is: " << word << endl;
    cout << "Value of static_cast<void *>(word) is: " << static_cast<void>(word) << endl;
} // main 结束
```

| Value of word is: again |
| Value of static_cast<void *>(word) is: 0135CC70 |

**图 21.3** 在 char* 变量中输出。

### 21.3.2 使用成员函数 put 输出

我们可以使用成员函数输出字符。例如，语句：

```cpp
cout.put('A');
```

显示单个字符 A。`put` 的调用可以是级联的，如语句所示：

```cpp
cout.put('A').put('\n');
```

输出字母 A 紧跟一个换行符。通过 `<<`，前面的状态以这种方式执行，因为点运算符 (`.`) 从左到右关联。

## 21.4 流输入

`put` 成员函数返回接收 `put` 调用的 ostream 对象 (`cout`) 的引用。`put` 函数也可以带有一个空表达式调用，该表达式表示一个 ASCII 值，如下句所示，它将输出 A：

```cpp
cout.put( 6 );
```

现在让我们考虑流输入。流（stream）提供了格式化输入和非格式化输入的能力。流提取操作符 `>>` 通常会跳过输入流中的空白字符（如空格、制表符和换行符）；我们稍后将看到如何更改这种行为。在输入之后，流提取操作符返回接收到的流对象的引用（例如 `cin >> grade` 中的 `cin`）。如果将引用用作条件（例如在 `while` 语句的循环继续条件中），流的重载的*布尔*（`*`）类型转换运算符被隐式调用，根据成功与否将引用转换为非空指针或 `false`。非空指针转换为 `bool` 类型 `true` 表示成功，空指针则转换为 `bool` 类型 `false` 表示失败。当尝试读取流的末尾时，流的重载的*布尔*类型转换运算符返回指向文件结束（EOF）的空指针。

每个对象包含一组状态位，用于控制流的状态（即格式化、错误状态等）。这些状态位用于流的重载的*布尔*类型转换运算符以判断返回非空指针还是空指针。如果输入了错误的类型，流提取会导致 `failbit` 被设置；如果操作失败，则会导致流的 `badbit` 被设置。第 21.7 节和 21.8 节详细讨论了状态位，现在展示如何在 I/O 操作后测试这些状态位。

### 21.4.1 get 和 get-line 成员函数

不带参数的 `get` 成员函数从指定的流中返回一个字符（包括空白字符和非图形字符，当键入序列返回文件结束时也是），并将其作为函数调用的值返回。当在流上遇到文件结束时，此版本返回 `eof`。

### 使用成员函数 eof, get 和 put

图 21.4 展示了在输入流上使用成员函数 `eof` 和 `get`，以及在输出流上使用成员函数 `put` 的用法。从第 4 章可知，EOF 表示为一个整数 `int`。程序将字符读入第一个变量 `character`，这样我们就可以测试每个提取器以查看它是否为 `eof()`。第一个程序在遇到文件结束（Windows 系统上按 `<Ctrl+z`，Mac 系统上按 `<D`）后按回车键，打印 `cin.eof()` 的值——即 `false`（输出为 0）。第 15 行读取每个字符，第 16 行使用成员函数 `put` 输出到 `cout`。当遇到文件结束时，结果为 `true`（输出为 1），这表示 `cin` 上设置了文件结束。程序使用了不带参数的 `istream` 成员函数版本，该版本返回正在输入的字符（第 15 行）。`eof()` 函数仅在程序读取超过流中的最后一个字符后才返回 `true`。

## 第 21 章 流输入/输出：深入探析

```cpp
// 图 21.4: fig21_04.cpp
// get, put 和 eof 成员函数。
#include <iostream>
using namespace std;
int main() {
    int character; // 使用 int，因为 char 不能表示 EOF
    // 提示用户输入一行文本
    cout << "输入行之前为 " << cin.eof() << endl;
    cout << "输入一个句子并加上文件结束：" << endl;
    // 使用 get 读取每个字符：使用 put 显示
    while ((character = cin.get()) != EOF) {
        put(character);
    }
    // 显示文件结束字符
    cout << "\n此系统中的 EOF: " << character << endl;
    cout << "输入 EOF 后，cin.eof() 为 " << cin.eof() << endl;
}
```

输入前，cin.eof() 为 0
输入一个句子并加上文件结束：
**测试 get 和 put 成员函数**
测试 get 和 put 成员函数
^Z

> 此系统中的 EOF: -1
输入 EOF 后，cin.eof() 为 1

**图 21.4** | get, put 和 eof 成员函数。

带有字符引用参数的成员函数从输入流中读取下一个字符（即使该字符是空格），并将其存储在字符参数中。此版本返回正在调用 `get` 成员函数的 `istream` 对象引用。
`get` 的一个版本接受三个参数——一个内置字符数组、一个大小限制和一个分隔符（默认值为 `'\n'`）。此版本从输入流中读取。它读取的字符数比指定的最大数量少一个，并在读取分隔符后立即终止。会插入一个空字符以终止缓冲区所用字符数组中的字符串。分隔符不会放置在字符数组中，但仍留在输入流中（分隔符将是下一个读取的字符）。因此，连续调用两次 `get` 的结果将是空行，除非从输入流中移除了分隔符（可能通过 `cin.ignore()`）。

## 比较 cin 和 cin.get

图 21.5 比较了使用 `cin` 进行输入提取（读取字符直到遇到空白字符）与使用 `cin.get` 进行输入。调用 `cin.get(line)`（第22 行）未指定分隔符，因此使用了默认的 `'\n'` 字符。

```cpp
// 图 21.5: fig21_05.cpp
// 对比通过 cin 和 cin.get 输入字符串
#include <iostream>
using namespace std;
int main()
{
    // 通过 cin 输入字符串 
    const int SIZE = 80; // 创建 80 字节数组
    char buffer[SIZE]; // 使用 cin 输入 buffer
    cout << "输入一个句子：" << endl;
    cin >> buffer;
    // 显示 buffer 内容
    cout << "读取的内容为：" << endl << buffer
    string line;
    cin.get(line); //    //2 getline 输入
    char buffer[SIZE]; // 使用 getline 输入 buffer
    cout << "输入一个句子：" << endl;
    cin.getline(buffer, SIZE);
    // 显示 buffer 内容
    cout << "读取的内容为：" << endl << buffer << endl;
} // 结束
```

输入句子：
通过 cin 和 cin.get 输入字符串

读取的内容为：
通过 cin 和 cin.get 输入字符串

### 使用 getline 成员函数

带有字符引用参数的成员函数从输入流中读取下一个字符（即使这是一个空格字符），并将其存储在字符参数中。此版本返回正在调用 `get` 成员函数的 `istream` 对象引用。
`get` 的一个版本接受三个参数——一个内置字符数组、一个大小限制和一个分隔符（默认值为 `'\n'`）。此版本从输入流中读取。它读取的字符数比指定的最大数量少一个，并在读取分隔符后立即终止。会插入一个空字符以终止缓冲区所用字符数组中的字符串。分隔符不会放置在字符数组中，但仍留在输入流中（分隔符将是下一个读取的字符）。因此，连续调用两次 `get` 的结果将是空行，除非从输入流中移除了分隔符（可能通过 `cin.ignore()`）。

## 21.6 流操纵符（Introduction to Stream Manipulators）

C++ 提供了各种流操纵符来执行任务。流操纵符提供了诸如设置字段宽度、设置精度、重置未设置的格式、设置字段填充字符、刷新流、在输出流中插入新换行符（刷新流）、在输出流中插入空字符以及在输入流中跳过空白字符等功能。这些功能将在接下来的章节中进行阐述。

### 21.6.1 整数流基数：dec, hex 和 setbase

整数通常被解释为十进制（10进制）值。要更改流上解释整数的基数，可以使用 `hex` 操纵符将基设置为十六进制（16进制），或使用 `oct` 操纵符将基数设置为八进制（8进制）。插入 `dec` 操纵符可以将基数重置为十进制。这些都是粘性（sticky）操纵符。

流的基数可以通过 `setbase` 流操纵符更改，它接受 10、8 或 16 作为参数，分别将基数设置为十进制、十六进制或八进制。因为 `setbase` 接受参数，所以它还需要包含 `<iomanip>` 头文件。流的基数在被显式更改之前会保持不变；`setbase` 是粘性的。图 21.8 展示了流操纵符 `hex`、`dec` 和 `setbase`。关于十进制、八进制和十六进制数字的更多信息，请参见附录 C。

```cpp
// Fig. 21.8: fig21_08.cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
    int number;
    cout << "Enter a decimal number: ";
    cin >> number;
    // 使用 hex 流操纵符显示十六进制数
    cout << " in hexadecimal is: " << hex;
    cout << number << endl;
    // 使用 oct 流操纵符显示八进制数
    cout << dec << number << " in octal is: "
    cout << oct << endl;
    // 使用 setbase 流操纵符显示十进制数
    cout << setbase(10) << number << " in decimal is: "
    cout << endl;
} // end main
```

![](img/fa81e30d8bce030c9060826ba9997d7b_856_0.png)

图 21.8 | 使用流操纵符 hex, oct, dec 和 setbase。

### 21.6.2 浮点精度（precision, setprecision）

我们可以通过使用 `setprecision` 流操纵符或 `ios_base` 的成员函数 `precision` 来控制浮点数的精度（即小数点右侧的位数）。对其中者的任何一个进行调用都会设置后续所有输出操作的精度，直到下一次精度设置调用为止。调用不带参数的成员函数会返回当前的精度设置（当你不再需要粘性设置并最终需要恢复原始精度时，这就是你需要使用的这种方法）。图 21.9 的程序使用了成员函数 `precision`（第 22 行）和 `setprecision` 操纵符（第 31 行）来打印一个表格，显示 2 的平方根，精度从 0 到 9 变化。

```cpp
// Fig 21.9: fig21_09.cpp
// 控制浮点数的精度。
#include <iostream>
```
