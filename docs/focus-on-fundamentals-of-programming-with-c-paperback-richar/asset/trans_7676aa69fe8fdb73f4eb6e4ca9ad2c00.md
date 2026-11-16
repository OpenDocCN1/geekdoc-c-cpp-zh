

The string.h 库包含多种用于操作字符串的函数。要使用其中任何函数，我们必须将以下声明添加到程序中：

```
#include <string.h>
```

我们将重点介绍 string.h 库中出现的四个字符串函数：strlen()、strcpy()、strcat()、strcmp()。我们还将为每个这些字符串函数编写自己的代码。

- strlen(s1)

告诉我们字符串的长度。它返回字符串中的字符数，不包括空终止字符。

函数原型：
int strlen(char *s1);

例如：

```
strlen("Computer");
```

返回值 8 而不是 9。

我们实际上可以编写一个简单函数来计算自己的字符串长度。请注意，我们使用字符串中空字符的位置来帮助确定字符串的结束：

```
// strlen1.c
int strlen(char s1[]) {
    int i = 0;
    while (s1[i] != '\0') {
        ++i;
    }
    return i;
}
```

形式参数 s1 并不真正是一个字符数组，而是一个保存数组首元素地址的变量。这称为字符指针，函数也可以声明为：

```
int strlen(char *s1)
```

当 strlen() 运行其循环时，它将依次查看 s1[0]、s1[1] 等。由于 s1 包含数组的初始地址，C 理解 s1[0] 表示该地址处的字符。

- strcpy(s1, s2) 将字符串 s2 复制到字符串 s1，在移动终止空字符后停止。

函数原型：
void strcpy(char *s1, char *s2);

例如：

```
strcpy(s, "Computer");
```

将字符串 "Computer" 复制到字符串变量 s 中。

同样，我们可以编写自己的 strcpy() 函数，并可以使用字符串中空字符的位置来帮助确定字符串的结束：

```
// strcpy1.c
void strcpy(char s1[], char s2[]) {
    int i = 0;
    while (s2[i] != '\0') {
        s1[i] = s2[i];
        ++i;
    }
    s1[i] = '\0';
}
```

我们可以更简洁地编写它：

```
// strcpy.c

void strcpy(char s1[], char s2[]) {
    int i = 0;

    while ((s1[i] = s2[i]) != '\0') {
        ++i;
    }
}
```

- strcat(s1, s2) 将字符串 s2 复制到字符串 s1 的末尾。

函数原型：
void strcat(char *s1, char *s2);

例如：

```
char buf[32] = "Hello,";
strcat(buf, " world.");
printf("%s\n", buf);
```

输出字符串：

```
Hello, world.
```

再次，我们可以编写自己的代码来执行字符串连接：

```
// strcat1.c

void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;

    while (s1[i] != '\0') {
        ++i;
    }
    while (s2[j] != '\0') {
        s1[i] = s2[j];
        ++i;
        ++j;
    }
    s1[i] = '\0';
}
```

我们可以简化代码：

```
// strcat2.c

void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;

    while (s1[i]) {
        ++i;
    }
    while (s2[j]) {
        s1[i++] = s2[j++];
    }
    s1[i] = '\0';
}
```

我们可以进一步简化代码：

```
// strcat3.c

void strcat(char s1[], char s2[]) {
    int i = 0, j = 0;

    while (s1[i]) {
        ++i;
    }
    while (s1[i++] = s2[j++]) {
        ;
    }
}
```

- strcmp(s1, s2) 将字符串 s1 与字符串 s2 进行比较，从每个字符串的第一个字符开始，继续比较后续字符，直到对应字符不同或到达字符串末尾。该函数返回一个值，其值为：
  - < 0 如果 s1 小于 s2
  - == 0 如果 s1 与 s2 相同
  - > 0 如果 s1 大于 s2

函数原型：
int strcmp(char *s1, char *s2);

我们编写自己的代码来执行字符串比较：

```
// strcmp1.c

int strcmp(char s1[], char s2[]) {
    int i = 0;

    while (s1[i] == s2[i] && s1[i] != '\0') {
        ++i;
    }
    return s1[i] - s2[i];
}
```

以下是 `strcmp()` 函数的使用示例：

```
// compareStrings.c

#include <stdio.h>
#include <string.h>

int main(void) {
    int num;

    char s1[] = "red";
    char s2[] = "blue";
    num = strcmp(s1, s2);
    if (num < 0) {
        printf("%s is smaller.\n", s1);
    } else if (num > 0) {
        printf("%s is smaller.\n", s2);
    } else {
        printf("The strings are the same.");
    }
    return 0;
}
```

生成的输出如下：

```
blue is smaller.
```

请注意，C 不允许我们直接使用相等运算符比较两个字符串是否相等：

