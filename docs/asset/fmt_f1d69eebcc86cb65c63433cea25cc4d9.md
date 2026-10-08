
运行：
输入名：`John`
输入姓：`Brown`
输入首字母：`A`

Full name in first format: John A. Brown
Full name in second format: Brown, John A.

## 示例 10.23

程序 10.23 展示了如何读取人的名、姓和首字母，以创建两种格式的全名。

## 示例 10.24

在这个示例中，我们展示了如何将一个左对齐文本的文件转换为右对齐文本的文件。解决这个问题有几种方法，取决于我们对文件的了解程度。如果我们知道最大行长度，问题非常简单。否则，我们需要找到最大行长度。要找到最大行长度，可以使用两种方法。第一种方法是将输入文件的行读入字符串数组中，找到最大行长度，然后将其写入输出文件。第二种方法是读取两次输入文件。

### 程序 10.24 在文件中写入行（继续）

```cpp
37 getline(inputFile, line);

38 string temp(maxSize, ' ');

39 line.insert(0, temp);

40 line.append("\n");

41 outputFile << line;

42 }

43 inputFile.close();

44 outputFile.close();

45 return;

46 }
```

以下展示了程序运行后输入文件和输出文件的内容。

| 输入文件的内容 | 输出文件的内容 |
|---|---|
| This is a line. | This is a line. |
| This is the second line. | This is the second line. |
| This is a new line. | This is a new line. |
| This is a shorter one. | This is a shorter one. |
| This is the longest line by far. | This is the longest line by far. |

## 转换

我们可以将 C++ 对象转换为字符数组或字符串。

| `const char *arr = str.data();` | 转换为字符数组 |
| `const char *str = str.c_str();` | 转换为字符串 |

# 1.3 程序设计

在这一部分，我们首先在字符串类中创建自定义函数。然后我们使用这些函数来解决字符串处理中的一些经典问题。我们通过定义与字符串类相关的新函数来演示这种能力。

## 10.3.1 自定义函数

库定义了一系列成员函数，但我们可以根据需要创建自定义函数。我们在成员函数中创建这些。我们把这些函数命名为：`pushBack`、`pushFront`、`popBack` 和 `popFront`。在随后的章节中，我们将看到这些函数被定义于其他库（尽管名称不同），但只有一个以 `push_back` 为名被定义在字符串类中。

### 程序 10.25 为我们的自定义函数头文件（继续）

```cpp
31 strg.erase(index, 1);

32 return temp;

33 }

34 // popBack 函数定义

35 char popBack(string& str)

36 {

37 int index = strg.size() - 1;

38 char temp = strg[index];

39 strg.erase(index, 1);

40 return temp;

41 }

42 #endif
```

### 程序 10.26 测试自定义函数

（继续）

### 程序 10.26 测试自定义函数（继续）

```cpp
cout << endl;

// 测试 popBack 函数

cout << "调用 popBack 前的字符串: " << strg << endl;

char c2 = popBack(strg);

cout << "调用 popBack 后的字符串: " << strg << endl;

cout << "弹出的字符: " << c2 << endl;

cout << endl;

return 0;

}
```

运行：
调用 `pushFront` 前的字符串: abcdefgh
调用 `pushFront` 后的字符串: Aabcdefgh

调用 `pushBack` 前的字符串: abcdefgh
调用 `pushBack` 后的字符串: AabcdefghZ

调用 `pushFront` 前的字符串: abcdefghZ
调用 `pushFront` 后的字符串: abcdefghZ
弹出的字符: A

调用 `pushBack` 前的字符串: abcdefghZ
调用 `pushBack` 后的字符串: abcdefgh
弹出的字符: Z

## 10.3.2 进制中的转换

在计算机科学中，我们使用不同的位置进制；这些在附录 B 中描述：二进制、八进制、十进制和十六进制。每个计数系统都使用一组符号和一个基数。基数定义了系统中使用的符号总数。表 10.3 显示了我们在编程中使用的基数和符号。符号 A、B、C、D、E、F 的值分别为 10, 11, 12, 13, 14 和 15。

虽然所有这些进制都使用不同的表示法表示整数，但十进制是唯一可以在程序中作为整数使用的系统。其他系统中的数字可能以字符字符串的形式表示。

