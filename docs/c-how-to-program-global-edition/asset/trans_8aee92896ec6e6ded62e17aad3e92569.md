
从第 7.4 节可知，返回一个整数以支持文件结束指示符。如你所知，函数 puts 以字符串作为参数并显示该字符串后跟换行字符。程序在读取 79 个字符或 getchar 读取用户输入以结束文本行的换行字符时停止输入字符。空字符被追加到数组 sentence（第 20 行），以便该数组可被视为字符串。然后第 24 行使用 puts 显示 sentence 中包含的字符串。

// Fig. 8.11: fig08_11.c
// Using function getchar.
#include <stdio.h>
#define SIZE 80

int main(void)
{
    int c; // variable to hold character input by user
    char sentence[SIZE]; // create char array
    int i = 0; // initialize counter i

    // prompt user to enter line of text
    puts("Enter a line of text:");

    // use getchar to read each character
    while ((i < SIZE - 1) && ((c = getchar()) != '\n')) {
        sentence[i++] = c;
    }

    sentence[i] = '\0'; // terminate string

    // use puts to display sentence
    puts("\nThe line entered was:");
    puts(sentence);
}

输入一行文本：
This is a test.

输入的行是：
This is a test.

Fig. 8.11 | 使用函数 getchar。

## 8.5.3 函数 sprintf

图 8.12 使用函数 sprintf 将格式化的<|message|> 数据打印到数组 s——一个字符数组。该函数使用与 printf 相同的转换说明符（有关格式化的详细讨论请参见第 9 章）。程序输入一个 int 值和一个 double 值以便格式化并打印到数组 s。数组 s 是 sprintf 的第一个参数。[注意：如果你的系统支持 C11 的 snprintf_s，则优先使用它而不是 sprintf。如果你的系统不支持 snprintf_s 但支持 snprintf，则优先使用 snprintf 而不是 sprintf。]

```c
// Fig. 8.12: fig08_12.c
// Using function sprintf
#include <stdio.h>
#define SIZE 80

int main(void)
{
    int x; // x value to be input
    double y; // y value to be input

    puts("Enter an integer and a double:");
    scanf("%d%lf", &x, &y);

    char s[SIZE]; // create char array
    sprintf(s, "integer:%6d\n double:%.2f", x, y);

    printf("%s\n%s\n", "The formatted output stored in array s is:", s);
}
```

输入一个整数和一个双精度数：
298 87.375
存储在数组 s 中的格式化输出是：
integer:  298
double: 87.38

Fig. 8.12 | 使用函数 sprintf。

## 8.5.4 函数 sscanf

图 8.13 使用函数 sscanf 从字符数组 s 读取格式化数据。该函数使用与 scanf 相同的转换说明符。程序从数组 s 读取一个 int 和一个 double，并分别将值存储在 x 和 y 中。x 和 y 的值将被打印。数组 s 是 sscanf 的第一个参数。

```c
// Fig. 8.13: fig08_13.c
// Using function sscanf
#include <stdio.h>

int main(void)
{
    char s[] = "31298 87.375"; // initialize array s
    int x; // x value to be input
    double y; // y value to be input

    sscanf(s, "%d%lf", &x, &y);
    printf("%s\n%s%6d\n%s%.3f\n",
           "The values stored in character array s are:",
           "integer:", x, "double:", y);
}
```

Fig. 8.13 | 使用函数 sscanf。（第 1 部分，共 2 部分。）

存储在字符数组 s 中的值是：
integer: 31298
double: 87.375

Fig. 8.13 | 使用函数 sscanf。（第 2 部分，共 2 部分。）

## 8.6 字符串处理库的字符串操作函数

字符串处理库 <string.h> 提供了许多用于操作字符串数据的有用函数（复制字符串和连接字符串）、比较字符串、搜索字符串中的字符和其他字符串、标记化字符串（将字符串分离为逻辑片段）以及确定字符串长度。本节介绍字符串处理库的字符串操作函数。这些函数在图 8.14 中进行了总结。每个函数——strncpy 除外——都会在其结果后追加空字符。[注意：这些函数中的每一个在 C11 标准的可选附录 K 中都有更安全的版本。我们将在本章的 Secure C Programming 部分提到这些。]

