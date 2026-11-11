

```text
? New York
Strings are not equal
s1 = NewYork     length = 7 characters
s2 = York        length = 4 characters
s3 = NewYork     length = 7 characters
Enter two string constants
? London London
Strings are equal
s1 = London      length = 6 characters
s2 = London      length = 6 characters
s3 = London      length = 6 characters
```

**图 10.10** *字符串处理函数示意图*

### 实战习题 10.10

图 10.11 中的程序展示了如何编写一个 C 程序，该程序读取一个字符串并打印它是否为回文。

程序

```c
#include <stdio.h>
#include <conio.h>
#include <string.h>
void main()
{
char chk='t', str[30];
int len, left, right;
printf("\nEnter a string:");
scanf("%s", &str);
len=strlen(str);
left=0;
right=len-1;
while(left < right && chk=='t')
  {
  if(str[left] == str[right])
    ;
  else
  chk='f';
  left++;
  right--;
  }
if(chk=='t')
    printf("\nThe string %s is a palindrome",str);
else
    printf("\nThe string %s is not a palindrome",str);
getch();
}
```

输出

```text
    Enter a string: nitin
    The string nitin is a palindrome
```

**图 10.11** *检查字符串是否为回文的程序*

## 其他字符串函数

头文件 **<string.h>** 包含更多字符串处理函数。它们在某些情况下可能有用。

### strncpy

除了将一个字符串复制到另一个字符串的函数 **strcpy** 之外，我们还有另一个函数 **strncpy**，它仅将源字符串最左边的 *n* 个字符复制到目标字符串变量中。这是一个三参数函数，调用方式如下：

```c
strncpy(s1, s2, 5);
```

该语句将源字符串 **s2** 的前 5 个字符复制到目标字符串 **s1** 中。由于前 5 个字符可能不包含终止空字符，我们必须显式地将其放在 **s1** 的第 6 个位置，如下所示：

```c
s1[6] = '\0';
```

现在，字符串 **s1** 包含一个有效的字符串。

### strncmp

函数 **strcmp** 的一个变体是函数 **strncmp**。该函数有三个参数，如下面的函数调用所示：

```c
strncmp (s1, s2, n);
```

它将 **s1** 最左边的 *n* 个字符与 **s2** 进行比较，并返回：

- (a) 如果它们相等，则返回 0；
- (b) 如果 s1 的子字符串小于 s2，则返回负数；以及
- (c) 否则返回正数。

### strncat

这是另一个拼接函数，它接受三个参数，如下所示：

```c
strncat (s1, s2, n);
```

该调用会将 **s2** 最左边的 *n* 个字符拼接到 **s1** 的末尾。示例：

![](img/11b034a94fc590add0a7808250a38792_373_0.png)

![](img/11b034a94fc590add0a7808250a38792_373_1.png)

执行 **strncat (s1, s2, 4);** 后：

![](img/11b034a94fc590add0a7808250a38792_373_2.png)

### strstr

它是一个双参数函数，可用于在字符串中定位子字符串。它采用以下形式：

```text
strstr (s1, s2);
strstr (s1, "ABC");
```

函数 **strstr** 搜索字符串 **s1**，以查看字符串 **s2** 是否包含在 **s1** 中。如果是，该函数返回子字符串首次出现的位置。否则，它返回 NULL 指针。

示例：

```c
if (strstr (s1, s2) == NULL)
    printf("substring is not found");
else
    printf("s2 is a substring of s1");
```

我们还有用于确定字符串中是否存在某个字符的函数。函数调用

```c
strchr(s1, 'm');
```

将定位字符 'm' 第一次出现的位置，而调用

```c
strrchr(s1, 'm');
```

将定位字符串 **s1** 中字符 'm' 最后一次出现的位置。

### 警告

- 在声明期间为字符串分配空间时，请记住计入终止空字符。
- 当创建一个数组来保存未知大小的字符串变量的副本时，我们可以使用以下表达式计算所需的大小
  ```c
  strlen(stringname) + 1
  ```
- 当将一个字符串复制或拼接到另一个字符串时，我们必须确保目标（目的）字符串有足够的空间来容纳传入的字符。请记住，即使不满足此条件，也不会出现错误消息。复制可能会覆盖内存，程序可能会以不可预测的方式失败。
- 当我们使用 **strncpy** 从源字符串复制特定数量的字符时，必须确保将空字符追加到目标字符串，以防字符数小于或等于源字符串。

## 10.9 字符串表

学习目标 10.4

我们经常使用字符串列表，例如班级学生姓名列表、组织中员工姓名列表、地点列表等。姓名列表可以视为字符串表，并且可以使用二维字符数组来存储整个列表。例如，字符数组 `student[30][15]` 可用于存储 30 个姓名，每个姓名的长度不超过 15 个字符。下面显示的是一个包含五个城市的表：

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|
| C | h | a | n | d | i | g | a | r | h |
| M | a | d | r | a | s |   |   |   |   |
| A | h | m | e | d | a | b | a | d |   |
| H | y | d | e | r | a | b | a | d |   |
| B | o | m | b | a | y |   |   |   |   |

通过以下声明，可以方便地将该表存储在字符数组 `city` 中：

```c
char city[5][11] =
{
    "Chandigarh",
    "Madras",
    "Ahmedabad",
    "Hyderabad",
    "Bombay"
};
```

要访问列表中第 i 个城市的名称，我们写

```c
city[i-1]
```

因此，`city[0]` 表示 “Chandigarh”，`city[1]` 表示 “Madras”，依此类推。这表明，一旦数组被声明为二维，在进一步操作中就可以像一维数组一样使用它。也就是说，该表可以被视为一列字符串。

### 实战习题 10.11

H

编写一个按字母顺序对姓名列表进行排序的程序。

图 10.12 给出了一个按字母顺序对字符串列表进行排序的程序。它采用了第 9 章案例研究 1 中描述的冒泡排序方法。

程序

```c
#define ITEMS 5
#define MAXCHAR 20
main( )
{
    char string[ITEMS][MAXCHAR], dummy[MAXCHAR];
    int i = 0, j = 0;
/* Reading the list */
printf ("Enter names of %d items \n ",ITEMS);
while (i < ITEMS)
    scanf ("%s", string[i++]);
/* Sorting begins */
for (i=1; i < ITEMS; i++) /* Outer loop begins */
{
    for (j=1; j <= ITEMS-i ; j++) /*Inner loop begins*/
    {
        if (strcmp (string[j-1], string[j]) > 0)
        { /* Exchange of contents */
            strcpy (dummy, string[j-1]);
            strcpy (string[j-1], string[j]);
            strcpy (string[j], dummy );
        }
    } /* Inner loop ends */
} /* Outer loop ends */
/* Sorting completed */
printf ("\nAlphabetical list \n\n");
for (i=0; i < ITEMS ; i++)
    printf ("%s", string[i]);
}
```

输出

```text
Enter names of 5 items
London Manchester Delhi Paris Moscow
Alphabetical list
Delhi
London
Manchester
Moscow
Paris
```

**图 10.12** 按字母顺序对字符串进行排序

注意，使用二维数组来存储字符串列表。每个字符串都使用带 **%s** 格式的 **scanf** 函数读取。请记住，如果任何字符串包含空白字符，那么空白字符之后的字符串部分将被 **scanf** 视为列表中的另一项。在这种情况下，我们应该使用合适的算法将整行读取为字符串。例如，我们可以使用 **gets** 函数读取包含一系列单词的一行文本。我们也可以使用 **puts** 函数代替 **scanf** 进行输出。

