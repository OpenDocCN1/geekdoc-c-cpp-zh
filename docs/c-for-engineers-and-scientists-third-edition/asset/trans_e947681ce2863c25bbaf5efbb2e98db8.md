

## 510 完善基础

## 信息点

## 字符串（string）和字符（char）数据类型

字符串可以包含零、一个或多个字符。当字符串没有字符时，被称为长度为零的空字符串。带有单个字符的字符串（例如 "a"）是长度为一的字符串，其存储方式与 char 数据类型（例如 'a'）不同。

然而，在许多实际用途中，长度为一的字符串和 char 的响应方式是相同的；例如，的 `cout << "\n"` 和 `cout << '\n'` 都会在屏幕上产生新行。重要的是理解它们是不同的数据类型；例如，以下声明：

```cpp
string sl = 'a';      // 无效初始化
char key = "\n";    // 无效初始化
```

这些声明会产生编译器错误，因为它们尝试用另一种数据类型的字面量来初始化一种数据类型。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_529_0.png)

**图 9.6** 类型化字符存储在缓冲区中

程序 9.8 中的 `cin` 输入流首先接受输入的数字，但将 `\n` 留在缓冲区中。下一个输入语句（即对 `getline()` 的调用）会将回车键的代码作为下一个字符获取并终止任何后续输入。以下是程序 9.8 的示例运行：

```
Enter a number: 26
The number entered is 26
Enter text:
The text entered is
```

在此输出中，针对提示 `Enter text:`，程序没有接受任何文本。没有发生文本输入是因为在程序接受了数字 26 之后，回车键的代码（即换行转义序列）仍留在缓冲区中，并被 `getline()` 函数获取并解释为其输入的结束。无论程序 9.8 中是整数、字符串还是任何其他输入被 `cin` 接受后跟随 `getline()` 调用，都会出现这种结果。这个“幻影”回车键问题有三种解决方案：

- 不要在一个程序中混合使用 `cin` 和 `getline()` 输入。
- 在 `cin` 输入后跟随调用 `cin.ignore()`。
- 在字符变量中接受回车键然后忽略它。

首选解决方案是第一种。然而，所有的解决方案都围绕这样一个事实：回车键是一个合法的字符输入，必须被识别为字符。你在第 9.4 节学习接受 char 数据类型时会遇到这个问题。

## 字符串处理

可以使用字符串类函数或第 9.4 节描述的逐字符函数对字符串进行操作。表 9.4 列出了最常用的字符串类函数，标准算术和比较运算符也可以用于字符串。

**表 9.4 字符串类函数（需要头文件 string）**

| 函数/操作 | 描述 | 示例 |
| --- | --- | --- |
| int length() | 返回字符串的长度 | string.length() |
| int size() | 与前述项相同 | string.size() |
| at(int index) | 返回指定索引处的字符，如果索引不存在则抛出异常 | string.at(4) |
| int compare(str) | 将给定字符串与 str 比较；如果给定的字符串小于 str 则返回负值，相等则返回 0，如果给定的字符串大于 str 则返回正值 | string1.compare(str2) |
| c_str() | 将字符串作为空终止的 C 字符串返回 | string1.c_str() |
| bool empty | 如果字符串为空返回 true，否则返回 false | string1.empty() |

**表 9.4 字符串类处理函数（需要头文件 string）（续）** |

| 函数/操作 | 描述 | 示例 |
| --- | --- | --- |
| erase(ind,n) | 从索引 ind 开始从字符串中删除 n 个字符 | string1.erase(2,3) |
| erase(ind) | 从索引 ind 开始到字符串末尾删除字符串的所有字符，剩余字符串的长度变为 ind | string1.erase(4) |
| int find(str) | 返回 str 在完整字符串中首次位置的索引 | string1.find("*") |
| int find(str, ind) | 返回 str 在完整字符串中首次位置的索引，从索引 ind 开始搜索 | string1.find("the",5) |
| int find_first_of(str, ind) | 返回完整字符串中 str 中任意字符的首次出现索引，从索引 ind 开始搜索 | string1.find_first_of("lt",6) |
| int find_first_not_of(str, ind) | 返回完整字符串中不在 str 中的任意字符的首次出现索引，从索引 ind 开始搜索 | string1.find_first_not_of("lt",6) |

**表 9.4 字符串类处理函数（需要头文件 string）（续）** |

| 函数/操作 | 描述 | 示例 |
| --- | --- | --- |
| void insert(ind, str) | 从索引 ind 开始在完整字符串中插入字符串 | string.insert(4, "there") |
| void replace(ind, n, str) | 从字符串对象中从索引 ind 开始删除 n 个字符并插入字符串 | string1.replace(2,4, "okay") |
| string substr(ind,n) | 返回一个从 ind 开始从字符串中提取的 n 个字符组成的字符串 | string1.substr(0,10) |
| void swap(str) | 交换字符串中的字符 | string1.swap(string2) |
| = | 赋值 | string1 = string2 |
| + | 连接两个字符串 | string1 + string2 |
| != | 关系 | string1 != string2 |
| < | 如果字符串小于则返回 true | string1 < string2 |
| >= | 如果字符串大于或等于则返回 true | string1 >= string2 |

## 514 完善基础

## 字符串类

## 程序 9.9

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string string1 = "Hello";
    string string2 = "Hello there";
    cout << "string1 is the string: " << string1 << endl;
    cout << "The number of characters in string1 is " << int(string1.length()) << endl;

    cout << "string2 is the string: " << string2 << endl;
    cout << "The number of characters in string2 is " << int(string2.length()) << endl;

    if (string1 < string2) {
        cout << string1 << " is less than " << string2 << endl;
    } else if (string1 == string2) {
        cout << string1 << " is equal to " << string2 << endl;
    } else {
        cout << string1 << " is greater than " << string2 << endl;
    }

    string1 = string1 + " there!";
    cout << "After concatenation, " << string1 << " contains the characters: " << string1 << endl;
    cout << "The length of this string is " << int(string1.length()) << endl;

    return 0;
}
```

以下是程序 9.9 的示例输出：

+   string1 is the string: Hello
The number of characters in string1 is 5

string2 is the string: Hello there
The number of characters in string2 is 11

Hello is less than Hello there endl

After concatenation, Hello there! contains the characters: Hello there! endl
The length of this string is 13

