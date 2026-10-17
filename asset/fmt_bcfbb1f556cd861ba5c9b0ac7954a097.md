
字符串 `"51.2 are admitted"` 转换为 `double` 值 `51.2`，以及字符串 `" are admitted`

# 图 22.31 | 字符串转换函数 `strtod`。

函数 `strtol`（图 22.32）将表示整数的字符字符串转换为 `long`。该函数接收一个字符串（`char*`）、一个 `char*` 指针的地址和一个整数。该字符串包含字符串的序列部分。第二个参数被赋值为字符串转换部分之后的第一个字符的位置。第 11 行表示 `x` 被赋值为从字符串转换来的 `long` 值，且 `remainderPtr` 被赋值为 `string1` 中转换后的值（`-1234567`）之后的第一个字符的位置。使用空指针作为第二个参数，则会忽略字符串的剩余部分。第三个参数 `0` 表示要转换的值可以是任意基数（基数 `8`）、十进制（基数 `10`）。这由初始字符决定——`0` 表示十六进制，`1` 到 `9` 的数字表示十进制。

```cpp
// Fig 22.32: fig22_32.cpp
// Using strtol
#include <iostream>
#include <cstdlib> // strtol prototype
using namespace std;
int main() {
    const char* string1="-1234567abc";
    char* remainderPtr=nullptr;
    long x=strtol(string1,&remainderPtr); // convert to long
    cout << "The original string is \"" << string1
         << "\nThe converted value is \"" << x
         << "\nremainder of the original string is \"" << remainderPtr
         << "\nThe converted value plus 123 is " << x + 123 << endl;
}
```

**字符串转换函数 `strtol`。（第 2 部分，共 2 部分。）**

原始字符串是 `"-1234567abc"`
转换后的值是 `"-1234567"`
原始字符串的剩余部分是 `"abc"`
转换后的值加上 `123` 是 `-1234444`

## 22.10 搜索函数（第 2 部分，共 2 部分）

原始字符串是 `"-1234567abc"`
转换后的值是 `"-1234567"`
原始字符串的剩余部分是 `"abc"`
转换后的值加上 `123` 是 `-1234444`

## 22.10 字符串处理库中的搜索函数

原始字符串是 `"-1234567abc"`
转换后的值是 `"-1234567"`
原始字符串的剩余部分是 `"abc"`
转换后的值加上 `123` 是 `-1234444`

## 22.10 字符串处理库中的搜索函数（第 2 部分，共 2 部分。）

本节介绍了用于搜索字符和其他字符串的字符串处理库函数。这些函数总结在图 22.34 中。`strspn` 和 `strcsp` 返回 `size_t`。`size_t` 是一种由标准返回的类型定义的类型。

| 原型 | 描述 |
|---|---|
| `char* strchr(const char* s, int c)` | 在字符串 `s` 中定位字符 `c` 首次出现的位置。如果找到，返回指向 `c` 的指针。否则，返回空指针。 |
| `char* strchr(const char* s, int c)` | 从字符串 `s` 的末尾开始搜索并在 `s` 中定位字符 `c` 最后出现的位置。如果找到，返回指向 `s` 中 `c` 的指针。否则，返回空指针。 |
| `size_t strcsp(const char* s1, const char* s2)` | 确定并返回 `s1` 中仅由 `s2` 字符起始部分的长度 |
| `char* strbrk(const char* s1, const char* s2)` | 在 `s1` 中定位 `s2` 中任意字符首次出现的位置。如果找到 `s2` 中的字符，返回指向 `s1` 中该字符的指针。否则，返回空指针。 |
| `size_t strcspn(const char* s1, const char* s2)` | 确定并返回 `s1` 中不包含字符串 `s2` 的起始部分的长度。 |
| `char* strstr(const char* s1, const char* s2)` | 在 `s1` 中定位字符串 `s2` 首次出现的位置。如果找到该字符串，返回 `s1` 中该字符串的指针。否则，返回空指针。 |

图 22.34 | C 字符串处理库中的搜索函数。

函数 `strchr` 在字符串中搜索字符的首次出现的位置。如果找到

# 第 22 章 位、字符、C 字符串与结构体

