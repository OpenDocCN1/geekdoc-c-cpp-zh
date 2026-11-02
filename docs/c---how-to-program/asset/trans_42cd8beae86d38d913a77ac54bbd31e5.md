

### 错误预防提示 8.1

在字符数组中存储字符串时，请确保数组足够大，能够容纳将要存储的最长字符串。C 语言允许存储任意长度的字符串。如果要存储的字符串比存储它的字符数组更长，超出数组末尾的字符将覆盖数组中该数组之后的内存数据。

可以使用 `scanf` 将字符串存储到数组中。例如，下面的语句把字符串存储到字符数组 `word[20]` 中：

```c
scanf("%19s", word);
```

用户输入的字符串被存储在 `word` 中。变量 `word` 是数组，而数组名本质上是指针，因此实参 `word` 前不需要 `&`。回顾 6.5.4 节可知，函数 `scanf` 会一直读取字符，直到遇到空格、制表符、换行符或文件结束指示符为止。因此，如果在转换说明符 `%19s` 中没有字段宽度 19，用户输入就可能超过 19 个字符，程序甚至可能会崩溃！出于这个原因，使用 `scanf` 读入字符数组时，应始终指定字段宽度。上述语句中的字段宽度 19 可确保 `scanf` 最多读取 19 个字符，并保留数组中的最后一个位置用于存放字符串的终止空字符。这可以防止 `scanf` 把字符写入字符数组末尾之外的内存。（若要读取任意长度的输入行，可以使用非标准但被广泛支持的 `readline` 函数，它通常包含在 `stdio.h` 中。）字符数组若要按字符串正确打印，则必须包含终止空字符。

### 常见编程错误 8.3

把单个字符当作字符串处理。字符串是指针，通常可能是一个相当大的整数。然而，字符是一个较小的整数（ASCII 值的范围为 0–255）。在许多系统上，这会导致错误，因为低内存地址被保留用于特殊用途，例如操作系统中断处理程序，因此会发生“访问冲突”。

### 常见编程错误 8.4

将字符作为实参传递给期望字符串的函数（反之亦然）属于编译错误。

## 8.3 字符处理库

字符处理库 `<ctype.h>` 包含若干函数，它们可以对字符数据执行有用的测试和操作。每个函数都以 `unsigned char`（表示为 `int`）或 `EOF` 作为实参。正如第 4 章所述，字符经常作为整数来处理，因为在 C 语言中，字符是一个单字节整数。`EOF` 通常的值为 –1。图 8.1 汇总了字符处理库中的函数。

| 原型 | 函数说明 |
|---|---|
| `int isblank(int c);` | 如果 c 是划分文本行中单词的空白字符，则返回真值，否则返回 0（假）。[注意：此函数在 Microsoft Visual C++ 中不可用。] |
| `int isdigit(int c);` | 如果 c 是数字，则返回真值，否则返回 0（假）。 |
| `int isalpha(int c);` | 如果 c 是字母，则返回真值，否则返回 0（假）。 |
| `int isalnum(int c);` | 如果 c 是数字或字母，则返回真值，否则返回 0（假）。 |
| `int isxdigit(int c);` | 如果 c 是十六进制数字字符，则返回真值，否则返回 0（假）。（有关二进制数、八进制数、十进制数和十六进制数的详细解释，请参阅附录 C。） |
| `int islower(int c);` | 如果 c 是小写字母，则返回真值，否则返回 0（假）。 |
| `int isupper(int c);` | 如果 c 是大写字母，则返回真值，否则返回 0（假）。 |
| `int tolower(int c);` | 如果 c 是大写字母，则 `tolower` 返回对应的小写字母；否则，`tolower` 原样返回实参。 |
| `int toupper(int c);` | 如果 c 是小写字母，则 `toupper` 返回对应的大写字母；否则，`toupper` 原样返回实参。 |
| `int isspace(int c);` | 如果 c 是空白字符——换行符（`'\n'`）、空格（`' '`）、换页符（`'\f'`）、回车符（`'\r'`）、水平制表符（`'\t'`）或垂直制表符（`'\v'`）——则返回真值，否则返回 0（假）。 |
| `int iscntrl(int c);` | 如果 c 是控制字符——水平制表符（`'\t'`）、垂直制表符（`'\v'`）、换页符（`'\f'`）、响铃符（`'\a'`）、退格符（`'\b'`）、回车符（`'\r'`）、换行符（`'\n'`）等——则返回真值，否则返回 0（假）。 |
| `int ispunct(int c);` | 如果 c 是除空格、数字或字母之外的可打印字符——如 `$`、`#`、`(`、`)`、`[`、`]`、`{`、`}`、`:`、`;` 或 `%`——则返回真值，否则返回 0。 |
| `int isprint(int c);` | 如果 c 是可打印字符（即在屏幕上可见的字符），包括空格，则返回真值，否则返回 0（假）。 |
| `int isgraph(int c);` | 如果 c 是除空格之外的可打印字符，则返回真值，否则返回 0（假）。 |

**图 8.1** | 字符处理库（`<ctype.h>`）的函数。

