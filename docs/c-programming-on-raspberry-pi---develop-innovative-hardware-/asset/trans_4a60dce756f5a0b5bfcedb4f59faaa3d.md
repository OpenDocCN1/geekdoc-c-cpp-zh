
```c
b = *p;            // b = a
*p = *p + 2;       // a = a + 2
*p = *p * *p       // a = a * a
(*p)++;            // a++
```

## 指针运算

指针可以递增、递减、相加、相减或比较，如下例所示：

- `p++` — 递增指针
- `p--;` — 递减指针
- `p = p + 10` — 给指针加上一个值
- `p1 = p1 + p2` — 两个指针相加
- `p = p - 5` — 从指针中减去一个值
- `p1 = p1 - p2` — 两个指针相减

可以使用字符指针创建字符串，如下所示。这里，指针 `p` 保存字符串第一个字符（`R`）的地址。注意，字符串会自动以 NULL 字符终止：

```c
char *p = "Raspberry Pi";
```

下面给出了在 C 程序中使用指针的示例。

### 例 3.31

编写一个函数，使用指针从基本原理出发计算字符串的长度。

### 解答 3.31

所需程序清单如图 3.59 所示（程序：`mystrlen.c`）。函数 `mystrlen` 有一个字符指针参数，它指向需要求长度的字符串。将字符串的内容与字符串终止符（NULL 字符）进行比较，并递增计数，直到找到字符串终止符。然后将计数返回给调用程序。主程序如图所示调用该函数。

```c
/*----------------------------------------
        STRING LENGTH
        =============

This program shows how a string length function can be
written using pointers and how this function can be used

Author: Dogan Ibrahim
File  : mystrlen.c
----------------------------------------------*/
#include <stdio.h>

int mystrlen(char *s)
{
    int cnt = 0;

    while(*s++ != '\0') cnt++;
    return(cnt);
}

int main(void)
{
    int len;

    char MyString[] = "Raspberry Pi";
    len = mystrlen(MyString);
    printf("String length = %d\n", len);

    return 0;
}
```

图 3.59 程序 mystrlen.c

### 例 3.32

编写一个函数，使用指针从基本原理出发将一个字符串复制到另一个字符串。

### 解答 3.32

所需程序清单如图 3.60 所示（程序：`mystrcpy.c`）。函数 `mstrcpy` 将源字符串中的字符复制到目标字符串，每次递增两个指针以指向下一个字符位置。主程序显示以下文本：

```text
Dest: Raspberry Pi
```

```c
/*--------------------------------------------------
                 STRING COPY
                 ===========

This program shows how a string can be copied to another
string using a function with pointers

Author: Dogan Ibrahim
File : mystrcpy.c
Date : December 2020
------------------------------------*/
#include <stdio.h>

void mstrcpy(char *d, char *s)
{
    while((*d++ = *s++) != '\0');
}

int main(void)
{
    int len;

    char MyString[] = "Raspberry Pi";
    char Dest[BUFSIZ];

    mstrcpy(Dest, MyString);
    printf("Dest: %s\n", Dest);

    return 0;
}
```

图 3.60 程序 mystrcpy.c

### 例 3.33

编写一个函数，使用指针从基本原理出发将一个字符串连接到另一个字符串。

### 解答 3.33

所需程序清单如图 3.61 所示（程序：`mystrcat.c`）。在函数 `mstrcat` 内部，指针 `p` 被设置为指向目标字符串的末尾。然后使用一个 while 循环，将源字符串追加到目标字符串的末尾。程序显示以下文本：

```text
Raspberry Pi Computer
```

```c
/*-----------------------------------------
STRING CONCATENATION
========================

This program shows how string concatenation can be done
using a function with pointers

Author: Dogan Ibrahim
```

数组 Numbers。构建一个 for 循环来显示数组的元素。注意，在循环中递增指针以访问数组的元素。运行程序时，显示以下内容：

```text
    1 3 5 7 9 11 13
```