```cpp
// 图 22.35: fig22_35.cpp
// 使用 strchr。
#include <iostream>
#include <cstring> // strchr 原型声明
using namespace std;
int main() {
    const char* string1="This is a test";
    char character1='a';
    char character2='z';
    // 在 string1 中搜索字符1
    if (strchr(string1, character1) != NULL) {
        cout << "" << character1 << "' was found in \"""
    } else {
        cout << "" << character1 << "' was not found in \"""
    }
    // 在 string1 中搜索字符2
    if (strchr(string1, character2) != NULL) {
        cout << "" << character2 << "' was found in \"""
    } else {
        cout << "" << character2 << "' was not found in \""" << endl;
    }
}
```

在 `"This is a test"` 中找到了 `'a'`。
在 `"This is a test"` 中没有找到 `'z'`。

图 22.35 | 字符串搜索函数 `strchr`。

函数 `strcspn`。22.36，第 14 行确定第一个参数字符串中起始部分的长度，该部分不包含第二个参数字符串中的任何字符。该函数返回该段的长度。

```cpp
// 图 22.36: fig22_36.cpp
// 使用 strcspn。
#include <iostream>
#include <cstring> // strcspn 原型声明
using namespace std;
int main() {
    const char* string1="The value is 3.14159";
    const char* string2="1234567890";
}
```

图 22.36 | 字符串搜索函数 `strcspn`（2 部分中的第1 部分）。

## 22.10 C 字符串处理库的搜索函数

```cpp
10
11 cout << "\nstring1 = " << string1 << "\nstring2 = " << string2
12 << "\nThe length of the initial segment of string1"
13 << "\ncontaining no characters from string2 = "
14 << strcspn(string1, string2) << endl;
15 }
```

`string1` = The value is 3.14159
`string2` = 1234567890

`string1` 中不包含 `string2` 字符的起始段长度 = 13

**图 22.36 | 字符串搜索函数 `strcspn`（2 部分中的第2 部分）。**

函数 `strbrk` 在其第一个参数中搜索其第二个参数中任意字符的首次出现位置。如果找到了第二个参数中的字符，`strbrk` 返回指向第一个参数中该字符的指针；否则，`strbrk` 返回空指针。图 22.37 的第 12 行确定了 `string1` 中来自 `string2` 的任意字符的首次出现位置。

```cpp
1 // 图 22.37: fig22_37.cpp
2 // 使用 strbrk
3 #include <iostream>
4 #include <cstring> // strbrk 原型声明
5 using namespace std;
6
7 int main() {
8 const char* string1{"This is a test"};
9 const char* string2{"beware"};
10
11 cout << "\Of the characters in \"" << string2 << " \"\n'"
12 << strbrk(string1, string2) << "' is the first character"
13 << " to appear in \n\"" << string1 << "\'" << endl;
14 }
```

`"beware"` 中的字符
`'a'` 是在 `"This is a test"` 中出现的第一个字符

**图 22.37 | 字符串搜索函数 `strbrk`。**

函数 `strchr` 在字符串中搜索指定字符的最后一次出现位置。如果找到了该字符，`strchr` 返回指向字符串中该字符的指针；否则，`strchr` 返回 `0`。图 22.38 的第 14 行在字符串 `"A zoo has many animals including zebras"` 中搜索字符 `'z'` 的最后一次位置。

```cpp
// 图 22.38: fig22_38.cpp
// 使用 strchr。
#include <iostream>
#include <cstring> // strchr 原型声明
using namespace std;
int main() {
    const char* string1="A zoo has many animals including zebras";
    char c = 'z';
    cout << "string1 = " << string1 << "\n";
    cout << "The remainder of string1 beginning with\n";
    cout << "last occurrence of character is: " << strchr(string1, c) << endl;
}
```

`string1` = A zoo has many animals including zebras
`string1` 从字符 `'z'` 最后一次出现开始的剩余部分是: `"zebras"`

图 22.38 | 字符串搜索函数 `strchr`。

函数 `strcspn` (22.39，第 14 行)确定第一个参数字符串中起始部分的长度，该部分不包含第二个参数字符串中的任何字符。该函数返回该段的长度。

```cpp
// 图 22.39: fig22_39.cpp
// 使用 strcspn。
#include <iostream>
#include <cstring> // strcspn 原型声明
using namespace std;
int main() {
    const char* string1="The value is 3.14159";
    const char* string2="1234567890";
}
```

