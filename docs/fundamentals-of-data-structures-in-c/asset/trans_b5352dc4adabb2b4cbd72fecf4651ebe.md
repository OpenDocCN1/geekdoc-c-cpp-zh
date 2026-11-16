

## 1.16 字符串库函数

随每个 C 编译器提供一大套有用的库函数。表 1.15 列出了常用的字符串函数及其用途。

### 表 1.15：字符串函数

| Function | Meaning |
| :--- | :--- |
| strcpy() | 将一个字符串复制到另一个字符串 |
| strcat() | 将一个字符串追加到另一个字符串末尾 |
| strchr() | 查找字符串中给定字符的第一次出现 |
| strcmp() | 比较两个字符串 |
| strcmpi() | 比较两个字符串，不区分大小写（“i”表示该函数忽略大小写） |
| strcpy() | 将一个字符串复制到另一个字符串 |
| strcspn() | 查找字符串 s1 的初始段，该段完全由不属于字符串 s2 的字符组成。 |
| strdup() | 复制一个字符串 |
| stricmp() | 比较两个字符串，不区分大小写（与 strcmpi 相同） |
| strlen() | 查找字符串的长度 |
| strlwr() | 将字符串转换为小写 |
| strncat() | 将一个字符串的前 n 个字符追加到另一个字符串末尾 |
| strncmp() | 比较两个字符串的前 n 个字符 |
| strncpy() | 将一个字符串的前 n 个字符复制到另一个字符串 |
| stricmp() | 比较两个字符串，不区分大小写（与 strcmpi 相同） |
| strnset() | 将字符串的前 n 个字符设置为给定字符 |
| strrbrk() | 扫描字符串 s1，查找任何出现在 s2 中的字符的第一次出现。 |
| strrchr() | 查找字符串中给定字符的最后一次出现 |
| strrev() | 反转一个字符串。 |
| strset() | 将字符串的所有字符设置为给定字符 |
| strspn() | 查找字符串 s1 的初始段，该段完全由属于字符串 s2 的字符组成。 |
| strstr() | 在另一个字符串中查找给定字符串的第一次出现 |
| strtok() | 扫描 s1，查找第一个不包含在 s2 中的标记 |
| strupr() | 将字符串转换为大写 |
| strxfrm() | 将字符串 s2 转换为字符串 s1，不超过 n 个字符。 |

从上面的列表中，我们将讨论 strlen()、strcpy()、strcat()、strcmp()、strrev()、strlwr() 函数，因为这些是最常用的字符串库函数。

### 1.16.1 strlen() 函数

strlen()（字符串长度）函数返回存储在字符串中的字符数。strlen() 函数的一般形式或语法是

```
x = strlen(str);
```

其中 x 是接收字符串长度的整型变量，str 是有效的字符串变量或常量。程序 1.17 有助于你更好地理解。

### 程序 1.17

```
/* strlen.c */
#include<stdio.h>
#include<string.h>
void main()
{
char str[25];
printf("Enter a string : ");
gets(str);
printf("The length of the string is %d", strlen(str));
}
```

程序显示以下输出

```
Enter a string : Surya
The length of the string is 5
```

在程序 1.17 中，strlen() 函数接受一个参数（即用户输入的字符串），并返回字符串的长度。请注意，字符串长度不计算空字符。如果用户输入带空格的字符串，strlen() 函数返回字符串的长度，包括字符串中之间的空格数量。例如，

```
Enter a string : Raj Kumar
The length of the string is 9
```

strlen() 函数还计算字符串中的空格，并将字符串长度返回为 9。

### 1.16.2 strcpy() 函数

字符串不能直接使用赋值语句复制（指针除外）。但是，可以使用赋值语句逐个元素复制字符串。strcpy()（字符串复制）函数用于将一个字符串的内容复制到另一个字符串。strcpy() 函数的一般形式或语法是

```
strcpy(string1, string2);
```

其中 string1 和 string2 是有效的字符串变量或字符串常量。strcpy() 函数接受两个参数用于复制。第二个参数（即 string2）中的字符串被复制到第一个参数（即 string1）。要将一个字符串复制到另一个字符串，应将源字符串和目标字符串的基地址提供给此函数。程序 1.18 有助于你更好地理解。

