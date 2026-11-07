
```
9
10 double d = strtod(string, &stringPtr);
11
12 printf("The string \"%%s\" is converted to the\n", string);
13 printf("double value %.2f and the string \"%%s\"\n", d, stringPtr);
14 }
```

字符串 "51.2% are admitted" 被转换为
double 值 51.20 以及字符串 "% are admitted"

Fig. 8.4 | 使用函数 strtod。 (第 2 部分，共 2 部分。)

### 8.4.2 函数 strtol

函数 strtol (图 8.5) 将表示整数的字符序列转换为 long int。 如果函数无法将其第一个参数的任何部分转换为 long int，则返回 0。 该函数的三个参数分别是字符串 (char *)、字符串指针和整数。 该函数的工作方式与 strtod 相同，但第三个参数指定要转换的值的基数。

```
1 // fig08_05.c
2 // Using function strtol
3 #include <stdio.h>
4 #include <stdlib.h>
5
6 int main(void) {
7 const char *string = "-1234567abc";
8 char *remainderPtr = NULL;
9
10 long x = strtol(string, &remainderPtr, 0);
11
12 printf("%%s\"%%s\"\n%%s%%ld\n%%s\"%%s\"\n%%s%%ld\n",
13 "The original string is ", string,
14 "The converted value is ", x,
15 "The remainder of the original string is ", remainderPtr,
16 "The converted value plus 567 is ", x + 567);
17 }
```

原始字符串是 "-1234567abc"
转换后的值是 -1234567
原始字符串的剩余部分是 "abc"
转换后的值加上 567 是 -1234000

Fig. 8.5 | 使用函数 strtol。

第 10 行将 x 分配为从 string 转换而来的 long 值，并使 remainderPtr 指向 string 中的 "a"。 使用 NULL 作为第二个参数会导致忽略字符串的剩余部分。 第三个参数 0 表示要转换的值可以采用八进制（基数 8）、十进制（基数 10）或十六进制（基数 16）格式。 基数可以指定为 0 或 2 到 36 之间的任何值。¹ 基数 11 到基数 36 的整数表示使用字母 A–Z 表示整数值 10–35。 例如，十六进制值可以由数字 0–9 和字符 A–F 组成。

### 8.4.3 函数 strtoul

函数 `strtoul` (图 8.6) 将表示 unsigned long int 值的字符序列转换为 unsigned long int。 该函数的工作方式与函数 `strtol` 相同。 第 10 行将 x 分配为从 string 转换而来的 unsigned long int 值，并使 remainderPtr 指向 string 中的 "a"。 第三个参数 0 表示要转换的值可以采用八进制、十进制或十六进制格式。

```c
// fig08_06.c
// Using function strtoul
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    const char *string = "1234567abc";
    char *remainderPtr = NULL;

    unsigned long int x = strtoul(string, &remainderPtr, 0);

    printf("%s\"%s\"\n%s%u\n%s\"%s\"\n%s%u\n",
        "The original string is ", string,
        "The converted value is ", x,
        "The remainder of the original string is ", remainderPtr,
        "The converted value minus 567 is ", x - 567);
}
```

原始字符串是 "1234567abc"
转换后的值是 1234567
原始字符串的剩余部分是 "abc"
转换后的值减去 567 是 1234000

**Fig. 8.6**  |  使用函数 `strtoul`。

## 自检

1. *(讨论)* 为什么函数的参数列表中会包含 `char **` 参数？

**答案：** `char **` 通常是指向调用者中 `char *` 指针的指针。 被调用的函数使用此类指针通过引用接收 char * 以便在调用者中修改它——例如，使其指向另一个字符串。 这是指针到指针的一个例子。

- 2. *(多选题)* 关于函数 `strtol` 的以下陈述中哪一个是错误的？
- a) 它将表示整数的字符序列转换为 long int，或者如果无法将其第一个参数的任何部分转换为 long int，则返回 0。
- b) strtol 的三个参数是字符串 (`char *`)、字符串指针 (`char **`) 和整数。
- c) 字符串参数包含要转换为 `long` 的字符序列——字符串开头任何空白字符都会被忽略。
- d) 函数使用 `char **` 参数使调用者能够访问正在转换的字符串的数值部分。

