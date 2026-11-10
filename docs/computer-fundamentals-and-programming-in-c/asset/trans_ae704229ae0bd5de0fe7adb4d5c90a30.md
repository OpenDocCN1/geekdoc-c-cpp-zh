
以及数组。本讨论同样适用于字符串，因为字符串就是字符数组。考虑以下程序，它使用指针移动到字符串的下一个字符。

```c
14. #include <stdio.h>
int main()
{
    char a[15] = "test string";
    char *pa;
    pa = a;
    while(*pa)
    {
        putchar(*pa);
        pa++;
    }
    printf("\n");
    return 0;
}
```

### 输出

test string

while 循环等价于 `while (*pa != '\0')`。通过研究改编自标准库 `string.h` 的一些有用函数的版本，这里进一步说明指针和字符串的更多方面。第一个函数是 `strcpy(t,s)`，它把字符串 `s` 复制到字符串 `t`。如果只写 `s = t` 当然很好，但这复制的是指针，而不是字符。要复制字符，就需要一个循环。数组版本如下。

```c
15. #include <stdio.h>
int main()
{
    char a[50], b[50];
    void scopy(char *, char *);
    printf("\n Enter the string: ");
    gets(a);
    scopy(b,a);
    printf("\n %s",b);
    return 0;
}
```

```c
/* scopy: copy s to t; array subscript version */
void scopy(char *t, char *s)
{
    int i;
    i = 0;
    while(s[i] != '\0')
    {
        t[i] = s[i];
        i++;
    }
    t[i] = '\0';
}
```

`scopy()` 的一个等价版本如下。

```c
void scopy(char *t, char *s)
{
    int i;
    i = 0;
    while((t[i] = s[i]) != '\0')
        i++;
}
```

作为对比，下面是指针版本的 `scopy()`。

```c
/* scopy: copy s to t; pointer version */
void scopy(char *t, char *s)
{
    int i;
    i = 0;
    while((*t = *s) != '\0')
    {
        s++;
        t++;
    }
}
```

由于参数是按值传递的，`scopy` 可以使用参数 `b` 和 `a`。在这里，它们被方便地初始化为指针，沿着数组一次前进一个字符，直到终止 `s` 的 `\0` 被复制到 `t` 中。有经验的 C 程序员会更喜欢下面这个版本。

```c
/* scopy: copy s to t; pointer version 2 */
void scopy(char *s, char *t)
{
    while((*t++ = *s++) != '\0')
        ;
}
```

这会把 `s` 和 `t` 的递增移入循环的测试部分。`*s++` 的值是 `s` 递增之前所指向的字符；后缀 `++` 直到取出该字符之后才改变 `s`。同样，该字符会在 `t` 递增之前被存入 `t` 原来的位置。这个字符也是用来与 `\0` 比较以控制循环的值。最终效果是：字符从 `s` 复制到 `t`，直到并包括终止符 `\0`。

C99 标准规定，`strcpy()` 函数必须返回其目标参数的一个副本。在这两种情况下，我们都返回目标参数的一个副本——也就是说，我们返回一个指针作为函数的值。因此，标准库（`<string.h>`）中的 `strcpy()` 返回目标字符串作为其函数值。它可能看起来像

```c
char *strcpy(char *destination, char *source)
{
    char *p = destination;
    while(*source != '\0')
    {
        *p++ = *source++;
    }
    *p = '\0';
    return destination;
}
```

下面是 `strlen` 库函数的数组下标版本。

```c
int strlen(char s[])
{
    int x;
    x=0;
    while(s[x] != '\0')
        x=x+1;
    return(x);
}
```

使用基于指针的方法，这个函数可以重写如下。

```c
int strlen(char *s)
{
    int c=0;
    while(*s != '\0')
    {
        c++;
        s++;
    }
    return(c);
}
```

这段代码可以缩写如下。

```c
int strlen(char *s)
{
    int c=0;
    while(*s++)
        c++;
    return(c);
}
```

现在来看 strcmp(s,t)，它比较字符串 s 和 t，并在 s 按字典序小于、等于或大于 t 时分别返回负数、零或正数。该值通过用 s 和 t 第一个不同位置上的字符相减得到。

```c
int strcmp(char *s, char *t)
{
    int i;
    for(i = 0; s[i] == t[i]; i++)
        if(s[i] == '\0')
            return 0;
    return s[i] - t[i];
}
```

strcmp 的指针版本如下：

```c
int strcmp(char *s, char *t)
{
    for(; *s == *t; s++, t++)
        if(*s == '\0')
            return 0;
    return *s - *t;
}
```

为了说明字符串处理，编写一个函数来统计字符串中的单词数。假设字符串中的单词由空白字符分隔。这里，该函数将使用宏 isspace()，它定义在标准头文件 ctype.h 中。这个宏用于测试一个字符是空格、制表符、换行符还是其他某种空白字符。如果参数是空白字符，则返回非零（真）值；否则返回零（假）。