| Function prototype | Function description |
|---|---|
| `char *strcpy(char *s1, const char *s2)` | 将字符串 s2 复制到数组 s1 中。返回 s1 的值。 |
| `char *strncpy(char *s1, const char *s2, size_t n)` | 最多复制字符串 s2 的 n 个字符到数组 s1 中并返回 s1。 |
| `char *strcat(char *s1, const char *s2)` | 将字符串 s2 追加到数组 s1。s2 的第一个字符会覆盖 s1 的终止空字符。返回 s1 的值。 |
| `char *strncat(char *s1, const char *s2, size_t n)` | 最多将字符串 s2 的 n 个字符追加到数组 s1。s2 的第一个字符会覆盖 s1 的终止空字符。返回 s1 的值。 |

Fig. 8.14 | 字符串处理库的字符串操作函数。

函数 strncpy 和 strncat 指定类型为 size_t 的参数。函数 strcpy 将其第二个参数（一个字符串）复制到其第一个参数——一个字符数组，你必须确保该数组足够大以存储字符串及其终止空字符，后者也会被复制。函数 strncpy 等同于 strcpy，只是 strncpy 指定了要从字符串复制到数组中的字符数。函数 strncpy 不一定复制其第二个参数的终止空字符。只有当要复制的字符数多于字符串的长度时才会发生这种情况。例如，如果第二个参数是 "test"，则只有当传递给 strncpy 的第三个参数至少为 5（"test" 中的四个字符加上一个终止空字符）时，才会写入终止空字符。如果第三个参数大于 5，则某些实现会向数组追加空字符，直到写入第三个参数指定的总字符数，而其他实现则在写入第一个空字符后停止。

## 常见编程错误 8.5

当 strncpy 的第三个参数小于或等于第二个参数中字符串的长度时，未向第一个参数追加终止空字符。

## 8.6.1 函数 strcpy 和 strncpy

图 8.15 使用 strcpy 将数组 x 中的整个字符串复制到数组 y，并使用 strncpy 将数组 x 的前 14 个字符复制到数组 z。由于程序中对 strncpy 的调用不会写入终止空字符（第三个参数小于第二个参数的字符串长度），因此向数组 z 追加了一个空字符（'\0'）。

// Fig. 8.15: fig08_15.c
// Using functions strcpy and strncpy
#include <stdio.h>
#include <string.h>
#define SIZE1 25
#define SIZE2 15

int main(void)
{
    char x[] = "Happy Birthday to You!"; // initialize char array x
    char y[SIZE1]; // create char array y
    char z[SIZE2]; // create char array z

    // copy contents of x into y
    printf("%s\n%s\n%s\n", "The string in array x is: ", x, "The string in array y is: ", strcpy(y, x));

    // copy first 14 characters of x into z. Does not copy null character
    strncpy(z, x, SIZE2 - 1);

    z[SIZE2 - 1] = '\0'; // terminate string in z
    printf("The string in array z is: %s\n", z);
}

数组 x 中的字符串是：Happy Birthday to You
数组 y 中的字符串是：Happy Birthday to You
数组 z 中的字符串是：Happy Birthday

Fig. 8.15 | 使用函数 strcpy 和 strncpy。

## 8.6.2 函数 strcat 和 strncat

函数 strcat 将其第二个参数（一个字符串）追加到其第一个参数（包含字符串的字符数组）。第二个参数的第一个字符会替换终止第一个参数中字符串的空字符（'\0'）。你必须确保用于存储第一个字符串的数组足够大，可以存储第一个字符串、第二个字符串以及从第二个字符串复制的终止空字符。函数 strncat 将第二个字符串的指定数量的字符追加到第一个字符串。终止空字符会自动追加到结果。图 8.16 演示了函数 strcat 和函数 strncat。
