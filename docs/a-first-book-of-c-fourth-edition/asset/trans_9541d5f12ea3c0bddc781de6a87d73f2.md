

## 信息点
## 处理 C 字符串

C 字符串变量在声明后不能被赋新值。例如，如果 test 已被声明为 C 字符串，其声明语句为

```
char test[] = "abcd";
```

随后的赋值，例如 test = "efgh"，是无效的。

作为替代赋值，可以使用 strcpy() 函数，例如 strcpy(test, "efgh")。使用 strcpy() 的唯一限制是声明的数组大小不能被超过，在本例中为五个元素。尝试将更大的 C 字符串值复制到 test 中会导致复制操作溢出目标数组，从最后一个数组元素之后紧邻的内存区域开始。这种内存溢出会覆盖这些内存位置中的内容，并且通常在通过其合法标识符名称访问被覆盖区域时导致运行时崩溃。

使用 strcat() 函数时也会发生相同的问题。确保连接后的 C 字符串能够容纳在原始字符串中是你的责任。

当 C 字符串变量使用指针定义时会出现一种有趣的情况（参见第 15.3 节中的信息点）。在这些情况下，可以在声明语句之后进行赋值。

## 库函数

由于 C 字符串是数组，而 C++ 不提供数组的内置操作，例如数组赋值和关系比较，因此这些操作不适用于 C 字符串。然而，所有 C++ 编译器都包含大量的 C 字符串处理函数。它们有效地提供了 C 字符串赋值、比较和其他有用的 C 字符串操作。表 15.2 列出了最常见的 C 字符串库函数，它们以与所有 C++ 函数相同的方式调用。这些函数的声明位于标准头文件 cstring 中，必须在调用函数之前将其包含在你的程序中。

### 表 15.2 C 字符串库函数（需要头文件 cstring）

| 名称 | 描述 | 示例 |
|---|---|---|
| strcpy(stringVar, stringExp) | 将 stringExp 复制到 stringVar 中，包括 '\0'。 | strcpy(test, "efgh") |
| strcat(stringVar, stringExp) | 将 stringExp 追加到 stringVar 包含的字符串值的末尾。 | strcat(test, "there") |
| strlen(stringExp) | 返回字符串的长度。不包括 '\0' 在长度计数中。 | strlen("Hello World!") |

## 字符串作为字符数组

**表 15.2 — C 字符串库函数（需要头文件 `cstring`） （续）**

| 名称 | 描述 | 示例 |
|---|---|---|
| `strcmp(stringExp1,stringExp2)` | 比较 `stringExp1` 与 `stringExp2`。如果 `stringExp1 < stringExp2` 则返回负整数，如果 `stringExp1 == stringExp2` 则返回 0，如果 `stringExp1 > stringExp2` 则返回正整数。 | `strcmp("Bebop","Beehive")` |
| `strncpy(stringVar,stringExp,n)` | 将 `stringExp` 的最多 n 个字符复制到 `stringVar`。如果 `stringExp` 的字符少于 n 个，则用 `\0` 填充 `stringVar`。 | `strncpy(str1, str2, 5)` |
| `strncmp(stringExp1,stringExp2, n)` | 比较 `stringExp1` 与 `stringExp2` 的最多 n 个字符。返回的数值与 `strcmp()` 相同，基于比较的字符数。 | `strncmp("Bebop","Beehive",2)` |
| `strchr(stringExp, character)` | 定位字符串中字符的首次出现。返回该字符的地址。 | `strchr("Hello", 'l')` |
| `strtok(string1, character)` | 将 `string1` 解析为标记。返回包含在 `string1` 中的下一个字符序列，直到但不包括分隔符字符。 | `strtok("Hello there World!",' ')` |

表 15.2 中列出的前四个函数使用最频繁。`strcpy()` 函数将源 C 字符串表达式，即字符串字面量或 C 字符串变量的内容，复制到目标 C 字符串变量中。例如，在函数调用 `strcpy(string1, "Hello World!")` 中，源字符串字面量 "Hello World!" 被复制到目标 C 字符串变量 `string1` 中。类似地，如果源字符串是名为 `src_string` 的 C 字符串变量，则函数调用 `strcpy(string1, src_string)` 将 `src_string` 的内容复制到 `string1` 中。在这两种情况下，确保 `string1` 足够大以容纳源 C 字符串是程序员的责任（参见前面的信息点）。

