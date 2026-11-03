
## 9.8 字符串处理函数

幸运的是，C 库支持大量字符串处理函数，可用于执行迄今为止讨论的许多字符串操作。以下是最常用的字符串处理函数。

| 函数 | 作用 |
|---|---|
| strcat() | 连接两个字符串 |
| strcmp() | 比较两个字符串 |
| strcpy() | 将一个字符串复制到另一个字符串 |
| strlen() | 查找字符串的长度 |

我们将简要讨论如何在使用字符串处理中应用这些函数。

### strcat() 函数

strcat 函数将两个字符串连接在一起。其形式如下：

```
strcat(string1, string2);
```

string1 和 string2 是字符数组。当执行 strcat 函数时，string2 会被追加到 string1。它通过移除 string1 末尾的空字符并从那里放置 string2 来实现。string2 中的字符串保持不变。例如，考虑以下三个字符串：

![](img/65953ea584e494f3d396b2252cb5ea53_240_0.png)

![](img/65953ea584e494f3d396b2252cb5ea53_240_1.png)

![](img/65953ea584e494f3d396b2252cb5ea53_240_2.png)

执行语句

```
strcat(part1, part2);
```

将得到结果：

![](img/65953ea584e494f3d396b2252cb5ea53_240_3.png)

![](img/65953ea584e494f3d396b2252cb5ea53_240_4.png)

而语句

```
strcat(part1, part3);
```

将得到结果：

![](img/65953ea584e494f3d396b2252cb5ea53_241_0.png)

![](img/65953ea584e494f3d396b2252cb5ea53_241_1.png)

我们必须确保 string1（string2 被追加到的字符串）的大小足够容纳最终的字符串。

strcat 函数也可以将字符串常量追加到字符串变量。以下写法是有效的。

```
strcat(part1, "GOOD");
```

C 允许嵌套 strcat 函数。例如，语句

```
strcat(strcat(string1,string2), string3);
```

是允许的，并且将三个字符串全部连接在一起。结果字符串存储在 string1 中。

### strcmp() 函数

strcmp 函数比较由参数指定的两个字符串，如果它们相等则返回值为 0。如果不相等，则返回字符串中第一个不匹配字符之间的数值差。其形式为：

```
strcmp(string1, string2);
```

string1 和 string2 可以是字符串变量或字符串常量。示例有：

```
strcmp(name1, name2);
strcmp(name1, "John");
strcmp("Rom", "Ram");
```

我们主要关心的是确定字符串是否相等；如果不相等，哪一个在字母顺序上靠前。不匹配的值很少重要。例如，语句

```
strcmp("their", "there");
```

将返回 -9 的值，这是 ASCII "i" 和 ASCII "r" 之间的数值差。即 ASCII 码中 "i" 减去 "r" 为 -9。如果值为负，则 string1 在字母顺序上高于 string2。

### strcpy() 函数

strcpy 函数的工作方式几乎像一个字符串赋值运算符。其形式为

```
strcpy(string1, string2);
```

并将 string2 的内容赋给 string1。string2 可以是字符数组变量或字符串常量。例如，语句

```
strcpy(city, "DELHI");
```

将把字符串 “DELHI” 赋给字符串变量 city。同样，语句

```
strcpy(city1, city2);
```

将把字符串变量 city2 的内容赋给字符串变量 city1。数组 city1 的大小应足够大以接收 city2 的内容。

### strlen() 函数

该函数计算并返回字符串中的字符数。

```
n = strlen(string);
```

其中 n 是一个整数变量，接收字符串长度的值。参数可以是字符串常量。计数在第一个空字符处结束。

### 示例 9.8

s1、s2 和 s3 是三个字符串变量。编写一个程序读取两个字符串常量到 s1 和 s2 中并比较它们是否相等。如果不相等，则将它们连接在一起。然后将 s1 的内容复制到变量 s3。最后，程序应打印三个变量的内容及其长度。

