
```
}
fputs(" \nTABLE OF SQUARES", fl);
fputs(" \n================\n", fl);

for(k = 1; k <= 5; k++)
{
    fprintf(fl, " %d\t%d\n", k, k*k);
}
fclose(fl);

return 0;
}
```

图 3.49 程序 fsquares2.c

### 例 3.28

编写一个程序，读取上一示例中创建的 **squares.txt** 的内容，并将其显示在屏幕上。

### 解 3.28

图 3.50 显示了程序清单（程序：**fdisp.c**）。该程序以读取模式打开 **squares.txt**。使用 **while** 循环通过 **getc** 从文件中读取字符，直到到达文件末尾（EOF）。函数 **putchar** 将文件中读取的字符显示在屏幕上。

```
/*---------------------------------------------
        READING DATA FROM A FILE
        =========================

This program shows how data can be read from a file

Author: Dogan Ibrahim
File  : fdisp.c
Date  : December 2020
--------------------------------------------------*/

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int c;
    FILE *fl;
```
```
if((fl = fopen("squares.txt", "r")) == NULL)
{
    printf("\nCould not open the file...\n");
    exit(0);
}

c = getc(fl);
while(c != EOF)
{
    putchar(c);
    c = getc(fl);
}
fclose(fl);

return 0;
}
```

图 3.50 程序 fdisp.c

图 3.51 显示了程序的一次示例运行。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_80_0.png)

图 3.51 程序示例运行

## 3.2.16 • 结构体

结构体用于当我们想要分组并操作相关但通常不同类型的数据时。例如，我们可能想要分组某人的个人数据，如姓名、年龄、身高、体重等。结构体在此类应用中非常高效，并使编程变得容易。

结构体使用关键字 **struct** 定义，后跟结构体名称。结构体主体包含结构体的元素。下面展示了一个示例结构体，可用于存储一个人的详细信息：

```
struct person
```
```
{
    char name[20];
    char surname[20];
    int age;
    float height;
    float weight;
};
```

需要认识到，上述内容只是一个模板，不占用内存中的任何空间。可以使用如下语句定义具有上述模板的 **struct** 类型变量。这里，变量 **p1** 是 **struct** 类型，并占用内存空间（注意 **p1** 是变量，而不是 person）：

```
struct person p1;
```

我们也可以定义模板并同时定义要使用的变量。示例如下：

```
struct person
{
    char name[20];
    char surname[20];
    int age;
    float height;
    float weight;
}p1, p2, p3;
```

在上述语句中，创建了一个名为 person 的结构体，并带有三个变量 **p1**、**p2** 和 **p3**，这些变量占用内存空间。

结构体的元素可以通过指定变量名、后跟一个点以及元素名来访问。下面给出一些示例：

```
p1.age = 25;
p1.height = 162.0;
```

结构体的大小是结构体占用的字节数。关键字 sizeof 可用于查找结构体变量的大小，如下所示：

```
sizeof(p1);
```

结构体可以使用赋值运算符相互复制：

```
p1 = p2;
```

结构体的元素可以使用花括号初始化：

```
struct person p1 = {val1, val2, val3,....};
```

下面展示一个初始化示例：

```
struct person
{
    char name[20];
    char surname[20];
    int age;
    float height;
    float weight;
} p1 = {"John", "Smith", 25, 162, 62};
```

下面给出一个示例。

### 例 3.29

编写一个程序，读取一个变量的姓名、姓氏、年龄、身高和体重，并将它们存储在结构体中。在屏幕上显示详细信息。

### 解 3.29

图 3.52 显示了程序清单（程序：struct.c）。使用变量 p1 创建了一个结构体。函数 scanf 用于读取个人详细信息，并将这些信息存储在结构体中。然后 printf 函数显示个人详细信息。

