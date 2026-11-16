

## 字符类型测试

字符类型测试在编程中出现的频率足够高，以至于它们已被纳入名为 ctype.h 的头文件中的标准 C 库中。使用此文件允许我们说：

```c
if(isdigit(c))
```

而不是

```c
if (c >= '0' && c <= '9')
```

或

```c
if (isupper(c))
```

而不是

```c
if (c >= 'A' && c <= 'Z')
```

要使用允许我们访问此库的 ctype.h 头文件，我们发出以下预处理器命令：

```c
#include <ctype.h>
```

这一行是发给 C 预处理器的命令，用于将一些标准定义包含到我们的编译中，以便 isdigit() 和 isupper() 等名称会被识别。

以下是可用库函数的列表：

- `int isalnum(int c);`
  c 是字母数字字符
  如果 c 是字母 (A-Z 或 a-z) 或数字 (0-9)，则返回非零值

- `int isalpha(int c);`
  c 是字母
  如果 c 是字母 (A-Z 或 a-z)，则返回非零值

- `int isascii(int c);`
  c 是 ASCII 字符（代码小于 0200 或 128）
  如果 c 的低序字节在范围 0-127 (0x00-0x7F) 内，则返回非零值

- `int iscntrl(int c);`
  c 是不可打印字符（小于 ' '）
  如果 c 是删除字符或普通控制字符 (0x7F 或 0x00-0x1F)，则返回非零值

- `int isdigit(int c);`
  c 是数字
  如果 c 是数字 (0-9)，则返回非零值

- `int isgraph(int c);`
  c 是图形字符
  如果 c 是打印字符，如 `isprint()`，但空格字符除外，则返回非零值

- `int islower(int c);`
  c 是小写字母
  如果 c 是小写字母，则返回非零值

- `int isprint(int c);`
  c 是可打印字符（包括空格）
  如果 c 是打印字符 (0x20-0x7E)，则返回非零值

- `int ispunct(int c);`
  c 是标点字符
  如果 c 是标点字符 (`iscntrl()` 或 `isspace()`)，则返回非零值

- `int isspace(int c);`
  c 是空白字符（空格、制表符、回车、换页或换行）
  如果 c 是空格、制表符、回车、换行、垂直制表符或换页 (0x09-0x0D, 0x20)，则返回非零值

- `int isupper(int c);`
  c 是大写字母
  如果 c 是大写字母，则返回非零值

- `int isxdigit(int c);`
  c 是十六进制数字
  如果 c 是十六进制数字 (0-9, A-F, a-f)，则返回非零值

- `int toascii(int c);`
  通过清除除低 7 位 (0-127) 之外的所有位，将整数 c 转换为 ASCII
  返回转换后的 c 的值

- `int tolower(int c);`
  将 c 转换为小写
  如果 c 是大写，则返回转换后的值；其他所有情况均保持不变

- `int toupper(int c);`
  将 c 转换为大写
  如果 c 是小写，则返回转换后的值；其他所有情况均保持不变

我们可以使用 ctype.h 库重写前面的程序：

```c
// ascii2.c

#include <stdio.h>
#include <ctype.h>

int main(void) {
    unsigned char c;

    for (c = 0; c < 127; ++c) {
        printf("%3d 0x%03x", c, c);
        if (isprint(c)) {
            printf(" '%c'", c);
        }
        if (isdigit(c)) {
            printf(" D");
        }
        if (isupper(c)) {
            printf(" UC");
        }
        if (islower(c)) {
            printf(" LC");
        }
        if (isalpha(c)) {
            printf(" L");
        }
        if (isalnum(c)) {
            printf(" AN");
        }
        if (isspace(c)) {
            printf(" S");
        }
        if (ispunct(c)) {
            printf(" P");
        }
        if (iscntrl(c)) {
            printf(" C");
        }
        printf("\n");
    }
    return 0;
}
```

## 以下是程序输出：

```
0 0x000 C
1 0x001 C
2 0x002 C
3 0x003 C
4 0x004 C
5 0x005 C
6 0x006 C
7 0x007 C
8 0x008 C
9 0x009 C
10 0x00a S C
11 0x00b S C
12 0x00c S C
13 0x00d S C
14 0x00e C
15 0x00f C
16 0x010 C
17 0x011 C
18 0x012 C
19 0x013 C
20 0x014 C
21 0x015 C
22 0x016 C
23 0x017 C
24 0x018 C
25 0x019 C
26 0x01a C
27 0x01b C
28 0x01c C
29 0x01d C
30 0x01e C
31 0x01f C
32 0x020 ' ' S
33 0x021 '!' P
34 0x022 '"' P
35 0x023 '#' P
36 0x024 '$' P
37 0x025 '%' P
38 0x026 '&' P
39 0x027 ''' P
40 0x028 '(' P
41 0x029 ')' P
42 0x02a '*' P
43 0x02b '+' P
44 0x02c ',' P
45 0x02d '-' P
46 0x02e '.' P
47 0x02f '/' P
```