`strcat()` 函数将字符串表达式追加到 C 字符串变量的末尾。例如，如果名为 `dest_string` 的 C 字符串变量的内容为 "Hello"，则函数调用 `strcat(dest_string, " there World!")` 的结果是将字符串值

"Hello there World!" 赋给 dest_string。与 strcpy() 函数一样，程序员有责任确保目标 C 字符串定义得足够大以容纳额外的连接字符。

strlen() 函数返回其 C 字符串参数中的字符数，但不包括终止的 NULL 字符。例如，函数调用 strlen("Hello World!") 返回的值为 12。

最后，可以使用 strcmp() 函数比较两个字符串表达式是否相等。此比较是逐字符进行的，其方式与第 14.1 节中对字符串类对象的描述相同。程序 15.5 在完整程序的上下文中使用了这些 C 字符串函数。

## 程序 15.5

```
#include <iostream>
#include <cstring>  // required for the string function library
using namespace std;
int main()
{
    const int MAXELS = 50;
    char string1[MAXELS] = "Hello";
    char string2[MAXELS] = "Hello there";
    int n;

    n = strcmp(string1, string2);

    if (n < 0)
        cout << string1 << " is less than " << string2 << endl;
    else if (n == 0)
        cout << string1 << " is equal to " << string2 << endl;
    else
        cout << string1 << " is greater than " << string2 << endl;

    cout << "\nThe length of string1 is " << strlen(string1)
         << " characters" << endl;
    cout << "The length of string2 is " << strlen(string2)
         << " characters" << endl;

    strcat(string1, " there World!");

    cout << "\nAfter concatenation, string1 contains "
         << "the string value\n" << string1
         << "\nThe length of this string is "
         << strlen(string1) << " characters" << endl;
```

```
```cpp
cout << "\nType in a sequence of characters for string2: ";
cin.getline(string2, MAXELS);

strcpy(string1, string2);

cout << "After copying string2 to string1, "
     << "the string value in string1 is:\n" << string2
     << "\nThe length of this string is "
     << strlen(string1) << " characters" << endl;

return 0;
}
```
```

以下是程序 15.5 生成的示例输出：

```
```text
Hello is less than Hello there

The length of string1 is 5 characters
The length of string2 is 11 characters

After concatenation, string1 contains the string value
Hello World!
The length of this string is 18 characters

Type in a sequence of characters for string2: It's a wonderful day
After copying string2 to string1, the string value in string1 is:
It's a wonderful day
The length of this string is 20 characters
```
```

## 字符处理函数

除了 C 字符串操作函数外，所有 C++ 编译器还包括先前在第 14.2 节中介绍并为方便起见在表 15.3 中重复的字符处理函数。这些函数的原型位于头文件 ctype 中，任何使用这些函数的程序都应包含该头文件。

**表 15.3** 字符库函数（需要头文件 string 和 cctype）

| 函数原型 | 描述 | 示例 |
|---|---|---|
| `int isalpha(charExp)` | 如果 charExp 求值为字母，则返回真（非零整数）；否则返回假（零整数） | `isalpha('a')` |

## 第 15 章
## 指针和 C 字符串库函数

**表 15.3** 字符库函数（需要头文件 `string` 和 `cctype`）  
*（续）*

| 函数原型 | 描述 | 示例 |
|---|---|---|
| `int isalnum(charExp)` | 如果 `charExp` 求值为字母或数字，则返回真（非零整数）；否则返回假（零整数） | `isalnum(key);` |
| `int isupper(charExp)` | 如果 `charExp` 求值为大写字母，则返回真（非零整数）；否则返回假（零整数） | `isupper('a')` |
| `int islower(charExp)` | 如果 `charExp` 求值为小写字母，则返回真（非零整数）；否则返回假（零整数） | `islower('a')` |
| `int isdigit(charExp)` | 如果 `charExp` 求值为数字（0 到 9），则返回真（非零整数）；否则返回假（零整数） | `isdigit('5')` |
| `int isascii(charExp)` | 如果 `charExp` 求值为 ASCII 字符，则返回真（非零整数）；否则返回假（零整数） | `isascii('a')` |
| `int isspace(charExp)` | 如果 `charExp` 求值为空格，则返回真（非零整数）；否则返回假（零整数） | `isspace(' ')` |
| `int isprint(charExp)` | 如果 `charExp` 求值为可打印字符，则返回真（非零整数）；否则返回假（零整数） | `isprint('a')` |

