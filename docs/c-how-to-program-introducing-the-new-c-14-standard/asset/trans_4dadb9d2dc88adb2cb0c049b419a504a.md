

从第二个参数复制到临时字符数组，然后再从临时数组复制到第一个参数。这使得我们可以将字符串某一部分中的字符复制到同一个字符串的另一部分。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2614_0.png)

**常见编程错误 22.11**

*除* `memmove` *之外，用于复制字符的字符串操作函数，在复制发生于同一个字符串的不同部分之间时，其结果是未定义的。*

**图 22.43** 中的程序使用 `memmove`（第 12 行）将数组 `x` 的最后 `10` 个字节复制到数组 `x` 的前 `10` 个字节中。

```cpp
// Fig. 22.43: fig22_43.cpp
// Using memmove.
#include <iostream>
#include <cstring> // memmove prototype
using namespace std;

int main() {
   char x[] {"Home Sweet Home"};

   cout << "The string in array x before memmove is: " << x;
   cout << "\nThe string in array x after memmove is: "
        << static_cast<char*>(memmove(x, &x[5], 10)) << endl;
}
```

```text
The string in array x before memmove is: Home Sweet Home
The string in array x after memmove is: Sweet Home Home
```

**图 22.43 内存处理函数 `memmove`。**

函数 `memcmp`（**图 22.44** 第 13～15 行）将其第一个参数中指定数量的字符与第二个参数中相应的字符进行比较。如果第一个参数大于第二个参数，该函数返回大于零的值；如果两个参数相等，则返回零；如果第一个参数小于第二个参数，则返回小于零的值。_[注意：在某些编译器中，函数 `memcmp` 返回 `−1`、`0` 或 `1`，如 **图 22.44** 的示例输出所示。在其他编译器中，该函数返回 `0`，或者返回所比较字符串中第一个不同字符的数值代码之差。例如，比较 `s1` 和 `s2` 时，它们之间第一个不同的字符是每个字符串的第五个字符——`s1` 中的 `E`（数值代码为 69）和 `s2` 中的 `X`（数值代码为 88）。在这种情况下，返回值将为 `19`（当用 `s2` 与 `s1` 比较时，则为 `−19`）。]_

```cpp
// Fig. 22.44: fig22_44.cpp
// Using memcmp.
#include <iostream>
#include <iomanip>
#include <cstring> // memcmp prototype
using namespace std;

int main() {
   char s1[]{"ABCDEFG"};
   char s2[]{"ABCDXYZ"};

   cout << "s1 = " << s1 << "\ns2 = " << s2 << endl
      << "\nmemcmp(s1, s2, 4) = " << setw(3) << memcmp(s1, s2, 4)
      << "\nmemcmp(s1, s2, 7) = " << setw(3) << memcmp(s1, s2, 7)
      << "\nmemcmp(s2, s1, 7) = " << setw(3) << memcmp(s2, s1, 7)
      << endl;
}
```

```text
s1 = ABCDEFG
s2 = ABCDXYZ

memcmp(s1, s2, 4) =   0
memcmp(s1, s2, 7) =  -1
memcmp(s2, s1, 7) =   1
```

**图 22.44 内存处理函数 `memcmp`。**

函数 `memchr` 在对象的指定字节数中搜索由 `unsigned char` 表示的某个字节。如果在对象中找到该字节，则返回指向它的指针；否则，该函数返回空指针。**图 22.45** 第 12 行在字符串 `"This is a string"` 中搜索字符（字节）`'r'`。

```cpp
// Fig. 22.45: fig22_45.cpp
// Using memchr.
#include <iostream>
#include <cstring> // memchr prototype
using namespace std;

int main() {
   char s[] {"This is a string"};

   cout << "s = " << s << "\n" << endl;
   cout << "The remainder of s after character 'r' is found is \""
      << static_cast<char*>(memchr(s, 'r', 16)) << "\"" << endl;
}
```

```text
s = This is a string

The remainder of s after character 'r' is found is "ring"
```

**图 22.45 内存处理函数 `memchr`。**

函数 `memset` 将其第二个参数中的字节值复制到其第一个参数所指向对象的指定数量的字节中。图 22.46 第 12 行使用 `memset` 将 `'b'` 复制到 `string1` 的前 7 个字节中。

```cpp
// Fig. 22.46: fig22_46.cpp
// Using memset.
#include <iostream>
#include <cstring> // memset prototype
using namespace std;

int main() {
   char string1[15] {"BBBBBBBBBBBBBB"};

   cout << "string1 = " << string1 << endl;
   cout << "string1 after memset = "
      << static_cast<char*>(memset(string1, 'b', 7)) << endl;
}
```

