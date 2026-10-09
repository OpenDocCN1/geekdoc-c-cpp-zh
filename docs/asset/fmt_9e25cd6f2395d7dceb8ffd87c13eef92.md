
```cpp
#include <iostream>

#include <cstdlib> // `atof` 原型

using namespace std;

int main() {

    double `d`=`atof`("99.0"); // 将字符串转换为 double

    cout << "The "99.0" converted to double is " << `d` / 2.0 << endl;

}
```

| 字符串 "99.0" 转换为 double 是 99
| 转换后的值除以 2 为 49.5 |

图 22.28 | 字符串转换函数 `atof`。

## 第 22 章 位、字符、C 字符串和结构体

```cpp
// Fig. 22.29: fig22_29.cpp
// 使用 `atoi`
#include <iostream>
#include <cstdlib> // `atoi` prototype
using namespace std;
int main() {
    int `i`=`atoi`("2593"); // 将字符串转换为 int
    cout << "string 2593 converted to int is " << `i` <<
         << "\nconverted value minus 593 is " << `i` - 593 << endl;
}
```

字符串 "2593" 转换为 int
转换后的值减去 593 为 2000

# 图 22.29 | 字符串转换函数 `atoi`。

函数 `atoi`（图 22.30, 第 8 行）将其参数——一个表示长整型（long）的数字字符串转换为 long。该函数返回 long 值。如果字符串无法转换，函数 `atoi` 返回零。如果 int 和 long 都存储在四个字节，则 `atoi` 和 `strtol` 的工作方式相同。

```cpp
// Fig. 22.30: fig22_30.cpp
// 使用 `atoi`。
#include <iostream>
#include <cstdlib> // `atoi` prototype
using namespace std;
int main() {
    long `x`=`atol`("1000000"); // 将字符串转换为 long
    cout << "The string \"1000000\" converted to long is " << `x` <<
         << "\nconverted value divided by 2 is " << `x` / 2 << endl;
}
```

字符串 "1000000" 转换为 long 为 1000000
转换后的值除以 2 为 500000

# 图 22.30 | 字符串转换函数 `atol`。

函数 `strtod`（图 22.31）将表示浮点值的字符序列转换为 double。函数 `strtod` 接受两个参数——一个字符串（`char*`）和一个 char 指针的地址（即 `char**`）。字符串包含要转换的字符序列。第二个参数允许 `strtod` 修改调用函数中的 `char*` 指针，使该指针指向字符串中转换部分之后第一个字符的位置。第 11 行表示 `d` 被赋值为从字符串转换的 double 值，而 `stringPtr` 被赋值为字符串中转换值（51.2）之后第一个字符的位置。

## 22.9 C 字符串转换函数

```cpp
// Fig. 22.31: fig22_31.cpp
// 使用 `strtod`。
#include <iostream>
#include <cstdlib> // `strtod` prototype
using namespace std;
int main() {
    const char* `string1`("51.2 are admitted");
    char* `stringPtr`(nullptr);
    double `d`=`strtod`(`string1`, &`stringPtr`); // 转换为 double
    cout << "The string " << `string1` << "\"";
    cout << " is converted to \"" << `d` << "\" << endl;
    cout << " and the string \"" << `stringPtr` << "\"" << endl;
}
```

字符串 "51.2 are admitted" 转换为 double 值 51.2，以及字符串 " are admitted"

图 22.31 | 字符串转换函数 `strtod`。

函数 `strtol`（图 22.32）将表示整数的字符序列转换为 long。该函数接收一个字符串（`char*`）、一个 `char*` 指针的地址和一个整数。字符串包含要转换的字符序列。第二个参数被赋值为字符串转换部分之后第一个字符的位置。该函数识别所转换值的基数，`remainderPtr` 被赋值为从字符串转换的 long 值的位置，并保持赋值为 `string1` 中转换值（-1234567）之后第一个字符的位置。对第二个参数使用空指针会导致字符串的剩余部分被忽略。第三个参数 0 表示该值可以在任何基数（8 进制、十进制（基数 10））下转换。这取决于字符串中的初始字符——0 表示八进制，0x 表示十六进制，1 到 9 之间的数字表示十进制。

