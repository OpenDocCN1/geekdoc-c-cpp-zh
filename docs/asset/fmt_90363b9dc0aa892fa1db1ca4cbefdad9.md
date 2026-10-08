
## 单个字符与字符串

C++ 区分了单个字符（`char`）和字符串（`string`）。这很大程度上取决于你使用单引号还是双引号。

表达式 `'A'` 表示单个字符。在编译期间，C++ 会将此表达式替换为字母 `'A'` 的 ASCII 值，该值恰好是十进制的 65。

## 第 8 章 字符串：分析文本

另一方面，表达式 `"A"` 表示一个长度为 1 的字符串。当 C++ 看到这个表达式时，它会在数据区域中放置两个字节：

- 字母 `'A'` 的 ASCII 码，如前所示。
- 一个空终止字节。

C++ 编译器会将表达式 `"A"` 替换为此双字节数组的地址。`'A'` 和 `"A"` 是不同的，因为一个是字符，另一个是字符串。

## 示例 8.4 使用 `strtok` 拆分输入

当你读取一行时，通常需要将其拆分为子字符串。例如，考虑这个 199

假设你想将其拆分成更小的字符串。使用 `strtok` 有两种方法：

| 函数用法 | 描述 |
|---|---|
| `strtok(source_string, delimiters)` | 返回字符串的第一个令牌。 |
| `strtok(nullptr, delimiters)` | 使用已指定的字符串。 |

第一次使用 `strtok` 时，要指定字符串和分隔符。它找到第一个令牌（子字符串），如果有，并返回指向它的指针。例如：

```cpp
p = strtok(the_string, " ");
```

此后调用 `strtok` 并对第一个参数传递空值；它返回字符串的下一个令牌。

```cpp
p = strtok(nullptr, " ");
```

如果你再次指定 *source_string*，`strtok` 将从头开始并返回第一个令牌。

函数的返回值通常是令牌的指针；但如果没有更多可读的令牌（子字符串），`strtok` 将返回空值，可以对其与零或假进行相等测试。

如果你使用的编译器是几年前的，可能需要用 `NULL` 替 `nullptr`。该关键字自 C++11 以来一直是规范的一部分。

## 第 8 章 字符串：分析文本

这是一个简单的程序，它将空格、逗号作为分隔符（分隔字符），并将每个子字符串（每个令牌）单独打印一行：

```cpp
tokenize.cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    char the_string[81], *p;
    cout << "Input a string to parse: ";
    cin.getline(the_string, 81);
    p = strtok(the_string, " ");
    while (p != nullptr) {
        cout << p << endl;
        p = strtok(nullptr, " ");
    }
    return 0;
}
```

# C++ 字符串类

```cpp
p = strtok(nullptr, " , ");
```

返回 `Nullptr` 值意味着“没有剩余的可读标记（tokens）”。

## 练习题

- **练习 8.4.1.** 修改示例，使程序在每行打印标记（子字符串）的同时，还打印一条语句，告知发现了多少个标记。
- **练习 8.4.2.** 将所有标记用和符号 (&) 隔开重新组合在一起。打印结果。
- **练习 8.4.3.** 使用和符号 (&) 作为分隔符。

# C++ 字符串类

在 C 和 C++ 中使用的以空字符结尾的字符串被称为 C 字符串（C-strings）。它们并不像 Visual Basic 提供的内置字符串那样方便，后者会向你隐藏几乎所有的实现细节。

多年来，几乎所有的 C++ 编译器都提供了一个类似的类型，其极具创意的名称是 `string`。（从技术上说，这个 C++ 类型的名称是 `std::string`，但如果你包含了 `using namespace` 语句，就不需要使用 `std::` 前缀了。）

`string` 是类的一个示例，而单个字符串都是对象，就像 `cin` 和 `cout` 一样。例如，假设你有两个标记为 `first_name` 和 `last_name` 的字符串：

```cpp
#include <string>
using namespace std;
...
string first_name("Abe ");
string last_name("Lincoln");
```

你不必担心数组或字符索引，你可以进行许多操作，用起来就好像这些对象是原始数据数据类型一样。

```cpp
string first_name = "Abe" "Abe"
first_name
```

```cpp
string last_name = "Lincoln" "Lincoln"
last_name
```

例如，你可以使用加号 (`+`) 来拼接字符串，而无需担心长度或容量等问题。

```cpp
string full_name = first_name + last_name;
```

该语句将两个字符串合并并形成一个新的字符串 `full_name`，其长度自动是正确的。你不需要担心新字符串是否有足够的空间来存储组合后的名称，因为 `string` 类本身会为你管理所有的存储问题。

```cpp
first_name last_name
"Abe" + "Lincoln"
```

```cpp
string full_name =
first_name + last_name
"Abe Lincoln"
full_name
```

而且，如果你需要索引单个字符，你仍然可以这样做，就像索引 C 字符串一样对它们进行。类似的考虑也适用：单个字符的类型为 `char`，就像你正在索引 C 字符串一样。