### 示例

```c
16. /* Count the number of words in a string. */
#include <stdio.h>
#include <ctype.h>
int word_cnt(char *s)
{
    int cnt = 0;
    while(*s != '\0')
    {
        while(isspace(*s))       /*skip white space */
            ++s;
        if(*s != '\0')
        {
            ++cnt;               /*found a word */
            while(!isspace(*s) && *s != '\0')
                                   /* skip the word */
                ++s;
        }
    }
    return cnt;
}
int main()
{
    char str[80];
    printf("\n ENTER THE SENTENCE");
    scanf("%[^\n]", str);
    printf("\n NO OF WORDS =%d", word_cnt(str));
    return 0;
}
```

作为示例，尝试编写一个函数，在一个字符串中查找另一个字符串：如果能够找到，就返回指向该字符串的指针；如果找不到，就返回空指针。下面是该函数（使用显而易见的暴力算法）：对于输入字符串的每个字符，代码都会检查是否与模式字符串匹配。

```c
17. #include <stddef.h>
    #include <stdio.h>
    int main()
    {
        char a[50], b[30];
        char *mystrstr(char *, char *);
        printf("\n Enter the string:");
        gets(a);
        printf("\n Enter the substring to search:");
        gets(b);
        if(mystrstr(a,b) == NULL)
            printf("NOT FOUND\n");
```

前面已经看到，指向兼容类型的两个指针可以相减。实际上，结果存储在变量类型 `ptrdiff_t` 中，该类型定义在头文件 `<stddef.h>` 中。两个指针都必须指向同一个数组中的元素，或指向数组末尾之后的一个位置，否则该减法未定义。结果的值是分隔这两个指针的数组元素个数。

### 示例

```c
18. #include <stdio.h>
int main()
{
    int x[100];
    int *pi, *cpi = &x[99]; /* cpi points to the last
                                element of x */
    pi = x;
    if ((cpi - pi) != 99)
        printf("Error\n");
    pi = cpi;
    pi++;
    /* increment past end of x */
    if ((pi - cpi) != 1)
        printf("Error\n");
    return 0;
}
```

上述程序的执行不会打印任何内容。考虑标准库函数 `strlen` 的另一个版本。

```c
int strlen(char *s)
{
    char *p = s;
    while (*p != '\0')
        p++;
    return p - s;
}
```

在它的声明中，p 被初始化为 s，也就是指向字符串的第一个字符。在 while 循环中，依次检查每个字符，直到看到末尾的 '\0'。因为 p 指向字符，所以 p++ 每次把 p 推进到下一个字符，而 p-s 给出前进经过的字符数，也就是字符串长度。字符串中的字符数可能太大，无法存储在 int 中。头文件 `<stddef.h>` 定义了一种变量类型 `ptrdiff_t`，它足够大，可以保存两个指针值的有符号差值。不过，如果我们谨慎一些，就会为 `strlen` 的返回值使用 `size_t`，以与标准库版本保持一致。`size_t` 是 `sizeof` 运算符返回的无符号整数类型。

### 注意

- 只要左侧是指向对象的指针，右侧是整数表达式，`+=` 和 `-=` 运算符就可以涉及指针。

## 13.10.4 比较指针

C 允许指针相互比较。如果两个指针比较相等，那么它们指向同一个东西，无论它是一个对象，还是数组末尾那个不存在的元素（参见上面的算术运算）。如果两个指针指向同一个东西，那么它们比较相等。诸如 >、<= 等关系运算符，在指针指向同一个数组时，会给出符合预期的结果：如果一个指针比较小于另一个指针，那么它指向更靠近数组前面的位置。考虑以下程序。

### 示例

```c
19. #include <stdio.h>
int main(void)
{
    int a[] = {10, 20, 30, 40, 50};
    int i, *p;
    for (p = a; p <= a + 4; p++)
        printf("%d\n", *p);
    return 0;
}
```

输出

```
10
20
30
40
50
```

在这里，每次都将 p 与数组的基地址进行比较。

指针比较的一个常见用途是使用指针复制数组。下面是一个代码片段，它使用指针把 10 个元素从 array1 复制到 array2。它使用结束指针 ep 来跟踪何时应停止复制。

```c
int array1[10], array2[10];
int *ip1, *ip2 = &array2[0];
int *ep = array1 + 10;
for (ip1 = &array1[0]; ip1 < ep; ip1++)
    *ip2++ = *ip1;
```

如前所述，并不存在元素 `array2[10]`，但计算指向这个（不存在的）元素的指针是合法的，只要它只用于像这样的指针比较（也就是说，只要不试图读取或存储它所指向的值，就是合法的）。

下面的程序将按逆序打印该行。该程序使用两个指向同一数组元素的指针，来说明指针比较。

### 示例

```c
20. #include <stdio.h>
    #include <string.h>
```