| 表 10.3 进制系统 |
| 系统 | 基数 | 符号 |
| 二进制 | 2 | 0, 1 |
| 八进制 | 8 | 0, 1, 2, 3, 4, 5, 6, 7 |
| 十进制 | 10 | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 |
| 十六进制 | 16 | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F |

# 第 10 章

# 字符串

刚开始

| | [0] | [1] | [2] |
|---|---|---|---|
| 迭代 1 后 | | [0] | [1] | |
| 迭代 2 后 | | | [0] | |
| 迭代 3 后 | | | | |

`decimal = 0`

| 图例: |
| 删除的字符 |
| 原始字符 |
| 十进制值 |

注意：在每次迭代中，字符串都会减小，但十进制值会增长。

图 10.14 从任意进制转换为十进制

# 在 C++ 中，十进制数被用作整数；其他系统的数被用作字符串。

这意味着当我们处理不同的进制系统时，必须将字符串转换为整数或反之。在本节中，我们提供了这种操作的通用设计。在学习本节其余部分之前，我们建议你复习附录 B。

## 从任意其他进制转换为十进制

图 10.14 显示了如何将一个三个字符的字符串转换为整数。我们使用由字符串大小控制的循环。当字符串为空时，我们退出循环。在开始循环之前，我们将 `decimal` 的值设置为 0。在每次迭代中，我们将 `decimal` 的上一个值乘以基数。然后我们弹出前面的字符，将其转换为十进制，并将其加到 `decimal` 的值上。注意，在每次迭代中，`decimal` 的值在增加，但字符串的大小在减小。当我们退出循环时，`decimal` 的值就计算出来了。表 10.4 显示了该算法。

| 表 10.4 将字符串转换为十进制的算法 |
| set base | // 将基数设置为 2, 16 |
| decimal = 0 | |
| input_string | |
| while (string not empty) | |
| { | |
| decimal *= base; | |
| ch = popFront(string) | // 在之前使用 popFront 函数 |
| decimal += findValue(ch) | // 使用函数将 ch 转换为其值 |
| } | |

## 示例 10.25

程序 10.27 将二进制字符串转换为十进制整数。在这种情况下，基数为 2。我们使用了之前开发的 `popFront` 函数（包含在头文件中）。我们写了一个小函数 `findValue` 来将提取的字符转换为其整数值。

### 程序 10.27 将二进制字符串转换为十进制整数

```cpp
****************************************************
* 将二进制字符串转换为十进制
* 整数的程序。
****************************************************

#include "customized.h"
#include <string>
#include <iostream>

using namespace std;

****************************************************
* 将字符转换为其整数值的
* 函数。
****************************************************

int findValue(char ch) {
    return static_cast<int>(ch) - 48;
}

int main() {
    // 变量声明
    string binary;
    int base = 2;
    int decimal = 0;
    // 输入二进制字符串
    cout << "输入二进制: ";
    getline(cin, binary);
    while (!binary.empty()) {
        decimal *= base;
        char ch = popFront(binary);
        decimal += findValue(ch);
    }
    cout << "十进制值: " << decimal << endl;
    return 0;
}
```

运行：
输入二进制: 10
十进制值: 10
输入二进制: 11
十进制值: 11
输入二进制: 10000
十进制值: 16

## 10.3.2 进制

在计算机科学中，我们使用不同的位置进制；这意味着当我们处理不同的进制系统时，必须将字符串转换为整数或反之。在本节中，我们提供了这种操作的通用设计。在学习本节其余部分之前，我们建议你复习附录 B。

## 从任意其他进制转换为十进制

图 10.14 显示了如何将一个三个字符的字符串转换为整数。我们使用一个由字符串大小控制的循环。当字符串为空时，我们退出循环。在开始循环之前，我们将 `decimal` 的值设置为 0。在每次迭代中，我们将 `decimal` 的上一个值乘以基数。然后我们弹出前面的字符，将其转换为十进制，并将其加到 `decimal` 的值上。注意，在每次迭代中，`decimal` 的值在增加，但字符串的大小在减小。当我们退出循环时，`decimal` 的值就计算出来了。表 10.4 显示了该算法。

## 从十进制到任意进制

