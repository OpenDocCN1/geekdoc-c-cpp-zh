
```c
/********************************************
      TABLES OF SQUARES
      ******************

Table of squares from 1 to 10

Author: Dogan Ibrahim
File   : squares.c
Date   : December 2020
********************************************/
#include <stdio.h>

int main(void)
{
    int k;

    printf("\nTABLE OF SQUARES");
    printf("\n=================\n");

    for(k = 1; k <= 10; k++)
    {
        printf("%4d\t%d\n", k, k*k);
    }

    return 0;
}
```

图 3.13 程序 squares.c

图 3.14 显示了该程序的运行示例。

```
TABLE OF SQUARES
=================
   1       1
   2       4
   3       9
   4      16
   5      25
   6      36
   7      49
   8      64
   9      81
  10     100
pi@raspberrypi:~ $ █
```

图 3.14 程序运行示例

## 例 3.9

编写一个程序，显示从 0° 到 20° 的正弦、余弦和正切三角函数表。

## 解答 3.9

所需程序清单（程序：**trig.c**）如图 3.15 所示。程序开头包含了数学库头文件 **<math.h>**。使用三角函数时，角度必须以弧度输入。程序将变量 **k** 中的度数转换为变量 **rad** 中的弧度，并在三角函数中使用该变量。

```c
/**********************************************************
              TABLE OF TRIGONOMETRIC FUNCTIONS
              ===============================
List of the table of trigonometric functions 0-20 Degrees

Author: Dogan Ibrahim
File   : trig.c
Date   : December 2020
**********************************************************/
#include <stdio.h>
#include <math.h>

int main(void)
{
    int k;
    float rad,s,c,t, Pi = 3.14159;

    printf("\nTABLES OF TRIGONOMETRIC FUNCTIONS");
    printf("\n==================================\n");
    printf("DEGREES\t SINE\tCOSINE\tTANGENT\n");

    for(k = 0; k <= 20; k++)
    {
        rad = k * Pi / 180.0;
        s = sin(rad);
        c = cos(rad);
        t = tan(rad);
        printf("  %d\t%6.4f\t%6.4f\t%6.4f\n", k, s,c,t);
    }

    return 0;
}
```

图 3.15 程序 trig.c

## 平方表

1 到 10 的平方表。程序在 5 次迭代后停止

作者：Dogan Ibrahim
文件：squares2.c
日期：2020 年 12 月

```
/*-------------------------------------------------
        TABLES OF SQUARES
        ================
Table of squares from 1 to 10. Program stops after 5 iterations

Author: Dogan Ibrahim
File  : squares2.c
Date  : December 2020
---------------------------------------------------*/

#include <stdio.h>

int main(void)
{
    int k;

    printf("\nTABLE OF SQUARES");
    printf("\n===============\n");

    for(k = 1; k <= 10; k++)
    {
        printf("%3d\t%3d\n", k, k*k);
        if(k == 5)break;
    }

    return 0;
}
```

图 3.17 程序 squares2.c

图 3.18 显示了该程序的运行示例。

```
TABLE OF SQUARES
===============
  1     1
  2     4
  3     9
  4    16
  5    25
pi@raspberrypi:~ $
```

图 3.18 程序运行示例

## 例 3.11

编写一个程序，显示 1 到 10 的整数平方，如例 3.8 所示。跳过数字 5 的表格。

## 解答 3.11

所需程序清单（程序：**squares3.c**）如图 3.19 所示。注意 **continue** 语句如何用于在 **for** 循环内跳过数字 5。

```c
/***********************************************
              TABLES OF SQUARES
              =================

Table of squares from 1 to 10. Number 5 is skipped in the loop

Author: Dogan Ibrahim
File  : squares3.c
Date  : December 2020
***********************************************/

#include <stdio.h>

int main(void)
{
    int k;

    printf("\nTABLE OF SQUARES");
    printf("\n================\n");

    for(k = 1; k <= 10; k++)
    {
        if(k == 5)continue;
        printf("  %d\t%d\n", k, k*k);
    }

    return 0;
}
```

图 3.19 程序：squares3.c

图 3.20 显示了该程序的运行示例。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_53_0.png)

## 3.2.8 数组

在程序开发过程中，通常需要记录同一类型的相关数据项。例如，我们可能想保存教室里学生的身高。在此类应用中，使用数组存储相关数据项很方便。

数组有类型和名称。例如，一个名为 age、包含 5 个元素的整数数组可以定义如下：

```
int age[5];
```

数组的每个元素都是唯一的。数组的索引始终从 0 开始，一直到所定义值减 1。因此，在上述定义中，数组 age 有 5 个元素，每个元素可按如下方式访问：

- age[0]
- age[1]
- age[2]
- age[3]
- age[4]

可以通过指定数组元素的索引并向其分配新数据来更改该元素的内容。在以下示例中，数组的第二个元素被改为 10：

```
age[1] = 10;
```

### 例 3.12

要求找出班级中学生的最大年龄。编写一个程序，读取学生人数及其年龄，并计算和显示教室中的最大年龄。

### 解答 3.12

所需程序清单（程序：**ages.c**）如图 3.21 所示。程序开始时读取学生人数并将其存储在变量 **no** 中。然后程序使用 **for** 循环读取年龄并将其存储在数组 **age** 中。第二个 **for** 循环用于查找最大年龄，然后显示该最大年龄。

~~~c
/******************************************
        MAXIMUM AGE OF STUDENTS
        ========================

Find the maximum age of students in a class

Author: Dogan Ibrahim
File  : ages.c
Date  : December 2020
------------------------------------------*/
#include <stdio.h>

int main(void)
{
    int k, no, maxage = 0;
    int age[50];

    printf("\nHow many students are there?: ");
    scanf("%d", &no);

    for(k = 0; k < no; k++)
    {
        printf("Enter age of student %d :", k+1);
        scanf("%d", &age[k]);
    }

    for(k = 0; k < no; k++)
    {
        if(age[k] > maxage)maxage = age[k];
    }

    printf("Maximum age = %d\n", maxage);

    return 0;
}
~~~

图 3.21 程序 ages.c

该程序的运行示例如图 3.22 所示。

```text
How many students are there?: 4
Enter age of student 1 :23
Enter age of student 2 :35
Enter age of student 3 :32
Enter age of student 4 :28
Maximum age = 35
pi@raspberrypi:~ $
```

图 3.22 程序运行示例

## 3.2.9 ● 字符串变量

在每种编程语言中，能够操作文本和字符都很重要。在 C 中，文本字符串表示为字符数组，其中第一个字符存储在索引 0 中。数组以空字符（'\0'）结尾，该字符是 ASCII 0。字符串声明如下所示：

```c
char name[] = "John";
```

注意，不必指定字符串长度，因为这由编译器计算。上述语句创建一个包含 5 个元素的字符数组，末尾包括空字符。字符在数组中的存储方式如下所示：

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| J | o | h | n | '\0' |

我们也可以指定数组大小如下：

```c
char name[10] = "John";
```

注意，指定的数组大小大于数组中的元素数量。这里，编译器在数组末尾分配额外空间，以便将来可以追加额外文本。如果数组长度未知，在声明数组时可以使用关键字 **BUFSIZ**。**BUFSIZ** 将数组大小设置为编译器允许的最大值。

数组的名称也是其在内存中的地址。因此，当需要输入数组的地址时，我们可以简单地输入其名称，或者通过在其第一个元素前使用 & 符号来指定其地址，例如 &name[0]。

可以使用 printf 示例中的 %s 限定符打印字符串，如下例所示。