### 程序 1.18

```
/* strcpy.c */
#include<stdio.h>
#include<string.h>
void main()
{
char str[25];
char cpy[25];
printf("Enter a string : ");
gets(str);
strcpy(cpy, str);
printf("\n The source string is %s", str);
printf("\n The copied string is %s", cpy);
}
```

程序显示以下输出

```
Enter a string : Krishna
The source string is Krishna
The copied string is Krishna
```

在程序 1.18 中，变量 str 用于读取输入字符串，并将输入字符串复制到 cpy。str 中的变量被逐个字符复制到 cpy，直到遇到空字符。空字符也被复制。

### 1.16.3 strcat() 函数

strcat()（字符串连接）函数将源字符串连接到目标字符串的末尾。strcat() 函数接受两个参数用于连接。第二个参数（即 string2）中的字符串与第一个参数（即 string1）中存在的字符串连接。strcat() 函数的一般形式或语法是

```
strcat(string1, string2);
```

其中 string1 和 string2 是有效的字符串变量或字符串常量。string2 的内容与 string1 的内容连接。程序 1.19 有助于你更好地理解。

### 程序 1.19

```
/* strcat.c */
#include<stdio.h>
#include<string.h>
void main()
{
    char str[25], cat[25];
    printf("Enter a string : ");
    gets(str);
    printf("Enter another string : ");
    gets(cat);
    strcat(str, cat);
    printf("The concatenated string is : %s", str);
}
```

程序显示以下输出

```
Enter a string : Rama
Enter another string : Chandran
The concatenated string is : RamaChandran
```

在程序 1.19 中，第一个字符串存储在变量 str 中，第二个字符串存储在变量 cat 中。cat 中的字符串与 str 中的字符串连接，并显示输出。

### 1.16.4 strcmp() 函数

strcmp()（字符串比较）函数比较两个字符串以查找字符串是否相等。strcmp() 函数的一般形式或语法是，

```
strcmp(string1, string2);
```

其中 string1 和 string2 是有效的字符串变量或字符串常量。strcmp() 函数接受两个参数用于比较并返回一个整数。第一个参数（即 string1）中的字符串与第二个参数（即 string2）中的字符串逐个字符比较，直到遇到两个字符串之间的不匹配或两个字符串中任何一个的末尾。程序 1.20 有助于你更好地理解。

### 程序 1.20

```
/* strcmp.c */
#include<stdio.h>
#include<string.h>
void main()
{
    char str[25], cmp[25];
    int x;
    printf("Enter a string : ");
    gets(str);
    printf("Enter another string : ");
    gets(cmp);
    x = strcmp(str, cmp);
    if(x == 0)
    puts("Strings are Equal");
    else if(x > 0)
    printf("String %s is greater than string %s", str, cmp);
    else
    printf("String %s is greater than string %s", cmp, str);
}
```

### 程序显示以下输出

```
RUN 1
Enter a string : Subramanian
Enter another string : Subramanian
Strings are Equal

RUN 2
Enter a string : Jaikumar
Enter another string : Sasikumar
String Sasikumar is greater than string Jaikumar

RUN 3
Enter a string : Yuvaraj
Enter another string : Jebaraj
String Yuvaraj is greater than string Jebaraj
```

在运行 1 中，用户输入两个字符串后，strcmp() 函数逐个字符比较两个字符串，由于在未检测到不等字符的情况下到达字符串末尾，因此字符串相等。strcmp() 函数返回值零，因此 if 语句中的条件为真，printf() 函数显示消息

> 字符串相等

在运行 2 中，用户输入两个字符串 Jaikumar、Sasikumar 后，由于字符串 Sasikumar 大于字符串 Jaikumar，strcmp() 函数返回大于零的值，else if 语句中的条件为真，printf() 函数显示消息

> 字符串 Sasikumar 大于字符串 Jaikumar

在运行 3 中，用户输入两个字符串 Yuvaraj、Jebaraj 后，由于字符串 Jebaraj 小于字符串 Yuvaraj，strcmp() 函数返回一个值

