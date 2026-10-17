
| 卡牌: 0 花色: 0 颜色: 0 | 卡牌: 0 花色: 2 颜色: 1 |
| :--- | :--- |
| 卡牌: 1 花色: 0 颜色: 0 | 卡牌: 1 花色: 2 颜色: 1 |
| 卡牌: 2 花色: 0 颜色: 0 | 卡牌: 2 花色: 2 颜色: 1 |
| 卡牌: 3 花色: 0 颜色: 0 | 卡牌: 3 花色: 2 颜色: 1 |
| 卡牌: 4 花色: 0 颜色: 0 | 卡牌: 4 花色: 2 颜色: 1 |
| 卡牌: 5 花色: 0 颜色: 0 | 卡牌: 5 花色: 2 颜色: 1 |
| 卡牌: 6 花色: 0 颜色: 0 | 卡牌: 6 花色: 2 颜色: 1 |
| 卡牌: 7 花色: 0 颜色: 0 | 卡牌: 7 花色: 2 颜色: 1 |
| 卡牌: 8 花色: 0 颜色: 0 | 卡牌: 8 花色: 2 颜色: 1 |
| 卡牌: 9 花色: 0 颜色: 0 | 卡牌: 9 花色: 2 颜色: 1 |
| 卡牌: 10 花色: 0 颜色: 0 | 卡牌: 10 花色: 2 颜色: 1 |
| 卡牌: 11 花色: 0 颜色: 0 | 卡牌: 11 花色: 2 颜色: 1 |
| 卡牌: 12 花色: 0 颜色: 0 | 卡牌: 12 花色: 2 颜色: 1 |
| 卡牌: 0 花色: 1 颜色: 0 | 卡牌: 0 花色: 3 颜色: 1 |
| 卡牌: 1 花色: 1 颜色: 0 | 卡牌: 1 花色: 3 颜色: 1 |
| 卡牌: 2 花色: 1 颜色: 0 | 卡牌: 2 花色: 3 颜色: 1 |
| 卡牌: 3 花色: 1 颜色: 0 | 卡牌: 3 花色: 3 颜色: 1 |
| 卡牌: 4 花色: 1 颜色: 0 | 卡牌: 4 花色: 3 颜色: 1 |
| 卡牌: 5 花色: 1 颜色: 0 | 卡牌: 5 花色: 3 颜色: 1 |

图 22.16 | 用于存储整副牌的位域。（2 部分中的第 1 部分。）

| 卡牌: 6 花色: 1 颜色: 0 | 卡牌: 6 花色: 3 颜色: 1 |
| :--- | :--- |
| 卡牌: 7 花色: 1 颜色: 0 | 卡牌: 7 花色: 3 颜色: 1 |
| 卡牌: 8 花色: 1 颜色: 0 | 卡牌: 8 花色: 3 颜色: 1 |
| 卡牌: 9 花色: 1 颜色: 0 | 卡牌: 9 花色: 3 颜色: 1 |
| 卡牌: 10 花色: 1 颜色: 0 | 卡牌: 10 花色: 3 颜色: 1 |
| 卡牌: 11 花色: 1 颜色: 0 | 卡牌: 11 花色: 3 颜色: 1 |
| 卡牌: 12 花色: 1 颜色: 0 | 卡牌: 12 花色: 3 颜色: 1 |

**图 22.16** 用于存储整副牌的位域。（2 部分中的第 2 部分）

可以指定未命名的位域，在这种情况下，该字段被用作结构中的填充——这三个位中无法存储任何内容。成员 `b` 存储在另一个单元中。

```cpp
struct Example {
  unsigned a : 13;
  unsigned : 3; // 对齐到下一个边界
  unsigned b : 4;
};
```

宽度为 0 的未命名位域用于对齐存储 `a` 的存储单元边界。例如，如下结构体定义：

```cpp
struct Example {
  unsigned a : 13;
  unsigned : 0; // 对齐到下一个边界
  unsigned b : 4;
};
```

未命名位域用于跳过 `a` 所在的存储单元边界。位域的操作取决于机器。例如，某些计算机允许位域跨越边界，而另一些则不允许。

