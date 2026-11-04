
### 解决方案 3.17

图3.30显示了程序清单（程序：lencmp.c）。字符串 a 用文本 John Smith 初始化，并创建了一个名为 b 的空字符串。该程序将字符串 a 复制到字符串 b，并显示字符串 b 的内容。随后在屏幕上显示字符串 a 的长度。程序的其余部分展示了如何使用字符串比较函数。

```c
/*---------------------------------------------------------------
strlen and strcmp

This program is an example use of the strlen and strcmp

Author: Dogan Ibrahim
File : lencmp.c
Date : December 2020
-------------------------------------------------*/

#include <stdio.h>
#include <string.h>

int main(void)
{
    char a[]="John Smith";
    char b[BUFSIZ];

    strcpy(b, a);
    printf("My name is %s\n", b);
    printf("Length of my name is %d characters\n", strlen(a));

    printf("%d\n",strcmp("Smith", "Smith"));
    printf("%d\n",strcmp("Smith", "Smit"));
    printf("%d\n",strcmp("Smit", "Smith"));
    printf("%d\n",strcmp("Smith", "Smiti"));
    printf("%d\n",strcmp("Smith", "John"));

    return 0;
}
```

图3.30 程序 lencmp.c

程序的示例运行如图3.31所示。

```text
My name is John Smith
Length of my name is 10 characters
0
1
-1
-1
1
pi@raspberrypi:~ $
```

图3.31 程序的示例运行

- **strcat：** 该函数将一个字符串连接到另一个字符串的末尾。
- **strchr：** 该函数在字符串中搜索指定字符的首次出现。
- **toupper：** 该函数将字符转换为大写。
- **tolower：** 该函数将字符转换为小写。

### 示例 3.18

编写一个程序，展示字符串函数 **strcat**、**strchr** 和 **toupper** 如何在程序中使用。

### 解决方案 3.18

图3.32显示了程序清单（程序：**catchr.c**）。该程序将字符串 **John Smith** 连接到数组 c。函数 **strchr** 用于检查该文本是否包含字符 **S**，并显示一条消息。然后将文本转换为大写字母并显示在屏幕上。

```c
/*--------------------------------------------------------
                    strcat, strchr and toupper

This program is an example use of the strcat,strchr and toupper

Author: Dogan Ibrahim
File : catchr.c
Date : December 2020
--------------------------------------------------------*/

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main(void)
{
    char a[]="John";
    char b[] = " Smith";
    char c[BUFSIZ];
    char u[BUFSIZ];
    int i;

    //
    // Using strcat
    //
    strcat(c, a);
    strcat(c, b);
    printf("My name is %s\n", c);


    //
    // Using strchr
    //
    if(strchr(c, 'S') != 0)
            printf("S was found in string %s\n", c);
    else
            printf("String %s does not contain S\n", c);


    //
    // Using toupper
    //
    for(i = 0; i < strlen(c); i++)
    {
            u[i] = toupper(c[i]);
    }
    printf("Upper case of %s is %s\n", c, u);


    return 0;
}
```

图3.32 程序 catchr.c

程序的示例运行如图3.33所示。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_64_0.png)

图3.33 程序的示例运行

### 示例 3.19

编写一个程序，展示字符串函数 **strcat** 和 **strcpy** 如何在程序中使用。

### 解决方案 3.19

图3.34显示了程序清单（程序：cpy.c）。该程序形成字符串 John-Smith 并显示在屏幕上。

```c
/*--------------------------------------------------------
                  strcpy and strcat

   This program is an example use of the strcpy and strcat

   Author: Dogan Ibrahim
   File  : cpy.c
   Date  : December 2020
----------------------------------------------------------*/

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main(void)
{
   char a[]="John";
   char b[] = "Smith";
   char c[] = "-";
   char d[BUFSIZ];


   //
   // Using strcpy
   //
   strcpy(d, a);                       // d=John
   strcat(d, c);                       // d=John-
   strcat(d, b);                       // d=John-Smith
   printf("My name is %s\n", d);

   return 0;
}
```

图3.34 程序 cpy.c

该程序显示以下文本：

My name is John-Smith

