
## 计算字符串中的字符数

其中第一个函数 strlen() 尤其简单直接。它只有一个参数，即字符串起始位置的地址；其返回值为字符串中的字符数，不包括结尾的 NUL。

为了演示 strlen() 的用法，下面是一个简单的程序：它读入一个字符串，并将其反向打印出来，这是一件有用的事情。该程序会重复运行，直到用户输入一个长度为零的字符串，也就是在程序提示后立即按 <Return> 键，才会终止。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char s[100];
    int len;    /* holds length of string */
    while(1)
    {
        printf("Enter a string");
        gets(s);
        len = strlen(s);    /* find length */
        if(len == 0) break; /* termination condition */
        while(len > 0)
        {
            len--;
            printf("%c",s[len]);
        }
        printf("\n");
    }
    return 0;
}
```

该程序通过逐个打印字符来工作，从字符串中最后一个非 NUL 字符开始。请注意，在输出该字符之前，'len' 会先递减。这是正确的，因为 strlen() 返回的长度不包括 NUL，而实际字符是聚合成员，编号为 0、...、length-1。该程序在不同示例运行中的输出如下

- (a) Enter a string 1234  
  4321
- (b) Enter a string manas  
  sanam
- (c) Enter a string abc def ghi  
  ihg fed cba

请看下面的程序，它读取一行文本，将其存入一个字符串，并打印其长度（不包括末尾的换行符）。

```c
#include <stdio.h>
int main()
{
    int n, c;
    char line[100];
    n = 0;
    while((c=getchar()) != '\n')
    {
        if(n < 100)
            line[n] = c;
        n++;
    }
    line[n]='\0';
    printf("length = %d\n", n);
    return 0;
}
```

最后，这里给出 strlen() 的另一个版本。

```c
int mystrlen(char str[])
{
    int i;
    for(i = 0; str[i] != '\0'; i++)
    {}
    return i;
}
```

在这种情况下，只需找到终止字符串的 \0 即可。事实证明，for 循环的三个控制表达式完成了全部工作；循环体中已无事可做。因此，使用一对空花括号 {} 作为循环体。等价地，也可以使用空语句，即如下所示的一个分号。

```c
for(i = 0; str[i] != '\0'; i++);
```

空循环体起初可能有点令人吃惊，但它们并非闻所未闻。

## 将字符串复制到另一个字符串

由于 C 语言从不允许对整个数组进行赋值，因此可以使用 strcpy() 函数将一个字符串复制到另一个字符串。strcpy() 将第二个参数所指向的字符串复制到第一个参数所指向的空间中。整个字符串（包括终止 NUL）都会被复制，并且不会检查第一个参数所指示的空间是否足够大。给出的代码展示了 strcpy() 函数的用法。

```c
#include <string.h>
int main()
{
    char s1[] = "Hello, world!";
    char s2[20];
    strcpy(s2, s1);
    puts(s2);
    return 0;
}
```

目标字符串是 strcpy() 的第一个参数，因此对 strcpy 的调用类似于赋值表达式，目标在左侧。请注意，必须为字符串 s2 分配足够的内存，以便它能容纳将要复制到其中的字符串。此外，在任何源文件的顶部，都必须包含以下行

```c
#include <string.h>
```

该行包含这些函数的外部声明。

由于字符串只是一个字符数组，所有字符串处理函数都可以相当简单地编写，所使用的技术不会比已经知道的更复杂。事实上，看看这些函数可能如何实现是很有启发性的。下面是 `strcpy` 的一个版本。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char src[30], dest[30];
    int i = 0;
    printf("\n Enter the source string: ");
    scanf("%[^\n]", src);
    while(src[i] != '\0')
    {
        dest[i] = src[i];
        i++;
    }
    dest[i] = '\0';
    printf("\n Source string is : %s\n", src);
    printf("\n Destination string is : %s\n", dest);
    return 0;
}
```

它的操作很简单。它逐个查看 `src` 字符串中的字符，只要它们不是 `\0`，就将它们逐个赋给 `dest` 字符串中的对应位置。完成后，它通过放置一个 `\0` 来终止 `dest` 字符串。退出 while 循环后，`i` 的值保证比 `src` 中最后一个字符的下标大 1。为了比较，下面给出用 for 循环代替 while 循环编写同一代码的一种方式。

```c
for(i = 0; src[i] != '\0'; i++)
    dest[i] = src[i];
dest[i] = '\0';
```

上述语句可以使用以下表达式重写：

`for(i=0;(dest[i] = src[i]) != '\0';i++);`

这实际上属于同一种组合操作。

## 比较字符串

另一个函数 `strcmp()` 以两个字符串的起始地址作为参数，如果字符串相等，则返回零值。如果字符串不相等，则返回负值或正值。如果第一个字符串大于第二个字符串，则返回值为正；如果第一个字符串小于第二个字符串，则返回值为负。在此上下文中，字符串的相对值是指由宿主计算机字符集（或排序序列）确定的相对值。