¹ 有关八进制、十进制和十六进制数系统的详细解释，请参阅在线附录 E。

答案：d) 是 *错误的*。 实际上，函数使用 `char **` 参数修改调用者中的 `char *`，使其指向字符串转换部分之后第一个字符的位置。 如果没有进行转换，函数会修改 `char *` 使其指向整个字符串。

## 8.5 标准输入/输出库函数

本节介绍标准输入/输出 (`<stdio.h>`) 库的字符和字符串操作函数，我们在下表中对其进行了总结。

| 函数原型 | 函数描述 |
| --- | --- |
| `int getchar(void);` | 从标准输入返回下一个字符作为整数。 |
| `char *fgets(char *s, int n, FILE *stream);` | 从指定流读取字符到数组 `s`，直到遇到换行符或文件结束字符，或读取 `n - 1` 个字节为止。 本章使用流 `stdin`——标准输入流——从键盘读取字符。 在数组末尾附加一个终止空字符。 返回读取到 `s` 中的字符串。 如果遇到换行符，则将其包含在存储的字符串中。 |
| `int putchar(int c);` | 打印存储在 `c` 中的字符并将其作为整数返回。 |
| `int puts(const char *s);` | 打印字符串 `s` 后跟换行符。 成功时返回非零整数，或在发生错误时返回 `EOF`。 |
| `int sprintf(char *s, const char *format, ...);` | 等同于 `printf`，但输出存储在数组 `s` 中而不是打印到屏幕上。 返回写入 `s` 的字符数，或在发生错误时返回 `EOF`。 |
| `int sscanf(char *s, const char *format, ...);` | 等同于 `scanf`，但输入从数组 `s` 读取而不是从键盘读取。 返回函数成功读取的项目数，或在发生错误时返回 `EOF`。 |

### 8.5.1 函数 fgets 和 putchar

图 8.7 使用函数 fgets 和 putchar 从标准输入（键盘）读取一行文本并递归地以相反顺序输出该行的字符。 第 12 行使用 fgets 读取字符到其字符数组参数中，直到遇到换行符或文件结束指示符，或读取最大数量的字符为止。

第 26 行和第 27 行中两个语句的顺序导致 reverse 在显示任何字符 *之前* 遍历到字符串的终止空字符。 随着递归调用的完成，字符以相反顺序输出。

### 8.5.2 函数 getchar

图 8.8 使用函数 getchar 逐个字符地从标准输入读取到字符数组 sentence 中，然后使用 puts 将字符作为字符串显示。 函数 getchar 从标准输入读取一个字符并将其作为整数返回。 回顾第 4.6 节，返回整数是为了支持文件结束指示符。 如你所知，puts 以字符串作为参数并显示字符串后跟换行符。 程序在读取 79 个字符或 getchar 读取换行符时停止输入字符。 第 18 行向 sentence 附加一个空字符以终止字符串。 然后第 21 行使用 puts 显示 sentence。

```c
 1  // Fig08_08.c
 2  // Using function getchar
 3  #include <stdio.h>
 4  #define SIZE 80
 5
 6  int main(void) {
 7      int c = 0; // variable to hold character input by user
 8      char sentence[SIZE] = "";
 9      int i = 0;
10
11      puts("Enter a line of text:");
12
13      // use getchar to read each character
14      while ((i < SIZE - 1) && (c = getchar()) != '\n') {
15          sentence[i++] = c;
16      }
17
18      sentence[i] = '\0'; // terminate string
19
20      puts("\nThe line entered was:");
21      puts(sentence); // display sentence
22  }
```

输入一行文本：
这是一次测试。

输入的行是：
这是一次测试。

**Fig. 8.8** | 使用函数 getchar。

### 8.5.3 函数 sprintf

图 8.9 使用函数 sprintf 将格式化的<|message|>