```cpp
// Fig. 22.32: fig22_32.cpp
// 使用 `strtol`。
#include <iostream>
#include <cstdlib> // `strtol` prototype
using namespace std;
int main() {
    const char* `string1`("-1234567abc");
    char* `remainderPtr`(nullptr);
    long `x`=`strtol`(`string1`, &`remainderPtr`); // 转换为 long
}
```

图 22.32 | 字符串转换函数 `strtol`。（2 的第一部分）

```cpp
13 cout << "The original string is \"" << `string1`
14 << "\\nThe converted value is \"" << `x`
15 << "\nremainder of the original string is \"" << `remainderPtr`
16 << "\"\nThe converted value plus 567 is \"" << `x` + 567 << endl;
17 }
```

原始字符串为 "-1234567abc"
转换后的值为 -1234567
原始字符串的剩余部分为 "abc"
转换值加 567 为 -1234000

图 22.32 | 字符串转换函数 `strtol`。（2 的第二部分）

在调用 `strtol` 时，基数可以指定为 0 或十六进制（详细解释参见附录）。第三个参数 0 表示该值可以在任何基数（8 进制、十进制（基数 10））下转换。这取决于字符串中的初始字符——0 表示八进制，0x 表示十六进制，1 到 9 之间的数字表示十进制。该函数识别所转换值的基数，`remainderPtr` 被赋值为从字符串转换的 long 值的位置，并保持赋值为转换值之后第一个字符的位置。对第二个参数使用空指针会导致字符串的剩余部分被忽略。第二个参数允许 `strtol` 修改调用函数中的指针，使该指针指向字符串转换部分之后第一个字符的位置。

```cpp
// Fig. 22.33: fig22_33.cpp
// 使用 `strtol`。
#include <iostream>
#include <cstdlib> // `strtol` prototype
using namespace std;
int main() {
    const char* `string1`="-1234567abc";
    char* `remainderPtr`(nullptr);
    long `x`=`strtol`(`string1`, &`remainderPtr`, 0); // 转换为 long
    cout << "The original string is \"" << `string1`
         << "\\nThe converted value is \"" << `x`
         << "\nremainder of the original string is \"" << `remainderPtr`
         << "\"\nThe converted value plus 567 is \"" << `x` + 567 << endl;
}
```

图 22.33 | 字符串转换函数 `strtol`。

## 2.10 C 处理库的搜索函数

本节介绍了用于在字符串中搜索字符的函数。这些函数在 22.34 中总结。`strcspn` 和 `strnspn` 返回 `size_t`。

| 原型 | 说明 |
|---|---|
| `char* strchr(const char* s, int c)` | 在字符串 `s` 中定位字符 `c` 的首次出现。如果找到，返回 `c` 的指针；否则返回空指针。 |
| `char* strrchr(const char* s, int c)` | 从字符串 `s` 的结尾搜索并定位字符 `c` 的最后出现。如果找到，返回 `s` 中 `c` 的指针；否则返回空指针。 |
| `size_t strcspn(const char* s1, const char* s2)` | 确定并返回字符串 `s1` 中由 `s2` 字符组成的起始部分的长度。 |
| `char* strpbrk(const char* s1, const char* s2)` | 在字符串 `s1` 中定位 `s2` 中任意字符的首次出现。如果找到字符，返回 `s1` 中该字符的指针；否则返回空指针。 |
| `size_t strnspn(const char* s1, const char* s2)` | 确定并返回字符串 `s1` 中由不包含在 `s2` 中的字符组成的起始部分的长度。 |
| `char* strstr(const char* s1, const char* s2)` | 在字符串 `s1` 中定位字符串 `s2` 的首次出现。如果找到，返回 `s1` 中该字符串的指针；否则返回空指针。 |

图 22.34 | C 字符串处理库的搜索函数。

## 976 第22章 位、字符、C 字符串和结构体