### 8.3.1 函数 isdigit、isalpha、isalnum 和 isxdigit

图 8.2 演示了 `isdigit`、`isalpha`、`isalnum` 和 `isxdigit` 函数。函数 `isdigit` 确定其实参是否为数字（0–9）。函数 `isalpha` 确定其实参是否为大写字母（A–Z）或小写字母（a–z）。函数 `isalnum` 确定其实参是否为大写字母、小写字母或数字。函数 `isxdigit` 确定其实参是否为十六进制数字（A–F、a–f、0–9）。

```c
// Fig. 8.2: fig08_02.c
// Using functions isdigit, isalpha, isalnum, and isxdigit
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    printf("%s\n%s%s\n%s%s\n", "According to isdigit: ",
        isdigit('8') ? "8 is a " : "8 is not a ", "digit",
        isdigit('#') ? "# is a " : "# is not a ", "digit");

    printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n",
        "According to isalpha:",
        isalpha('A') ? "A is a " : "A is not a ", "letter",
        isalpha('b') ? "b is a " : "b is not a ", "letter",
        isalpha('&') ? "& is a " : "& is not a ", "letter",
        isalpha('4') ? "4 is a " : "4 is not a ", "letter");

    printf("%s\n%s%s\n%s%s\n%s%s\n",
        "According to isalnum:",
        isalnum('A') ? "A is a " : "A is not a ",
        "digit or a letter",
        isalnum('8') ? "8 is a " : "8 is not a ",
        "digit or a letter",
        isalnum('#') ? "# is a " : "# is not a ",
        "digit or a letter");

    printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n%s%s\n",
        "According to isxdigit:",
        isxdigit('F') ? "F is a " : "F is not a ",
        "hexadecimal digit",
        isxdigit('J') ? "J is a " : "J is not a ",
        "hexadecimal digit",
        isxdigit('7') ? "7 is a " : "7 is not a ",
        "hexadecimal digit",
        isxdigit('$') ? "$ is a " : "$ is not a ",
        "hexadecimal digit",
        isxdigit('f') ? "f is a " : "f is not a ",
        "hexadecimal digit");
}
```

**图 8.2** | 使用函数 isdigit、isalpha、isalnum 和 isxdigit。（第 1 部分，共 2 部分。）

```text
According to isdigit:
8 is a digit
# is not a digit

According to isalpha:
A is a letter
b is a letter
& is not a letter
4 is not a letter

According to isalnum:
A is a digit or a letter
8 is a digit or a letter
# is not a digit or a letter

According to isxdigit:
F is a hexadecimal digit
J is not a hexadecimal digit
7 is a hexadecimal digit
$ is not a hexadecimal digit
f is a hexadecimal digit
```

**图 8.2** | 使用函数 isdigit、isalpha、isalnum 和 isxdigit。（第 2 部分，共 2 部分。）

图 8.2 使用条件运算符（?）确定在测试每个字符时，输出中应打印字符串 `" is a "` 还是 `" is not a "`。例如，表达式

```c
isdigit('8') ? "8 is a " : "8 is not a "
```

表示如果 `'8'` 是数字，则打印字符串 `"8 is a "`；如果 `'8'` 不是数字（即 `isdigit` 返回 0），则打印字符串 `"8 is not a "`。

### 8.3.2 函数 islower、isupper、tolower 和 toupper

图 8.3 演示了 `islower`、`isupper`、`tolower` 和 `toupper` 函数。函数 `islower` 确定其实参是否为小写字母（a–z）。函数 `isupper` 确定其实参是否为大写字母（A–Z）。函数 `tolower` 将大写字母转换为小写字母并返回该小写字母。如果实参不是大写字母，则 `tolower` 原样返回实参。函数 `toupper` 将小写字母转换为大写字母并返回该大写字母。如果实参不是小写字母，则 `toupper` 原样返回实参。

```c
// Fig. 8.3: fig08_03.c
// Using functions islower, isupper, tolower and toupper
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n",
        "According to islower:",
        islower('p') ? "p is a " : "p is not a ",
        "lowercase letter",
        islower('P') ? "P is a " : "P is not a ",
        "lowercase letter",
        islower('5') ? "5 is a " : "5 is not a ",
        "lowercase letter",
        islower('!') ? "! is a " : "! is not a ",
        "lowercase letter");

    printf("%s\n%s%s\n%s%s\n%s%s\n%s%s\n\n",
        "According to isupper:",
        isupper('D') ? "D is an " : "D is not an ",
        "uppercase letter",
        isupper('d') ? "d is an " : "d is not an ",
        "uppercase letter",
        isupper('8') ? "8 is an " : "8 is not an ",
        "uppercase letter",
        isupper('$') ? "$ is an " : "$ is not an ",
        "uppercase letter");

    printf("%s%c\n%s%c\n",
        "u converted to uppercase is ", toupper('u'),
        "7 converted to uppercase is ", toupper('7'));
}
```

**图 8.3** | 使用函数 islower、isupper、tolower 和 toupper。（第 1 部分，共 2 部分。）