程序如 图 9.9 所示。在第一次运行中，输入字符串为 “New” 和 “York”。这些字符串由语句比较

```
x = strcmp(s1, s2);
```

由于它们不相等，它们被连接在一起并使用语句复制到 s3 中

```
strcpy(s3, s1);
```

程序输出三个字符串及其长度。在第二次运行中，两个字符串 s1 和 s2 相等，因此它们不会被连接。在这种情况下，三个字符串都包含相同的字符串常量 “London”。

## 9.9 字符串表

我们经常使用字符字符串列表，例如班级学生姓名列表、组织员工姓名列表、地点列表等。姓名列表可以视为字符串表，并且可以使用二维字符数组来存储整个列表。例如，字符数组 student[30][15] 可用于存储最多 30 个姓名列表，每个姓名长度不超过 15 个字符。

下面是一个五个城市的表：

|   | C | h | a | n | d | i | g | a | r | h |
|---|---|---|---|---|---|---|---|---|---|---|
| M | a | d | r | a | s |   |   |   |   |
| A | h | m | e | d | a | b | a | d |   |   |
| H | y | d | e | r | a | b | a | d |   |   |
| B | o | m | b | a | y |   |   |   |   |

该表可以方便地存储在字符数组 city 中，使用以下声明：

```c
static char city[][]
{
    "Chandigarh",
    "Madras",
    "Ahmedabad",
    "Hyderabad",
    "Bombay"
};
```

访问列表中第 i 个城市的名称，我们写 city[i-1]

```
Program
/*******************************************************/
/* ILLUSTRATIONS OF STRING-HANDLING FUNCTIONS */
/*******************************************************/

#include <string.h>
main()
{
    char s1[20], s2[20], s3[20];
    int x, l1, l2, l3;
    printf("\nEnter two string constants \n");
    printf("?");
    scanf("%s %s", s1, s2);
    /* comparing s1 and s2 */
    x = strcmp(s1, s2);
    if(x != 0)
    {
        printf("\n\nStrings are not equal \n");
        strcat(s1, s2); /* joining s1 and s2 */
    }
    else
        printf("\nStrings are equal \n");
    /* copying s1 to s3 */
    strcpy(s3, s1);
    /* Finding length of strings */
```

```
l1 = strlen(s1);
l2 = strlen(s2);
l3 = strlen(s3);

/* output */
printf("\ns1 = %s\tlength = %d characters\n", s1, l1)
printf("\ns2 = %s\tlength = %d characters\n", s2, l2);
printf("\ns3 = %s\tlength = %d characters\n", s3, l3);
}
Output
Enter two string constants
? New York
Strings are not equal

s1 = New York      length = 7 characters
s2 = York          length = 4 characters
s3 = New York      length = 7 characters

Enter two string constants
? London   London
Strings are equal

s1 = London        length = 6 characters
s2 = London        length = 6 characters
s3 = London        length = 6 characters
```

### 图 9.9 字符串处理函数的说明

因此 city[0] 表示 "Chandigarh"，city[1] 表示 "Madras"，以此类推。这表明一旦数组被声明为二维，就可以在进一步的操作中像一维数组一样使用。也就是说，该表可以被视为字符串的列。

### 示例 9.9

编写一个程序，按字母顺序对姓名列表进行排序。

对字符串列表按字母顺序排序的程序在图 9.10 中给出。它采用了上一章案例研究 1 中描述的冒泡排序方法。

```
Program
/*
************************************************************/
*          SORTING STRINGS IN ALPHABETICAL ORDER          */
************************************************************/
#define ITEMS   5
#define MAXCHAR 20
main()
{
    char string[ITEMS][MAXCHAR], dummy[MAXCHAR];
    int i = 0, j = 0;
    /* Reading the list */
    printf("\nEnter names of %d items \n",ITEMS);
    while (i < ITEMS)
        scanf("%s", string[i++]);
```