```c
    /***********************************************************
    ARRAY ACCESS
    ===========

    This program shows how the elements of an array can be accessed
    using pointers

    Author: Dogan Ibrahim
    File   : parray.c
    Date   : December 2020
    -----------------------------------------------------------*/

    #include <stdio.h>
    #define nums 7

    int Numbers[] = {1, 3, 5, 7, 9, 11, 13};
    int *ptr = Numbers;
    int k;

    int main(void)
    {
        for(k = 0; k < nums; k++)
        {
            printf("%d ", *(ptr+k));
        }

        return 0;
    }
```

图 3.62 程序 parray.c

## 按引用将数组传递给函数

数组元素通常按引用传递给函数，函数使用这些值。除非将变量的地址传递给函数，否则函数不能修改作为参数传递的变量。可以使用指针将变量的地址传递给函数，以便函数可以修改这些变量。下面给出一些示例。

### 例 3.35

编写一个程序，按引用将两个变量传递给函数。该函数应递增这些变量的值。从函数返回后，主程序应显示这些变量的值。

### 解答 3.35

图 3.63 显示了程序清单（程序：`byref.c`）。函数 `Temp` 的参数是整数指针，因此期望传入两个整数的地址。该函数递增每个参数的值。主程序将变量 `a` 和 `b` 分别初始化为 10 和 20。然后如下显示 `a` 和 `b` 的内容。注意两个变量都递增了 1：

```text
a = 11  b = 21
```

```c
/***********************************************************
        PASSING ARGUMENTS TO A FUNCTION
        ================================

This program shows how arguments can be passed to a function
by reference so that the function can modify the variables

Author: Dogan Ibrahim
File  : byref.c
Date  : December 2020
***********************************************************/

#include <stdio.h>

void Temp(int *x, int *y)
{
    *x = *x + 1;
    *y = *y + 1;
}

int main(void)
{
    int a = 10;
    int b = 20;

    Temp(&a, &b);
    printf("a = %d  b = %d\n", a, b);

    return 0;
}
```

图 3.63 程序 byref.c

### 例 3.36

编写一个程序，将字符串转换为大写。

### 解答 3.36

图 3.64 显示了程序清单（程序：`convupper.c`）。函数 `UpperCase` 接收字符串的地址，并通过调用内置函数 `toupper` 将其转换为大写。然后主程序如下显示该字符串：

```text
MY RASPBERRY PI COMPUTER
```

```c
/*------------------------------------------------------------------
   CONVERT A STRING TO UPPER CASE
   ==============================

   This program converts a given string to upper case using pointers

   Author: Dogan Ibrahim
   File  : convupper.c
   Date  : December 2020
-------------------------------------------------------------------*/
#include <stdio.h>
#include <ctype.h>

void UpperCase(char *s)
{
    while(*s != '\0')
    {
        *s = toupper(*s);
        ++s;
    }
}

int main(void)
{
    char MyString[] = "my Raspberry Pi computer";
    UpperCase(MyString);
    printf("%s\n", MyString);

    return 0;
}
```

图 3.64 程序 convupper.c

## 指针数组

指针数组的一个常见用途是处理字符串。这里，数组中的每个条目都是一个字符串，并由数组索引指向。例如，考虑以下指针数组：

```c
char *names[4] = {"John", "James", "Mark", "Mary"};
```

在上面的声明中，`names[0]` 指向字符串 `John`，`names[1]` 指向字符串 `James`，`names[2]` 指向字符串 `Mark`，依此类推。下面给出一个示例。

### 例 3.37

编写一个程序，展示如何使用指针数组。声明一个函数来更改数组元素。

### 解答 3.37

图 3.65 显示了程序清单（程序：`apointers.c`）。主程序中声明了一个包含 5 个名字的指针数组。函数 `Chng` 将该数组的第三个元素从 `Jane` 更改为 `Susan`。程序显示以下内容：

- John
- Smith
- Susan
- Mark
- Mary

```c
/*--------------------------------------------------
                         ARRAY OF POINTERS
                         ================

This program is an example of array of pointers

Author: Dogan Ibrahim
File  : apointers.c
Date  : December 2020
--------------------------------------------------*/

#include <stdio.h>
#include <ctype.h>

void Chng(char *s[])
{
    s[2] = "Susan";
}

int main(void)
{
    char *names[5] = {"John", "Smith", "Jane", "Mark", "Mary"};
    int k;

    Chng(names);
}
```