| 十进制 | 十六进制 | 字符 | 标志 |
|-----|-----|------|-------|
| 48 | 0x030 | '0' | D AN |
| 49 | 0x031 | '1' | D AN |
| 50 | 0x032 | '2' | D AN |
| 51 | 0x033 | '3' | D AN |
| 52 | 0x034 | '4' | D AN |
| 53 | 0x035 | '5' | D AN |
| 54 | 0x036 | '6' | D AN |
| 55 | 0x037 | '7' | D AN |
| 56 | 0x038 | '8' | D AN |
| 57 | 0x039 | '9' | D AN |
| 58 | 0x03a | ':' | P |
| 59 | 0x03b | ';' | P |
| 60 | 0x03c | '<' | P |
| 61 | 0x03d | '=' | P |
| 62 | 0x03e | '>' | P |
| 63 | 0x03f | '?' | P |
| 64 | 0x040 | '@' | P |
| 65 | 0x041 | 'A' | UC L AN |
| 66 | 0x042 | 'B' | UC L AN |
| 67 | 0x043 | 'C' | UC L AN |
| 68 | 0x044 | 'D' | UC L AN |
| 69 | 0x045 | 'E' | UC L AN |
| 70 | 0x046 | 'F' | UC L AN |
| 71 | 0x047 | 'G' | UC L AN |
| 72 | 0x048 | 'H' | UC L AN |
| 73 | 0x049 | 'I' | UC L AN |
| 74 | 0x04a | 'J' | UC L AN |
| 75 | 0x04b | 'K' | UC L AN |
| 76 | 0x04c | 'L' | UC L AN |
| 77 | 0x04d | 'M' | UC L AN |
| 78 | 0x04e | 'N' | UC L AN |
| 79 | 0x04f | 'O' | UC L AN |
| 80 | 0x050 | 'P' | UC L AN |
| 81 | 0x051 | 'Q' | UC L AN |
| 82 | 0x052 | 'R' | UC L AN |
| 83 | 0x053 | 'S' | UC L AN |
| 84 | 0x054 | 'T' | UC L AN |
| 85 | 0x055 | 'U' | UC L AN |
| 86 | 0x056 | 'V' | UC L AN |
| 87 | 0x057 | 'W' | UC L AN |
| 88 | 0x058 | 'X' | UC L AN |
| 89 | 0x059 | 'Y' | UC L AN |
| 90 | 0x05a | 'Z' | UC L AN |
| 91 | 0x05b | '[' | P |
| 92 | 0x05c | '\\' | P |
| 93 | 0x05d | ']' | P |
| 94 | 0x05e | '^' | P |
| 95 | 0x05f | '_' | P |
| 96 | 0x060 | '\`' | P |
| 97 | 0x061 | 'a' | LC L AN |
| 98 | 0x062 | 'b' | LC L AN |
| 99 | 0x063 | 'c' | LC L AN |
| 100 | 0x064 | 'd' | LC L AN |
| 101 | 0x065 | 'e' | LC L AN |
| 102 | 0x066 | 'f' | LC L AN |
| 103 | 0x067 | 'g' | LC L AN |
| 104 | 0x068 | 'h' | LC L AN |
| 105 | 0x069 | 'i' | LC L AN |
| 106 | 0x06a | 'j' | LC L AN |
| 107 | 0x06b | 'k' | LC L AN |
| 108 | 0x06c | 'l' | LC L AN |
| 109 | 0x06d | 'm' | LC L AN |
| 110 | 0x06e | 'n' | LC L AN |
| 111 | 0x06f | 'o' | LC L AN |
| 112 | 0x070 | 'p' | LC L AN |
| 113 | 0x071 | 'q' | LC L AN |
| 114 | 0x072 | 'r' | LC L AN |
| 115 | 0x073 | 's' | LC L AN |
| 116 | 0x074 | 't' | LC L AN |
| 117 | 0x075 | 'u' | LC L AN |
| 118 | 0x076 | 'v' | LC L AN |
| 119 | 0x077 | 'w' | LC L AN |
| 120 | 0x078 | 'x' | LC L AN |
| 121 | 0x079 | 'y' | LC L AN |
| 122 | 0x07a | 'z' | LC L AN |
| 123 | 0x07b | '{' | P |
| 124 | 0x07c | '\|' | P |
| 125 | 0x07d | '}' | P |
| 126 | 0x07e | '~' | P |
| 127 | 0x07f | | C |

## 自增和自减运算符

自增和自减是一元运算符（即，只需要一个操作数）：

```
++ adds one to its operand
-- subtracts one from its operand
```

语句：

```c
++num;
num++;
```

都将 num 的值加 1，并且与语句的效果相同：

```c
num = num + 1;
```

语句：

```c
--num;
num--;
```

都将 num 的值减 1，并且与语句的效果相同：

```c
num = num - 1;
```

请注意，当 ++ 或 -- 运算符用于操作数的左侧时：

```c
++num;
--num;
```

它被称为运算符的 *前缀* 形式。当 ++ 或 -- 运算符用于操作数的右侧时，它被称为运算符的 *后缀* 形式。

当自增或自减运算符仅用于操作数时，表达式的前缀形式和后缀形式没有区别。但是，当自增或自减运算符用于较大表达式的上下文中时，使用运算符的前缀或后缀形式可能会产生非常不同的结果。

例如，检查前缀自增运算符的用法：

```c
y = 10;
x = ++y;
```

最初，变量 y 被初始化为 10。在第二个语句中，我们使用自增运算符的前缀形式。首先，y 的值递增到 11，然后该新的 y 值用于表达式的其余部分，即，y 的新值 (11) 然后被赋给 x。因此，在执行这两个语句后，x 和 y 都等于 11。

现在让我们检查后缀自增运算符的用法：

```c
y = 10;
x = y++;
```

在这里，y 的初始值也是 10。但在第二个语句中，在 y 递增之前，其当前值 (10) 用于表达式，即，x 被赋值为 10。然后 y 的值递增到 11。因此，在执行这两个语句后，x 的值为 10，y 的值为 11！