```
if (s1 == s2)
```

这是因为相等运算符只能应用于 int、float、char 等简单变量类型，而不能应用于结构体或数组。

## 其他字符串函数

以下是字符串库中位于的其他字符串操作函数：

- strncpy(s1, s2, max)

将最多 max 个字符从字符串 s2 复制到字符串 s1，截断或用空字符填充 s1。如果 s2 的长度为 max 或更多，目标字符串 s1 可能不是空终止的。

函数原型：
char *strncpy(char *s1, char *s2, int max);

- strncmp(s1, s2, max)

与 strcmp() 进行相同的比较，但最多查看 max 个字符。它从每个字符串的第一个字符开始，继续比较后续字符，直到对应字符不同或已检查 max 个字符。根据比较字符串 s1（或其部分）与字符串 s2（或其部分）的结果返回一个 int 值。该函数返回一个值，其值为：
< 0 如果 s1 小于 s2
== 0 如果 s1 与 s2 相同
> 0 如果 s1 大于 s2

函数原型：
int strncmp(char *s1, char *s2, int max);

- strchr(s1, c)

扫描字符串 s1 查找字符 c 的第一次出现。返回指向 s1 中字符 c 第一次出现位置的指针。如果 c 在 s 中不出现，strchr() 返回 null。

函数原型：
char *strchr(char *s1, int c);

- strrchr(s1, c)

扫描字符串查找给定字符的最后一次出现。strrchr() 以反向扫描字符串 s1，查找字符 c。返回指向字符 c 最后一次出现位置的指针。如果字符 c 在字符串 s1 中不出现，strrchr() 返回 null。

函数原型：
char *strrchr(char *s1, int c);

- strstr(s1, s2)

扫描字符串 s1 查找子字符串 s2 的第一次出现。返回指向 s1 中 s2 开始位置的元素的指针（在 s1 中指向 s2）。如果 s2 在 s1 中不出现，strstr() 返回 null。

函数原型：
char *strstr(char *s1, char *s2);

- strset(s1, c)

将字符串 s1 中的所有字符设置为字符 c。在找到终止空字符时停止。返回 s1。

函数原型：
char *strset(char *s1, int c);

- strrev(s1)

反转字符串。strrev() 将字符串中的所有字符更改为逆序，但终止空字符除外。返回指向反转后字符串的指针。

函数原型：
char *strrev(char *s1);

- strlwr(s1)

将字符串 s1 中的大写字母转换为小写。不更改其他字符。返回 s1。

函数原型：
char *strlwr(char *s1);

- strupr(s1)

将字符串 s1 中的小写字母转换为大写。
不更改其他字符。返回 s1。

函数原型：
char *strupr(char *s1);

## 两个字符串示例

以下是两个字符串函数。看看你能否弄清楚它们的工作原理。

```
// reverse.c
// Function to reverse a string in place
void reverse(char s[]) {
    int c, i, j;
    for (i = 0, j = (int)strlen(s)-1; i < j; ++i, --j) {
        c = s[i];
        s[i] = s[j];
        s[j] = c;
    }
}
```

```
// convert.c
// Function converts a string of digits into its numeric equivalent
int atoi(char buf[]) {
    int i, num;
    num = 0;
    for (i = 0; buf[i] >= '0' && buf[i] <= '9'; ++i) {
        num = 10 * num + buf[i] - 48;
    }
    return num;
}
```

## 字符串与指针

考虑以下两个声明：

```
(1) char word[] = "Computer";
(2) char *word = "Computer";
```

在声明 (1) 中，编译器会计算字符数并相应调整数组大小，总共 9 个字节（包括 '\0' 字符）。在这里，数组名 word 是指向数组首元素的常量指针：

```
word == &word[0]
```

我们可以展示以下等式：

```
*word == 'C'
*(word + 1) == word[1] == 'o'
```

在声明 (2) 中，使用指针表示法来设置字符串。编译器实际上预留了 13 个字节的存储空间：9 个字节用于字符串，4 个字节用于将指向该字符串的指针变量。

在两种情况下，word 都是指向字符串的指针。在两种情况下，字符串本身决定为字符串预留的存储量。但这两种形式不完全相同。数组形式在存储中设置一个包含 9 个元素（包括 '\0' 字符）的数组，编译器将名称 word 视为首数组元素地址 &word[0] 的同义词。请注意，word 是一个包含数组基地址且不可更改的指针常量。您可以引用 word + 1 来标识数组中的下一个元素，但不允许 ++word。

指针形式也会为字符串在存储中预留 9 个元素。但是，它还为指针变量 word 预留了一个额外的存储位置。该变量最初指向字符串的开头，但其值可以更改。在这里，++word 将指向第二个字符，等等。