> **移植性提示**：像访问数组元素一样使用下标访问单个位是错误的。

> **常见错误**：尝试获取位域的地址（`&` 运算符不能用于位域）是错误的。

> **性能提示**：尽管位域节省了空间，但使用它们会导致编译器生成额外的机器语言代码，以访问存储单元的一部分。

## 22.7 字符处理库

大多数数据是以字符、数字和各种符号的形式输入计算机的。字符处理库包含了用于检查和操作字符数据的有用函数。每个函数返回一个字符（表示为 `int` 或 EOF。注意 `EOF` 的值为 -1，且某些架构不允许在 `char` 变量中存储负值。要使用字符处理库函数，请包含 `<ctype>` 头文件。

| 原型 | 描述 |
| :--- | :--- |
| int isdigit(int c) | 如果 `c` 是数字，返回 1；否则返回 0。 |
| int isalpha(int c) | 如果 `c` 是字母，返回 1；否则返回 0。 |
| int isnum(int c) | 如果 `c` 是数字或字母，返回 1；否则返回 0。 |
| int isxdigit(int c) | 如果 `c` 是十六进制数字，返回 1；否则返回 0。（二进制、八进制和十进制的详细解释见附录 D。） |
| int islower(int c) | 如果 `c` 是小写字母，返回 1；否则返回 0。 |
| int isupper(int c) | 如果 `c` 是大写字母，返回 1；否则返回 0。 |
| int towlower(int c) | 如果 `c` 是大写字母，`towlower` 返回其小写字母；否则返回参数。 |
| int toupper(int c) | 如果 `c` 是小写字母，`toupper` 返回其大写字母；否则返回参数。 |
| int isspace(int c) | 如果 `c` 是空白字符——换行 `\n`、空格 ` `、回车 `\r`、水平制表符 `\t` 或垂直制表符 `\v`——返回 1；否则返回 0。 |
| int iscntrl(int c) | 如果 `c` 是控制字符，如换行 `\n`、分页符 `\f`、回车 `\r`、水平制表符 `\t`、垂直制表符 `\v` 或退格 `\b`——返回 1；否则返回 0。 |
| int isprint(int c) | 如果 `c` 是包括空格在内的打印字符，返回 1；否则返回 0。 |
| int isgraph(int c) | 如果 `c` 是除空格 以外的打印字符，返回 1；否则返回 0。 |

图 22.17 | 字符处理库函数。

图 22.18 展示了 `isdigit`、`isalpha`、`isnum` 和 `isxdigit` 函数。`isdigit` 确定其参数是否为数字（0–9）。`isalpha` 确定其参数是否大写字母（A–Z）或小写字母（a–z）。

```cpp
// // 图 22.18: fig22_18.cpp
// 字符处理函数 isdigit, isalpha, isalnum 和 isxdigit
#include <iostream>
#include <ctype> // 字符处理函数
using namespace std;
int main() {
    cout << "According to isdigit:\n";
    cout << isdigit('8') ? "8 is a" : "8 is not a" << endl;
    cout << isdigit('B') ? "B is a" : "B is not a" << endl;
    cout << "According to isalpha:\n";
    cout << isalpha('A') ? "A is a" : "A is not a" << endl;
    cout << isalpha('B') ? "B is a" : "B is not a" << endl;
    cout << isalpha('6') ? "6 is a" : "6 is not a" << endl;
    cout << isalpha('4') ? "4 is a" : "4 is not a" << endl;
    cout << "According to isalnum:\n";
    cout << isalnum('A') ? "A is a" : "A is not a" << endl;
    cout << isalnum('8') ? "8 is a" : "8 is not a" << endl;
    cout << isalnum('#') ? "# is a" : "# is not a" << endl;
    cout << "According to isdigit:\n";
    cout << isdigit('F') ? "F is a" : "F is not a" << endl;
    cout << isdigit('J') ? "J is a" : "J is not a" << endl;
    cout << isdigit('7') ? "7 is a" : "7 is not a" << endl;
    cout << isdigit('$') ? "$ is a" : "$ is not a" << endl;
    cout << isdigit('f') ? "f is a" : "f is not a" << endl;
    return 0;
}
```