## 22.11 C 字符串处理库的内存函数

```
9 // 总共 17 个字符（包括终止空字符）
10 char s2[]{"Copy this string"};
12
13 memcpy(s1, s2, 17); // 将 s2 的 17 个字符拷贝到 s1
14
15 cout << "After s2 is copied into s1 with memcpy,\n"
16 << "s1 contains " << s1 << "\n" << endl;
17 }
```

用 `memcpy` 将 `s2` 拷贝到 `s1` 后，
`s1` 包含 `"Copy this string"`

图22.42 | 内存处理函数内存（部分 2/2）

函数 `memmove` 与 `memcpy` 一样，从其第二个参数指向的对象将指定数量的字节拷贝到其第一个参数指向的对象。拷贝的执行方式就像先将字节从第二个参数拷贝到一个临时字符数组，然后从临时数组拷贝到第一个参数。这允许将字符串的某部分的字符拷贝到字符串的另一部分。

## 常见编程错误 22.11

> 除 `memmove` 以外的其他拷贝字符的字符串处理函数在同一字符串的不同部分之间拷贝时，结果是未定义的。

22.43 中的程序使用 `memmove`（第 12 行）将数组 `x` 的后 10 个字节拷贝到数组 `x` 的前 10 个字节。

```
1 // 图 22.43: fig22_43.cpp
2 // 使用 memmove。
3 #include <iostream>
4 #include <cstring> // 内存原型
5 using namespace std;
6
7 int main() {
8 char x[]="Home Sweet Home";
9 cout << "The string in array after memmove: " << x << endl;
10 cout << "\nThe string in array after memmove: " << endl;
11 << << static_cast<char*>(memmove(x, &x[5], 10)) << endl;
12 }
```

`memmove` 后数组中的字符串为: Sweet Home
`memmove` 后数组中的字符串为: Sweet Home

图22.43 | 内存处理函数 `memmove`。

## `memcmp`（图 22.44，第 13–15 行）将其第一个参数的指定数量字符与第二个参数的对应字符进行比较。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_981_0.png)

如果第一个参数大于第二个参数，函数返回大于零的值；如果参数相等，返回零；如果第一个参数小于第二个参数，则返回小于零的值。[注意：在某些编译器中，函数 `memcmp` 返回 0 或 1，如图22.44 的示例输出所示。在其他编译器中，此函数返回 0 或所比较字符串中第一个不同字符的数值代码差；当比较 `s1` 和 `s2` 时，它们第一个不同的字符是每个字符串的第五个字符——s1 为 E（数值代码为 69），s2 为 X，返回值为 19（当 s2 与 s1 比较时为负）。]

```cpp
// 图 22.44: fig22_44.cpp
// 使用 memcmp。
#include <iostream>
#include <iomanip>
#include <string> // memcmp 原型
using namespace std;
int main() {
    char s1[] = "ABCDEFG";
    char s2[] = "ABCDXYZ";
    cout << "s1 = " << s1 << "\ns2 = " << s2 << endl;
    cout << "\memcmp(s1, s2, 4) = " << setw(3) << memcmp(s1, s2, 4) << endl;
    cout << "\memcmp(s1, s2, 7) = " << setw(3) << memcmp(s1, s2, 7) << endl;
    cout << "\memcmp(s2, s1, 7) = " << setw(3) << memcmp(s2, s1, 7) << endl;
}
```

| s1 = s2, s2, 4 = 0 |
| memcmp(s1, s2, 7) = -1 |
| memcmp(s2, s1, 7) = 1 |

**图 22.44** | 内存处理函数 `memcmp`。

`memchr` 搜索字节的首次出现处

```cpp
// 图 22.45: fig22_45.cpp
// 使用 memchr。
#include <iostream>
#include <string> // memchr 原型
using namespace std;
```

**图 22.45** | 内存处理函数 `memchr`。（部分 1/2）。

## 22.12 总结

```
6
7 int main() {
8 char s[]="This is a string";
9
10 cout << "s = " << s << "\n" << endl;
11 cout << "The remainder of s after character 'r' is found is ""
12 << << static_cast<char*>(memchr(s, 'r', 16)) << "\"" << endl;
13 }
```