```cpp
// 图 22.35: fig22_35.cpp
// 使用 `strchr`。
#include <iostream>
#include <cstring> // `strchr` 原型
using namespace std;
int main() {
    const char* `string1`="This is a test";
    char `character1`[]={'a'};
    char `character2`[]={'z'};
    // 在 `string1` 中搜索字符1
    if (`strchr`(`string1`, `character1`) != NULL) {
        cout << "\"" << `character1` << "\" was found in " << endl;
    } else {
        cout << "\"" << `character1` << "\" was not found in " << endl;
    }
    // 在 `string1` 中搜索字符2
    if (`strchr`(`string1`, `character2`) != NULL) {
        cout << "\"" << `character2` << "\" was found in " << endl;
    } else {
        cout << "\"" << `character2` << "\" was not found in " << endl;
    }
}
```

'a' was found in "This is a test".
'z' was not found in "This is a test".

图 22.35 | 字符串搜索函数 `strchr`。

函数 `strcspn` 22.36, 第 14 行确定了第一个参数字符串开头部分的长度，该部分不包含第二个参数字符串中的任何字符。该函数返回该片段的长度。

```cpp
// 图 22.36: fig22_36.cpp
// 使用 `strcspn`。
#include <iostream>
#include <cstring> // `strcspn` 原型
using namespace std;
int main() {
    const char* `string1`="The value is 3.14159";
    const char* `string2`="1234567890";
}
```

图 22.36 | 字符串搜索函数 `strcspn`。（2部分中的第1部分）。

## 22.10 C 字符串处理库的搜索函数

```cpp
10 cout << "\nstring1 = " << `string1` << "\nstring2 = " << `string2`
12 << "\nThe length of the initial segment of string1"
13 << "\nnot containing, no characters from string2 = "
14 << `strcspn`(`string1`, `string2`) << endl;
15 }
```

string1 = The value is 3.14159
string2 = 1234567890

string1 的开头不包含来自 string2 任何字符的片段长度 = 13

图 22.36 | 字符串搜索函数 `strcspn` （2部分中的第2部分。）

函数 `strpbrk` 在其第一个字符串参数中搜索其第二个参数中字符的第一次出现的位置。如果找到了第二个参数中的字符，`strpbrk` 返回指向第一个参数中该字符的指针；否则，`strpbrk` 返回空指针。图 22.37 的第 12 行确定了 `string1` 中任何来自 `string2` 字符的首次出现位置。

```cpp
1 // 图 22.37:fig22_37.cpp
2 // 使用 `strpbrk`
3 #include <iostream>
4 #include <string> // `strpbrk`
5 using namespace std;
7 int main() {
8 const char* `string1`{"This is a test"};
9 const char* `string2`{"beware"};
11 cout << "\"Of the characters in \"" << `string2` << "\"\n'"
12 << `strcspn`(`string1`, `string2`) << "\' is the first character"
13 << "to appear in\n\"" << `string1` << '\'' << endl;
14 }
```

"beware" 中的字符
'a' 是在 "This is a test" 中首次出现的字符

图 22.37 | 字符串搜索函数 `strpbrk`。

函数 `strchr` 用于查找字符串中指定字符的最后一次出现位置。
如果找到了该字符，`strchr` 返回指向字符串中该字符的指针；否则，`strchr` 返回 0。图 22.38 的第 14 行在字符串 "A zoo has many zebras" 中搜索 'z' 的最后一次出现位置。

## 第22章 位、字符、C 字符串和结构体

```cpp
// 图 22.38: fig22_38.cpp
// 使用 `strchr`。
#include <iostream>
#include <cstring> // `strchr` 原型
using namespace std;
int main() {
    const char* `string1`="A zoo has many zebras";
    char `c` = 'z';
    cout << "string1 = " << `string1` << "\n";
    cout << "The remainder of string1 beginning with\n";
    cout << "last occurrence of character " << `c` << " is:" << `strchr`(`string1`, `c`) << endl;
}
```

string1 = A zoo has many zebras
The remainder of string1 beginning with
occurrence of character 'z' is: "zebras"

图 22.38 | 字符串搜索函数 `strchr`。

函数 `strcspn`（图 22.39, 第 14 行）确定了第一个参数字符串开头部分的长度，该部分仅包含来自第二个参数字符串的字符。该函数返回该片段的长度。

```cpp
// 图 22.39: fig22_39.cpp
// 使用 `strcspn`。
#include <iostream>
#include <cstring> // `strcspn` 原型
using namespace std;
int main() {
    const char* `string1`="The value is 3.14159";
    const char* `string2`="1234567890";
}
```