## 第 22 章 位、字符、C 字符串和结构体

根据 `isalnum`，A 是数字或字母
8 是数字或字母
# 不是数字或字母

根据 `isdigit`：
F 是十六进制数字
J 不是十六进制数字
7 不是十六进制数字
$ 不是十六进制数字
f 是十六进制数字

# 图 22.18 | 字符处理函数 isdigit, isalpha, isalnum 和 isdigit。（22 部分中的第 2 部分。）

22.18 在每个函数中使用了条件运算符 (?:) 来决定对于每个测试的字符，在输出中应该打印字符串 " a " 还是字符串 " a"。第 9 行表示，如果 '8' 是数字——即如果 `isdigit` 返回真（非零）值——则打印字符串 "8 a"。如果 '8' 不是数字（即如果 `isdigit` 返回 0），则打印字符串 "8 is not a a"。

22.19 展示了 islower, isupper, tolower 和 toupper。`islower` 函数判断参数是否为小写字母 (a-z)。`isupper` 函数判断参数是否为大写字母 (A-Z)。`tolower` 函数将大写字母转换为小写字母返回——如果参数不是大写字母，`tolower` 返回原参数。`toupper` 函数将小写字母转换为大写字母并返回大写字母——如果参数不是小写字母，`toupper` 返回原参数。

```cpp
// Fig. fig22_19.cpp
// 字符处理函数 islower, isupper, tolower 和 toupper.
#include <iostream>
#include <cctype> // 字符处理函数原型
namespace std;
int main() {
  cout << "According to islower:\n";
  cout << (islower('a')) ? "p is a" : "p is not a";
  cout << "-- lowercase letter\n";
  cout << (islower('P')) ? "P is a" : "P is not a";
  cout << "-- lowercase letter\n";
  cout << (islower('S')) ? "S is a" : "S is not a";
  cout << "-- lowercase letter\n";
  cout << (islower('I')) ? "I is a" : "I is not a";
  cout << "-- lowercase letter\n";
```
# 图 22.19 | 字符处理函数 islower, isupper, tolower 和 toupper。（22 部分中的第 1 部分。）

```cpp
18 cout << "\nAccording to isupper:\n"
19 << (isupper('D') ? "D is an" : "D is not an")
20 << " uppercase letter\n"
21 << (isupper('d') ? "d is an" : "d is not an")
22 << " uppercase letter\n"
23 << (isupper('8') ? "8 is an" : "8 is not an")
24 << " uppercase letter\n"
25 << (isupper('$') ? "$ is an" : "$ is not an")
26 << " converted to uppercase letter;\n";
28 cout << "\nconverted to uppercase is "
29 << static_char(toupper('m'))
30 << "\n7 converted to uppercase is "
31 << static_char(toupper('7'))
32 << "\n$ converted to uppercase is "
33 << static_char(toupper('$'))
34 << "\nL converted to lowercase is "
35 << static_char(tolower('L')) << endl;
36 } }
```

根据 `islower`：
p 是一个小写字母
P 不是小写字母
5 不是小写字母
8 不是小写字母
$ 不是小写字母

根据 `isupper`：
D 是一个大写字母
d 不是大写字母
8 不是大写字母
$ 不是大写字母
m 转换为大写是
7 转换为大写是
$ 转换为大写是
L 转换为小写是

图 22.19 | 字符处理函数 islower, isupper, tolower 和 toupper。（22 部分中的第 2 部分。）

22.20 展示了 isspace, iscntrl, ispunct 和 isprint。`isspace` 判断参数是否为空白字符。`iscntrl` 判断参数是否为控制字符。`ispunct` 判断参数是否为标点符号。`isprint` 判断参数是否为可打印字符。

位、字符、C 字符串和结构体

```cpp
// Fig. fig22_20.cpp
// 字符处理函数 isspace, iscntrl, ispunct and isprint.
#include <iostream>
#include <ctype> // 字符处理函数原型
namespace std;
int main() {
  cout << "According to islower:\n";
  cout << (islower('a')) ? "p is a" : "p is not a";
  cout << "-- lowercase letter\n";
// ... (省略重复代码以保持逻辑一致)
```