重要的是要认识到，不能仅仅通过比较两个字符串的起始地址来比较它们，尽管这在语法上是有效的。以下程序演示了两个字符串的比较：

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char x[50], y[] = "a programming example";
    strcpy(x, "A Programming Example");
    if(strcmp(x, "A Programming Example") == 0)
        printf("Equal \n");
    else
        printf("Unequal \n");
    if(strcmp(y, x) == 0)
        printf("Equal \n");
    else
        printf("Unequal \n");
    return 0;
}
```

它产生以下输出：

```
Equal
Unequal
```

## 将字符串连接在一起

算术加法不能用于按以下方式连接两个或多个字符串

```
string1 = string2 + string3; or
string1 = string2 + "RAJA";
```

为此，需要使用标准库函数 `strcat()` 来连接字符串。它并不会将两个字符串连接起来并生成第三个新字符串。它实际做的是将一个字符串追加到另一个字符串的末尾。下面是一个示例。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char s[30] = "Hello,";
    char str[] = "world!";
    printf("%s\n", s);
    strcat(s, str);
    printf("%s\n", s);
    return 0;
}
```

第一次调用 `printf` 打印出 “Hello,”，第二次调用打印出 “Hello,world!”，这表明 `str` 的内容已被追加到 `s` 的末尾。请注意，`s` 声明时预留了额外空间，以便为追加的字符腾出位置。

请注意，在算术运算中，`char` 变量通常可以像 `int` 变量一样处理。对字符进行算术运算是完全合法的，而且通常是有意义的。

```
c = c + 'A' - 'a';
```

将存储在 `c` 中的单个小写 ASCII 字符转换为大写字母，利用的是对应 ASCII 字母之间相隔固定距离这一事实。支配这种算术运算的规则是：在进行算术运算之前，所有 `char` 都会转换为 `int`。请注意，转换可能涉及符号扩展；如果某个字符的最左位为 1，则得到的整数可能为负数。

因此，要将文本转换为小写，可以使用以下程序：

```c
#include <stdio.h>
int main()
{
    char c;
    while((c=getchar()) != '\n')
    if('A'<=c && c<='Z')
        putchar(c+'a'-'A');
        /* equivalent statement in putchar(c+32);*/
    else
        putchar(c);
    return 0;
}
```

示例运行：

```
TIMES OF INDIA
times of india
```

以下程序将演示 strncat() 库函数：

```c
#include <string.h>
#include <stdio.h>
int main()
{
    char aString1[80] = "RCC Institute of Information Technology",
    aString2[80] = "Oxford University Press";
    printf("\n Before the copy...\n");
    puts(aString1);
    puts(aString2);
    strncat(aString1, aString2, 6);
    printf("\nAfter the copy...\n");
    puts(aString1);
    puts(aString2);
    return 0;
}
```

**输出**

```
Before the copy...
RCC Institute of Information Technology
Oxford University Press
After the copy...
RCC Institute of Information Technology Oxford
Oxford University Press
```

**注意**

- 由于 C 语言从不允许对整个数组进行赋值，因此可以使用 strcpy() 函数将一个字符串复制到另一个字符串。
- 可以借助 strcmp() 函数比较字符串。
- 算术加法不能用于连接两个或多个字符串；这可以通过使用标准库函数 strcat() 来完成。

## 一些示例程序

*一件有趣的事：这个程序试图证明字符串实际上是一个字符数组。注意字符串终止符被显式放在字符串末尾。注意 &str[2] 这个写法。记住 str[2] 是第三个字符，所以 &str[2] 是第三个字符的地址。由于 str 是第一个字符的地址，&str[2] 实际上就是去掉了前两个字符的 str。试着把 &str[2] 替换为 str+2。这样能行吗？最后，注意使用了 string.h 库中的 strcpy（字符串复制）函数。*

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char str[30];
    str[0]='M';
    str[1]='A';
    str[2]='D';
    str[3]='A';
    str[4]='M';
    str[5]='\0'; /* terminate string with a null */
    printf("String is %s\n",str);
    printf("Part of string is %s\n",&str[2]);
    strcpy(str,"SIR");
    printf("String is %s\n",str);
    return(0);
}
```

示例运行：

```
String is MADAM
Part of string is DAM
String is SIR
```

为了确保理解正在发生什么，请考虑下表：

| 代码 | 输出 |
|---|---|
| `printf("%s?", str);` | MADAM |
| `printf("%s?", str[1]);` | Error |
| `printf("%s?", &str[1]);` | ADAM |
| `printf("%s?", &str);` | MADAM |

以下一些程序将演示字符串操作。下面的程序切换输入字符串中每个字符的大小写。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char istr[128]; /* input buffer */
    char tstr[128]; /* translated string here */
    int i;
    int slen; /* string length */
    while(1)
    {
