
`strng2` 的前四个字符被拼接到 `strng1` 的值中，生成的字符串存储在 `strng1` 中。

拼接前的字符串：

| strng1 |
| C | O | M | P | U | T | E | R | \0 | | | | | | |

| strng2 |
| S | C | I | E | N | C | E | \0 | | | | | | | |

拼接后的字符串：

| strng1 |
| C | O | M | P | U | T | E | R | S | C | I | E | \0 | | | | | | |

| strng2 |
| S | C | I | E | N | C | E | \0 | | | | | | |

注意，`strng2` 的前四个字符被拼接到 `strng1`，结果存储在 `strng1` 中，末尾带有空终止符。

以下代码拼接了四个单词以构造一个句子。

```c
#include <stdio.h>
#include <string.h>
#define STRLNG 80

int main()
{
    char result[STRLNG] = "";
    char word[STRLNG];
    int i;

    for(i = 0; i < 4; i++)
    {
        gets(word);
        strcat(result, word);
        strcat(result, " ");
    }
    printf("\n%s\n\n", result);
}
```

# 输入与输出

- Computers输入
- Computers结果
- are输入
- Computers结果
- 电子输入
- Computers是电子结果
- 机器输入
- Computers是电子机器。最终结果

输入字符串和拼接后的字符串通过回车交替显示。开始时结果包含一个空字符串。最终生成的字符串是 "Computers are electronic machines."。在构造句子时，必须在每个字符串的结尾或开头包含空格，以便在单词之间留空。此程序可以通用化拼接任意数量的单词以构造句子。

## 9.4.4 字符串比较

在 C 中，字符在内部机器码中用数字表示，这些数字的选择遵循 A < B < C < D，大写字母在小写字母之前以此此类推。大多数计算机使用 ASCII 或 EBCDIC 编码。因此，可以通过比较它们的数字表示来对字符串进行等价、差异或字母顺序的比较。这是通过使用 `string.h` 库中的字符串比较函数实现的。有两个字符串函数：`strcmp()` 和 `strncmp()`。

`strcmp()` 函数有两个参数并返回一个整数，如下：

```c
int k;
k = strcmp(strng1, strng2);
```

在这种情况下，字符串 `strng1` 和 `strng2` 逐字符比较。当发现不相等的字符时，确定两个字符串的顺序。根据两个字符串的顺序，比较产生以下结果：

- k > 0 正数，strng1 在 strng2 之后
- k = 0 正数，strng1 与 strng2 相同
- k < 0 负数，strng1 在 strng2 之前

# 以下示例展示了 `strcmp()` 函数的使用：

```c
int k;
strng1[] = "comparison";
strng2[] = "communication";
```

k = strcmp(strng1, strng2);

`strng1` 和 `strng2` 中的字符逐字符比较。在第四位置 m 和 p 不相等，且 p 的数值代码大于 m 的数值代码，这识别出 `strng1` 在 `strng2` 之后。此比较产生了一个大于零的数字，因为 `strng1` 跟随 `strng2`。程序员可以测试此比较的结果并执行如下一条或多语句：

```c
if(strcmp(strng1, strng2) > 0)
    statement1;
else
    statement2;
```

在这种情况下，由于 `strng1` 按字母顺序后于 `strng2`，因此执行 `statement1`。
这也可以通过另一种方式实现，声明一个整数变量并将字符串比较的结果赋值给该整数变量。以下代码展示了这种实现。

```c
int c;
c = strcmp(strng1, strng2);
if(c > 0)
    statement1;
else
    statement2;
```

`strng1` 大于 `strng2`，字符串比较产生了一个大于零的数字并赋值给 `c`，在这种情况下关系表达式 `c > 0` 为真，因此执行 `statement1`。

有时只需要比较字符串中的前几个字符，例如通过比较 mm/dd/yyyy 格式的日期来仅比较月份。为了处理此类

## 9.4 字符串库函数

还有另一种形式的字符串比较函数。该函数有三个参数。以下示例展示了此类函数的使用。

```
strng1[] = "comparison";
strng2[] = "communication";
```

| c | o | m | p | a | r | i | s | o | n | \0 |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |

```c
k = strncmp(strng1, strng2, n);
```

| c | o | m | m | u | i | c | a | t | i | o | n | \0 |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |

`strng1` 大于 `strng2`，字符串比较产生了一个大于零的数字并将数字赋值给 `c`，在这种情况下关系表达式 `c > 0` 为真，因此执行 `statement1`。 (注：此处原文文本似乎存在重复或乱码，翻译时已根据逻辑进行处理)