```cpp
string s = "I am what I am;"
cout << s[3]; // 打印第四个字符 (m)。
```

`string` 类具有了 C 字符串类型几乎所有的优势，但通常用起来更简单、更方便。`string` 类唯一的缺点可能是它不与 `strtok` 函数兼容，该函数需要 C 字符串才能工作。

## 包含字符串类支持

要使用新的 `string` 类型，你必须做的第一件事是使用 `#include <string>` 指令开启对它的支持。这与函数库中启用 C 字符串支持的指令不同。这些指令看起来相似。

# C++ 字符串类

```cpp
#include <string> // 支持新的字符串类
```

但请记住，C 字符串支持使用的是 "cstring" 而不是 "string"：

```cpp
#include <cstring> // 支持旧式字符串
functions
```

这个 "c" 带来的差异是大！顺便说一下，你可以开启两者的支持，但只有当你打算调用如 `strcpy` 等旧式函数时，才需要包含 "cstring"。

与 `cin` 和 `cout` 一样，除非你在程序开头使用了 `using` 语句，否则 `string` 的名称必须带有 `std::` 前缀：

```cpp
using namespace std;
```

如果你不包含这条语句，你始终可以使用 `std` 前缀（如 `std::string`）引用字符串类。然而，`using namespace` 语句使得对于 C++ 库中的任何内容都不再需要 `std::` 了。

## 声明和初始化 string 类的变量

一旦你开启了 `string` 类型，就可以很容易地使用它来声明变量。（再次，如果你省略了命名空间语句，你应该用 `std::string` 而不是 `string` 来引用该类。）

```cpp
string a, b, c;
```

这创建了三个 C++ 标准库类 `string` 变量。注意这多简单：你不必担心每个字符串可能需要多少空间。你可以通过多种方式初始化字符串。例如：

```cpp
string a("Here is a string."), b("Here is another.");
```

你也可以使用赋值运算符 (`=`) 实现此目的。

```cpp
string a, b;
a = "Here is a string."
b = "Here is another.";
```

你还可以将声明和初始化结合起来：

```cpp
string a = "Here is a string.";
```

# string 类的变量

与 `cin` 和 `cout` 一样，`string` 类对象可以像 C 字符串一样被赋值、复制和比较。与 C 字符串不同，`string` 变量可以根据需要增长单个字符，就像你索引 C 字符串一样。

```cpp
string s = "I am what I am;"
cout << s[3]; // 打印第四个字符 (m).
```

`string` 类具有了 C 字符串类型几乎所有的优势，但通常用起来更简单、更方便。`string` 类唯一的缺点可能是它不与 `strtok` 函数兼容，该函数需要 C 字符串才能工作。

## 包含字符串类支持

要使用新的 `string` 类型，你必须做的第一件事是使用 `#include <string>` 指令开启对它的支持。这与函数库中启用 C 字符串支持的指令不同。这些指令看起来相似。

# C++ 字符串类

```cpp
#include <string> // 支持新的字符串类
```

但请记住，C 字符串支持使用的是 "cstring" 而不是 "string"：

```cpp
#include <cstring> // 支持旧式字符串
functions
```

这个 "c" 带来的差异是大！顺便说一下，你可以开启两者的支持，但只有当你打算调用如 `strcpy` 等旧式函数时，才需要包含 "cstring"。

与 `cin` 和 `cout` 一样，除非你在程序开头使用了 `using` 语句，否则 `string` 的名称必须带有 `std::` 前缀：

```cpp
using namespace std;
```

如果你不包含这条语句，你始终可以使用 `std` 前缀（如 `std::string`）引用字符串类。然而，`using namespace` 语句使得对于 C++ 库中的任何内容都不再需要 `std::` 了。

## 声明和初始化 string 类的变量

一旦你开启了 `string` 类型，就可以很容易地使用它来声明变量。（再次，如果你省略了命名空间语句，你应该用 `std::string` 而不是 `string` 来引用该类。）

```cpp
string a, b, c;
```

这创建了三个 C++ 标准库类 `string` 变量。注意这多简单：你不必担心每个字符串可能需要多少空间。你可以通过多种方式初始化字符串。例如：

```cpp
string a("Here is a string."), b("Here is another.");
```

你也可以使用赋值运算符 (`=`) 实现此目的。

```cpp
string a, b;
a = "Here is a string."
b = "Here is another.";
```

你还可以将声明和初始化结合起来：

```cpp
string a = "Here is a string.";
```

# string 类的变量

与 `cin` 和 `cout` 一样，`string` 类对象可以像 C 字符串一样被赋值、复制和比较。与 C 字符串不同，`string` 变量可以根据需要增长单个字符，就像你索引 C 字符串一样。

```cpp
string s = "I am what I am;"
cout << s[3]; // 打印第四个字符 (m).
```

# C++ 字符串类 207

