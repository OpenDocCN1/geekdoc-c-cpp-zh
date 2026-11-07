
## 写入带引号的文本

类似地，你可以将带引号的文本写入流。例如，如果 name 包含 Silvio Flores，则语句

```
outputStream << std::quoted(name);
```

会向 outputStream 写入

```
"Silvio Flores"
```

如果字符串包含 `"` 或 `\`，则它会显示为 `\"` 或 `\\`。

## 检查点

- **1.（填空）** 流操纵器 ________（头文件 `<iomanip>`）用于从流中读取带引号的文本。它会包含带引号文本中的任何空白字符，并丢弃双引号分隔符。**答案：** quoted。
- **2.（代码）** 编写一条语句，以带引号的形式输出字符串 "Nella Chirwa"。**答案：** `std::cout << std::quoted("Nella Chirwa");`

## 8.16 更新顺序文件

如第 8.13 节所示，格式化并写入顺序文件的数据无法就地修改，否则会有破坏文件中其他数据的风险。例如，如果需要将名字“Devi”改为“Manirakiza”，则旧名字不能在不损坏文件的情况下被覆盖。Devi 的记录写入文件后如下

```
300 Devi 0.00
```

如果使用较长的名字从文件中的同一位置开始重写该记录，则该记录会变成

```
300 Manirakiza 0.00
```

新记录比原记录多六个字符。“Manirakiza”中“i”之后的任何字符都会覆盖分隔名字与 0.00 的空格、值 0.00，以及文件中下一条顺序记录的开头。使用流插入运算符 << 和流提取运算符 >> 的格式化输入/输出模型的问题在于，字段——因而记录——的大小可能不同。例如，值 7、14、−117、2074 和 27383 都是 int，它们在内部存储相同数量的“原始数据”字节。然而，当作为格式化文本（字符序列）输出时，这些整数会根据其实际值变成大小不同的字段。因此，格式化输入/输出模型通常不用于就地更新记录。

这种更新可以用顺序文件完成，但很笨拙。例如，要在顺序文件中完成前面的名字更改，我们可以：

- 将 `300 Devi 0.00` 之前的记录复制到新文件，
- 将更新后的记录写入新文件，然后
- 将 `300 Devi 0.00` 之后的记录写入新文件。

然后我们可以删除旧文件并重命名新文件。这需要处理文件中的每条记录才能更新一条记录。不过，如果在文件的一次遍历中要更新许多记录，这种技术是可以接受的。

## 检查点

**（判断正误）** 格式化并写入顺序文件的数据无法就地修改，否则会有破坏文件中其他数据的风险。  
**答案：** 正确。

## 8.17 字符串流处理

除了标准流 I/O 和文件流 I/O 之外，C++ 还包含从内存中的字符串输入以及向内存中的字符串输出的功能。这些功能通常称为内存内 I/O 或字符串流处理。你可以使用 `istringstream` 从字符串读取，并使用 `ostringstream` 向字符串写入，二者都来自头文件 `<sstream>`。

类模板 `istringstream` 和 `ostringstream` 提供与类 `istream` 和 `ostream` 相同的功能，外加其他特定于内存内格式化的成员函数。`ostringstream` 对象使用一个字符串对象来存储输出数据。其 `str` 成员函数返回该字符串的副本。

字符串流处理的一个应用是数据验证。程序可以一次从输入流中读取一整行到字符串中。接下来，验证例程可以仔细检查字符串的内容，并在必要时更正（或修复）数据。然后，程序可以从该字符串输入，因为它知道输入数据格式正确。

为了协助数据验证，C++ 提供了强大的模式匹配正则表达式功能。例如，在需要美国格式电话号码（例如 (800) 555-1212）的程序中，你可以使用正则表达式来确认字符串是否匹配该格式。许多网站提供用于验证电子邮件地址、URL、电话号码、地址和其他常见数据类型的正则表达式。我们将在第 8.20 节介绍正则表达式并提供几个示例。

### 演示 ostringstream

图 8.12 创建一个 `ostringstream` 对象，然后使用流插入运算符将一系列字符串和数值输出到该对象。