图 10.15 显示了如何将一个十进制数转换为字符串。我们使用一个由 `decimal` 值控制的循环。当 `decimal` 为 0 时，我们退出循环。在开始循环之前，我们将字符串设置为特殊情况。在每次迭代中，我们将 `decimal` 除以基数得到余数。然后我们将余数转换为字符，并将其推入字符串前面。注意，在每次迭代中，`decimal` 的值在减小，但字符串的大小在增加。当我们退出循环时，字符串就准备好了。表 10.5 显示了该算法。

| 表 10.5 将十进制转换为字符串的算法 |
| set base | // 将基数设置为 2, 8, 16 |
| string str | |
| input decimal | |
| while (decimal > 0) | |
| { | |
| decimal /= base; | |
| ch = char(decimal % base) | // 将余数转换为字符 |
| str.pushFront(ch) | // 将字符推入字符串前面 |
| } | |

## 示例 10.26

程序 10.28 显示了如何将一个十进制数转换为二进制字符串。

### 程序 10.28 十进制转二进制

```cpp
****************************************************
* 将十进制数转换为
* 二进制字符串的程序。
****************************************************

#include <string>
#include "customized.h"
#include <iostream>

using namespace std;

****************************************************
* 将整数转换为字符的
* 函数。
****************************************************

char findChar(int digit) {
    return char (digit + 48);
}

int main() {
    // 变量声明
    int decimal;
    int base = 2;
    string string;
    // 输入十进制数
    cout << "输入十进制: ";
    cin >> decimal;
    if (decimal == 0) {
        string = "0";
    } else {
        while (decimal > 0) {
            decimal /= base;
            char ch = findChar(decimal % base);
            string.pushFront(ch);
        }
    }
    cout << "二进制字符串: " << string << endl;
    return 0;
}
```

运行：
输入十进制: 10
二进制字符串: 1010
输入十进制: 15
二进制字符串: 1111
输入十进制: 16
二进制字符串: 10000

### 程序 10.28 从十进制转换为二进制（续）

```cpp
26 {
    cout << "Enter a positive decimal: ";
    cin >> decimal;
} while (decimal <= 0);
    // 转换为二进制
    while (decimal > 0) {
        int digit = decimal % base;
        char ch = findChar(digit);
        pushFront(str, ch);
        decimal /= base;
    }
    // 输出二进制
    cout << "Binary: " << str;
    40 return 0;
}
```

运行：
Enter a positive decimal: 35
Binary: 100011
运行：
Enter a positive decimal: 5
Binary: 111
运行：
Enter a positive decimal: 126
Binary: 1111110

对输入的十进制数值进行验证非常简单，通过一个 `do-while` 循环完成。为了在二进制字符串中插入字符，我们使用了之前在头文件中创建创建并包含的 `pushFront` 函数。

## 关键术语

- C 字符串
- C++ 字符串
- 字符串字面量
- 字符串标记 (`token`)

## 总结

C 字符串是一个以空字符结尾的字符数组，可以像数组一样创建。字面量是一个用两个双引号包含字符的常量值。我们可以使用提取运算符或 `getline` 库函数输入 C 字符串。我们可以使用插入运算符输出 C 字符串。

C++ 字符串类位于 `<string>` 头文件中。它是一个创建字符数组的类，该数组不是空字符结尾的且在内存中创建。它像其他类一样定义了数据成员和成员函数。

## 练习

- PR-1. 下面的代码片段使用 C 语言。将代码修改为使用 C++ 字符串。
```cpp
const char* str = "This is a string";

cout << strlen(str) << endl;
```

- PR-2. 下面的代码片段使用 C 语言。将代码修改为使用 C++ 字符串。
```cpp
const char* str1 = "This is a string";
const char* str2 = "This is another one";

cout << strcmp(str1, str2) << endl;
```

- PR-3. 下面的代码片段使用 C 语言。重写代码使用 C++ 字符串来实现相同目标。
```cpp
char str1[] = "This is the first string";
char str2[] = "Here is another one";

strncpy(str1, str2);

cout << str1 << endl;
```

- PR-4. 下面的代码片段使用 C 语言。重写代码使用 C++ 字符串来实现相同目标。
```cpp
char str1[] = "This is the first string";
char str2[] = "Here is another one";

strncpy(str1, str2, 4);

cout << str1 << endl;
```

- PR-5. 下面的代码片段使用 C 语言。将代码修改为使用 C++ 字符串。
```cpp
char str1[40] = "The time has changed.";
const char* str2 = "Are you ready?";

strcat(str1, str2);

cout << str1 << endl;
```