那么，打印结果字符串就是很容易了。
`cout << str;`

## 练习

- **练习 8.5.1.** 从用户处获取三条信息：狗的名字、品种和它的年龄。然后打印一个包含所有这些信息的句子。
- **练习 8.5.2.** 打印一个复杂的段落，在多个句子中多次使用所有这些数据。

示例 8.6。

## 加法器 #2

处理字符串——无论是 C 字符串还是 `string` 类——都提供了一种每次获取一行输入的方法，并对如何处理这些输入做出智能决策。通过结合使用 `getline` 函数和指针的使用，你可以构建一个比第 2 章“决策，抉择”中的加法器程序要好得多的版本。

那个程序必须使用一个任意代码（如 0）来终止要相加的数字序列，这会产生明显的问题。这个改进版本将继续接受数字，直到用户在未输入任何内容后按下 ENTER 键为止。

你可以使用两种字符串来编写此程序：传统的 C 字符串（以空字符结尾的 `char` 数组）或 STL `string` 类的实例。在你都用过两者之后，你可能会同意处理后者更加简单。

```cpp
adding2.cpp
#include <iostream>
#include <string> // Include support for string class.
using namespace std;
bool get_next_num(int *p)
{
int main()
{
    int sum = 0;
    int n = 0;
```
```cpp
adding2.cpp. cont.
while (get_next_num(&n)) {
    sum += n;
    cout << "The total is: " << sum << endl;
    return 0;
}
bool get_next_num(int *p) {
    string input_line;
    cout << "Enter num (press ENTER to quit): ";
    getline(cin, input_line);
    if (input_line.size() == 0) {
        return false;
    }
    *p = stoi(input_line);
    return true;
}
```

![](img/b88f5481c752ba5bbade24ce372725ab_240_0.png)

## 工作原理

这是一个简单的程序。它所做的只是提示另一个数字，直到用户在输入长度为的字符串后按下 ENTER。

该程序的一个微妙之处在于，它使用的与本章之前描述的 `getline` 版本不同。请记住：对于 C 字符串，使用 `getline` 方法。对于 `string` 类型的对象，使用 `getline` 函数。这确实有点不符合直觉。

```cpp
char my_str[10]; // C-string decl.
string my_str; // string object.
cin.getline(my_str, 10); // Use this on C-strings
getline(cin, my_str); // Use this on string objects.
```

此示例中的返回值用于信号“现在终止”条件。因此，插入数值必须通过其他某种方式返回。这是通过使用指针参数来模拟引用传递来实现的。数值实际上通过这个指针被“返回”了：

```cpp
*p = stoi(input_line);
```

`stoi` 函数自 C++11 以来提供，用于将字符串转换为整数。对于转换为浮点数，C++11 同样

## 对 string 类型的其他操作

提供了 `stof` 函数。如果你的编译器太旧，不支持 `stoi` 和 `stof`，你仍然可以使用替代方案 `atoi` 和 `atof`。唯一的问题是，如果你想使用这些函数之一，需要先使用 `c_str` 函数转换为 C 风格格式。

```cpp
*p = atoi(input_line.c_str());
```

这看起来很丑陋，但在早期版本的 C++ 中可以工作。

## 练习

- **练习 8.6.1.** 修改 `get_next_num` 函数，使其中一个参数指定为默认值。如果终端用户在不输入任何文本的情况下按下 ENTER，函数将返回此默认值。
- **练习 8.6.2.** 重写示例以使得

# 文件：电子存储

在你编程生涯的某个时刻，你将将不得不处理磁盘文件。大多数现实世界的应用程序都需要存储和检索持久化信息，例如薪资程序、电子表格和文本编辑器等（这只是其中几个例子）。即使是更简单的应用程序通常也需要长期数据存储。

当程序结束时，你不希望这些信息消失在虚无中。例如，如果这是你的薪资信息，或者是肯塔基上校的秘密炸鸡配方怎么办？在某些情况下，你可能希望它保留下来——持续很多年之久。

磁盘文件与主内存（RAM）不同，即使在计算机关闭时也能继续保持其状态。因此，当你需要一个地方存放数据以备后用时，请将其放入磁盘文件中。

## 引入文件流对象

在使用 `cin` 和 `cout`（控制台输入输出）时，你已经使用了“对象”——即知道如何响应请求的自包含实体。是时候引入一些新对象了。C++ 提供了文件流，它们支持与 `cin` 和 `cout` 相同的函数调用和运算符。

C++ 程序员经常讨论流（streams）。流是你读取或写入数据的东西。仅此而已。这个术语唤起了数据像河水一样流动的意象，即从某个源（例如文件）流动。虽然数据流并不总是像河流那样无止尽，但这是一个非常有用的比喻。

写入文本文件涉及几个简单的步骤。第一步是通过使用 `#include <fstream>` 指令启用对文件流操作的支持。这会隐式地引入文件流操作的声明。

```cpp
#include <fstream>
```