```cpp
// Fig08_12.cpp
// Using an ostringstream object.
#include <iostream>
#include <sstream> // header for string stream processing
#include <string>

int main() {
    std::ostringstream output; // create ostringstream object

    const std::string string1{"Output of several data types"};
    const std::string string2{"to an ostringstream object:"};
    const std::string string3{"\n double: "};
    const std::string string4{"\n   int: "};

    constexpr double d{123.4567};
    constexpr int i{2};

    // output strings, double and int to ostringstream
    output << string1 << string2 << string3 << d << string4 << i;

    // call str to obtain string contents of the ostringstream
    std::cout << "output contains:\n" << output.str();

    // add additional characters and call str to output string
    output << "\nmore characters added";
    std::cout << "\n\noutput now contains:\n" << output.str() << '\n';
}
```

```text
output contains:
Output of several data types to an ostringstream object:
double: 123.457
    int: 2

output now contains:
Output of several data types to an ostringstream object:
double: 123.457
    int: 2
more characters added
```

**图 8.12** | 使用 ostringstream 对象。

第 19 行将 string1、string2、string3、double d、string string4 和 int i 全部输出到内存中的 output。第 22 行显示 output.str()，它返回第 19 行由 output 创建的字符串。第 25 行通过简单地向 output 再发出一次流插入操作，将更多数据追加到内存中的字符串，然后第 26 行显示更新后的内容。

### 演示 istringstream

`istringstream` 对象从内存中的字符串输入数据。数据以字符形式存储在 `istringstream` 对象中。从 `istringstream` 对象输入的工作方式与从任何文件输入完全相同。字符串的末尾会被 `istringstream` 对象解释为文件结束。

图 8.13 演示从 `istringstream` 对象输入。第 9 行创建字符串 `inputString`，它由表示两个字符串（"Atonia" 和 "test"）、一个 `int`（123）、一个 `double`（4.7）和一个 `char`（'A'）的字符组成。第 10 行创建 `istringstream` 对象 `input`，并将其初始化为从 `inputString` 读取。第 17 行将 `inputString` 中的数据项读入变量 `s1`、`s2`、`i`、`d` 和 `c`，然后在第 19–20 行显示。接下来，我们在第 23 行再次尝试从 `input` 读取，但操作失败，因为 `inputString` 中没有更多数据可读。因此，`input` 对象求值为 false，`if...else` 语句的 `else` 部分执行。

```cpp
// fig08_13.cpp
// Demonstrating input from an istringstream object.
#include <format>
#include <iostream>
#include <sstream>
#include <string>

int main() {
    const std::string inputString{"Atonia test 123 4.7 A"};
    std::istringstream input{inputString};
    std::string s1;
    std::string s2;
    int i;
    double d;
    char c;

    input >> s1 >> s2 >> i >> d >> c;

    std::cout << "Items extracted from the istringstream object:\n"
              << std::format("{}\n{}\n{}\n{}\n{}\n", s1, s2, i, d, c);

    // attempt to read from empty stream
    if (long value; input >> value) {
        std::cout << std::format("\nlong value is: {}\n", value);
    }
    else {
        std::cout << std::format("\ninput is empty\n");
    }
}
```

```text
Items extracted from the istringstream object:
Atonia
test
123
4.7
A

input is empty
```

**图 8.13** 演示从 istringstream 对象输入。

## 检查点

- **1.（填空）** C++ 包含从内存中的字符串输入以及向内存中的字符串输出的功能。这些功能通常称为内存内 I/O 或 ________。**答案：** 字符串流处理。
- **2.（填空）** ________ 和 ________ 提供与 `istream` 和 `ostream` 相同的功能，外加其他特定于内存内格式化的成员函数。**答案：** `istringstream`、`ostringstream`。
- **3.（讨论）** 解释字符串流处理如何用于数据验证。**答案：** 程序可以一次从输入流中读取一整行到字符串中。接下来，验证例程可以仔细检查字符串的内容，并在必要时更正（或修复）数据。然后，程序可以从该字符串输入，因为它知道输入数据格式正确。