```
/*-----------------------------------------------
          Person Details
          =============

This example program shows how a structure can be used

Author: Dogan Ibrahim
File  : struct.c
Date  : December 2020
---------------------------------------------------*/

#include <stdio.h>

struct person
{
    char name[10];
    char surname[10];
    int age;
    float height;
    float weight;
```
```
}p1;

int main(void)
{
    printf("\nEnter name surname age height weight: ");
    scanf("%s %s %d %f %f", &p1.name,&p1.surname,&p1.age,&p1.height,&p1.weight);

    printf("\nName: %s\nSurname: %s\nAge: %d\nHeight: %f\nWeight: %f\n",
           p1.name,p1.surname,p1.age,p1.height,p1.weight);

    return 0;
}
```

图 3.52 程序 struct.c

图 3.53 显示了程序的一次示例运行。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_83_0.png)

图 3.53 程序示例运行

## 3.2.17 • 联合体

联合体与结构体类似，但在联合体中，所有成员共享公共存储空间。联合体的声明与结构体类似。下面展示一个联合体声明示例。这里，相同的内存位置用于存储多种数据类型。分配给联合体的内存足以容纳联合体中最大的成员。在下面的示例中，联合体占用 20 字节的内存空间：

```
union Data
{
        int i;
        float f;
        char name[20];
}MyData;
```

与结构体一样，sizeof 函数可用于查找联合体的大小。联合体成员的访问方式与结构体中相同。

下面给出一个示例，展示如何在程序中使用联合体。

### 例 3.30

编写一个程序，将一些数据存储在联合体中，并显示其内容。

### 解 3.30

图 3.54 显示了程序清单（程序：union.c）。该联合体存储一个整数、一个浮点数和一个字符串。图 3.55 显示了程序的输出。注意，整数变量和浮点变量的内容被破坏了。这是因为三个变量共享同一内存位置，向字符串加载数据破坏了另外两个变量的内容。

```
/*---------------------------------------------------------------
 Unions
 =====

This example program shows how a union can be used

Author: Dogan Ibrahim
File : union.c
Date : December 2020
--------------------------------------------------*/
#include <stdio.h>
#include <string.h>

union Data
{
 char name[20];
 int j;
 float k;
}p1;

int main(void)
{
 p1.j = 20;
 p1.k = 12.5;
 strcpy(p1.name, "Raspberry Pi");

 printf(" j: %d\n", p1.j);
 printf(" k: %f\n", p1.k);
 printf("name: %s\n", p1.name);

 return 0;
}
```

图 3.54 程序 union.c

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_85_0.png)

图 3.56 显示了修正后的程序（程序：**union2.c**），其输出如图 3.57 所示。

```
/*------------------------------------------------------
                         Unions
                         ======
This example program shows how a union can be used
Author: Dogan Ibrahim
File   : union2.c
Date   : December 2020
------------------------------------------------------*/
#include <stdio.h>
#include <string.h>

union Data
{
    char name[20];
    int j;
    float k;
}p1;

int main(void)
{
    p1.j = 20;
    printf("  j: %d\n", p1.j);

    p1.k = 12.5;
    printf("  k: %f\n", p1.k);

    strcpy(p1.name, "Raspberry Pi");
    printf("name: %s\n", p1.name);

    return 0;
}
```

图 3.56 程序 union2.c

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_85_1.png)

图 3.57 程序输出

## 3.2.18 • 指针

指针是 C 编程语言中非常重要的部分。指针保存内存中变量的地址，或者它指向变量的地址。指针通过指定其类型、后跟 * 字符和指针名称来定义：

```
char *ptr;
```

在上述示例中，**ptr** 是一个字符指针。类似地，我们可以有一个名为 **p** 的整数指针：

```
int *p;
```

我们可以用变量的地址初始化指针，如下所示。这里，字符变量 **c** 被赋值为 Z。**p** 被定义为字符指针，并用 **c** 的地址初始化，即 **p** 指向变量 **c** 的地址：

```
char c = 'Z';
char *p = &c;
```

上述赋值如图 3.58 所示，其中假设字符 j 位于地址 200。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_86_0.png)

间接运算符 * 可用于向指针所指向的内存地址赋值。例如，图 3.58 中位置 200 的内容可以通过以下语句改为 'Y'：

```
*p = 'Y';
```

下面给出一些使用指针的示例：

```
int a = 10;
int b;
int *p = &a;
```