```text
string1 = BBBBBBBBBBBBBB
string1 after memset = bbbbbbbBBBBBBB
```

**图 22.46 内存处理函数 `memset`。**

## 22.12 总结

本章介绍了 `struct` 定义、`struct` 的初始化以及如何将它们与函数结合使用。我们讨论了 `typedef`，并介绍了如何使用它创建别名，以帮助提高可移植性。我们还介绍了用于操作数据的按位运算符，以及用于紧凑存储数据的位字段。你还学习了 `<cstdlib>` 中的字符串转换函数和 `<cstring>` 中的字符串处理函数。

## 总结

### 第 22.2 节 结构定义

- 关键字 `struct`（第 900 页）开始每个结构定义。
- 结构定义的大括号之间是结构成员声明。
- 结构定义会创建一种新的数据类型，可用于声明变量。

### 第 22.3 节 `typedef` 和 `using`

- 使用 `typedef`（第 902 页）创建新的类型名称并不会创建新类型；它只是为之前定义的类型创建一个同义名称。
- C++11 添加了关键字 `using`，作为创建类型别名的另一种机制。

### 第 22.5 节 按位运算符

- `bitwise AND operator (&; p. 905)` 接受两个整型操作数。如果两个操作数中对应的位都为 1，则结果中的相应位被设置为 1。
- `Masks (p. 907)` 与按位 AND 一起使用，可以隐藏某些位，同时保留其他位。
- `bitwise inclusive OR operator (|; p. 905)` 接受两个操作数。如果任一操作数中的对应位被设置为 1，则结果中的相应位被设置为 1。
- 除补码运算符之外，每个按位运算符都有相应的赋值运算符。
- `bitwise exclusive OR operator (^; p. 905)` 接受两个操作数。如果两个操作数中对应的位恰好有一个为 1，则结果中的相应位被设置为 1。
- `left-shift operator (<<; p. 905)` 将其左操作数的位向左移动由右操作数指定的位数。右侧空出的位将以 `zeros` 填充。
- `right-shift operator (>>; p. 905)` 将其左操作数的位向右移动由右操作数指定的位数。对无符号整数进行右移时，左侧空出的位将以零填充。有符号整数中空出的位可能以零或一填充。
- `bitwise complement operator (~; p. 905)` 接受一个操作数，并将其各个位取反——这会产生该操作数的一补码。
- 从 C++14 开始，你可以在源代码中包含二进制字面量。要实现这一点，请在由 1 和 0 组成的序列前加上 `0b` 或 `0B`。

### 第 22.6 节 位字段

- `Bit fields`（第 914 页）通过使用存储数据所需的最少位数来减少存储空间的使用。位字段成员必须声明为 `int` 或 `unsigned`。
- 声明位字段时，应在 `unsigned` 或 `int` 成员名称后跟一个冒号和位字段宽度。
- 位字段宽度必须是整数常量。
- 如果指定了位字段但未指定名称，则该字段会作为结构中的 `padding`（第 917 页）使用。
- `unnamed bit field with width 0`（第 917 页）会将下一个位字段对齐到新的机器字边界。

### 第 22.7 节 字符处理库

- 函数 `islower`（第 920 页）判断其参数是否为小写字母（`a–z`）。函数 `isupper`（第 920 页）判断其参数是否为大写字母（`A–Z`）。
- 函数 `isdigit`（第 918 页）判断其参数是否为数字（`0–9`）。
- 函数 `isalpha`（第 918 页）判断其参数是否为大写字母（`A–Z`）或小写字母（`a–z`）。
- 函数 `isalnum`（第 918 页）判断其参数是否为大写字母（`A–Z`）、小写字母（`a–z`）或数字（`0–9`）。
- 函数 `isxdigit`（第 918 页）判断其参数是否为十六进制数字（`A–F`、`a–f`、`0–9`）。
- 函数 `toupper`（第 920 页）将小写字母转换为大写字母。函数 `tolower`（第 920 页）将大写字母转换为小写字母。
- 函数 `isspace`（第 921 页）判断其参数是否为以下空白字符之一：`' '`（空格）、`\f`、`\n`、`\r`、`\t` 或 `\v`。
- 函数 `iscntrl`（第 921 页）判断其参数是否为控制字符，例如 `\t`、`\v`、`\f`、`\a`、`\b`、`\r` 或 `\n`。
- 函数 `ispunct`（第 921 页）判断其参数是否为除空格、数字或字母之外的打印字符。