## 3.2.12 • 字符宏

有几个有用的宏可用于测试各种字符。在使用这些宏之前，必须在程序开头包含头文件 <ctype.h>。

| 函数 | 描述 |
|---|---|
| isalnum(c) | 测试是否为字母数字（a-z、A-Z、0-9） |
| isalpha(c) | 测试是否为字母（a-z、A-Z） |
| isdigit(c) | 测试是否为数字（0-9） |
| islower(c) | 测试是否为小写 |
| isupper(c) | 测试是否为大写 |
| isprint(c) | 测试是否为可打印字符 |
| ispunct(c) | 测试是否为标点字符 |
| isxdigit(c) | 测试是否为十六进制字符 |

### 示例 3.20

编写一个程序，展示字符宏 isalpha 和 isdigit 如何在程序中使用。

### 解决方案 3.20

图3.35显示了程序清单（程序：tmacro.c）。提示用户输入一个字符。程序检查输入的字符，并根据用户输入的字符类型显示消息“You entered a digit”或“You entered alpha character”。程序在循环中运行，用户可以在提示“Continue (y/n)?”中输入 y 或 Y 来继续：

```c
/*---------------------------------------------------------------
Character macros

This program is an example of using the isdigit and isalpha

Author: Dogan Ibrahim
File : tmacro.c
Date : December 2020
---------------------------------------------------------------*/

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main(void)
{
    char ch, yn = 'Y';

    while(yn == 'Y')
    {
        printf("\nEnter a character: ");
        scanf("%c%*c", &ch);

        if(isdigit(ch))printf("\nYou entered a digit");
        else if(isalpha(ch))printf("\nYou entered alpha character");
```

```text
How many numbers are there? : 5
Enter number 1: 12
Enter number 2: 10
Enter number 3: 18
Enter number 4: 25
Enter number 5: 20
Average = 17.000000
pi@raspberrypi:~ $
```

图3.38 程序的示例运行

## 3.2.14 • 用户函数

通过将大型程序分解为更小、更易管理的部分，开发起来会更容易。函数就是用于此目的。当程序中需要重复执行某一组操作时，也会使用函数。例如，如果需要在程序的不同位置计算一些数字的平均值，将求平均值的代码编写为函数，并在需要时从主程序调用该函数，会更容易。

用户函数的一般格式如下：

```
type name(parameter list)
{
    statements inside the function
    optional return
}
```

函数的类型可以是有效变量类型之一，例如 char、int、float 等。函数将指定类型的变量返回给调用程序。如果函数不向调用程序返回任何数据，可以使用 void 关键字。函数名是有效的 C 变量名。括号内的参数是可选的，取决于应用。return 关键字是可选的，并且必须在 return 语句之后指定要返回给主程序的数据。

从主程序调用函数时，需要指定函数名，后跟一组括号。使用的任何参数都必须在括号内指定。下面给出一些示例。

### 示例 3.22

编写一个函数来计算三角形的面积。三角形的底和高将从键盘读取，并作为参数传递给该函数。

### 解决方案 3.22

所需的程序清单（程序：Func1.c）如图3.39所示。三角形的底和高从键盘读取，并传递给名为 **TriangleArea** 的函数。该函数返回计算出的面积，然后由主程序显示。

```c
/*-------------------------------------------------------------

    Example use of a function

This program is an example use of a function

Author: Dogan Ibrahim
File  : Func1.c
Date  : December 2020
-------------------------------------------------------------*/

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

float TriangleArea(float h, float b)
{
    float area;
    area = h * b / 2;
    return(area);
}

int main(void)
{
    float base, height, area;

    printf("\nAREA OF A TRIANGLE");
    printf("\nEnter the base and height of the triangle: ");
    scanf("%f %f", &base, &height);
    area = TriangleArea(height, base);
    printf("\nArea = %f\n", area);

    return 0;
}
```

图3.39 程序 Func1.c

程序的示例运行如图3.40所示。

```text
AREA OF A TRIANGLE
Enter the base and height of the triangle: 12 4
Area = 24.000000
pi@raspberrypi:~ $
```

图3.40 程序的示例运行
