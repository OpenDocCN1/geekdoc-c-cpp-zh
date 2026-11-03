
8.14 下列语句的作用是什么？

```c
while ( ( m = getw(f1) ) != EOF )
printf("%5d", m);
```

8.15 下列代码段的作用是什么？

```c
for ( i = 1; i <= 5; i++ )
{
    fscanf(stdin, "%s", name);
    fprintf(fp, "%s", name);
}
. . .
```

8.16 下列函数的用途是什么？

- (a) feof()
- (b) ferror()

8.17 举例说明在程序中使用 feof 和 ferror。

8.18 我们能否在不重置文件指针的情况下从同一文件读取并写入？如果不能，为什么？

8.19 我们何时使用下列函数？

- (a) free ( )
- (b) rewind ( )

8.20 描述一种将一个文件的内容追加到另一个文件末尾的算法。

## 编程练习

- 8.1 编写一个程序，将一个文件的内容复制到另一个文件。
- 8.2 文件 DATA1 和 DATA2 包含已排序的整数列表。编写一个程序，生成第三个文件 DATA，其中保存这两个列表合并后的单个有序列表。使用命令行参数指定文件名。
- 8.3 编写一个程序，比较两个文件，如果相等则返回 0，如果不相等则返回 1。
- 8.4 编写一个程序，将一个文件追加到另一个文件的末尾。
- 8.5 编写一个程序，读取一个包含整数的文件，并在其末尾追加所有整数的和。
- 8.6 编写一个程序，提示用户输入两个文件，一个包含一行文本，称为源文件，另一个为空文件，称为目标文件，然后将源文件的内容复制到目标文件。
- 修改该程序，使得在将源文件复制到目标文件时，从源文件中删除指定字符。
- 8.7 编写一个程序，请求输入文件名和一个整数（称为偏移值）。程序然后从偏移值指定的位置开始读取文件，并将内容打印到屏幕上。

**注意：** 如果偏移值为正整数，则打印时跳过那么多行。如果为负数，则从文件末尾打印那么多行。如果出现任何错误，应打印适当的错误消息。
- 8.8 编写一个程序，创建一个顺序文件，用于存储五个产品的详细信息。详细信息包括产品代码、成本和可用项目数，并通过键盘提供。
- 8.9 编写一个程序，读取练习 14.8 中创建的文件，计算并打印所有五个产品的总价值。
- 8.10 重写练习 14.8 中开发的程序，将详细信息存储在随机存取文件中，并打印文件中交替产品的详细信息。修改该程序，使其能够在交互式指定产品代码时输出该产品的详细信息。

## 关键术语

- **文件名：** 它是由字符组成的字符串，构成操作系统有效的文件名。
- **ftell：** 它是一个函数，接受一个文件指针并返回一个 long 类型的数字，对应当前位置。
- **rewind：** 它是一个函数，接受一个文件指针并将位置重置到文件开头。
- **fseek：** 它是一个用于将文件位置移动到文件中所需位置的函数。

## 示例 A.1 编写一个程序，演示符号常量的使用。

程序
```c
/*Program for demonstrating use of Symbolic Constants*/
#include <stdio.h>
#include <conio.h>
#define CP 50 /*Defining Symbolic Constant for Cost Price*/

void main() {
    int SP, profit;
    clrscr();
    printf("Enter the SELLING PRICE ");
    scanf("%d", &SP);
    profit=SP-CP; /*Using Symbolic Constant CP in an expression*/
    printf("\nThe profit earned is %d", profit);
    getch();
}
```

输出
输入售价 65

获得的利润为 15

## 示例 A.2 编写一个程序，读取 dd/mm/yyyy 格式的日期，并判断输入的日期是否正确。

程序
```c
/*Program for demonstrating the use of scanf function*/
#include <stdio.h>
#include <conio.h>
void main()
{
int dd,mm,yyyy;
clrscr();
printf("Enter the date in dd mm yyyy format ");
scanf("%d %d %d", &dd, &mm, &yyyy); /*Reading the date values*/
/*Checking whether day, month, and year is correct */
if((dd==1 || dd==31 || mm==1 || mm==12 || yyyy==0 || (mm==2 && dd==29))
printf("NO");
else
printf("YES");
}
getch();
}
```

输出
输入 dd mm yyyy 格式的日期 22 09 2001
是

## A.2 计算机编程

## 示例 A.3 编写一个程序，判断输入数字是偶数还是奇数。

```c
/*Program for demonstrating use of Modulo Division Operator */
#include <stdio.h>
#include <conio.h>
void main()
{
int num;
clrscr();
printf("\nEnter a number : ");
scanf("%d",&num); /*Reading an Integer*/
if(num%2==0) /*Using % operator to compute the remainder value*/
printf("\n%d is an even number",num);
else
printf("\n%d is an odd number",num);
getch();
}
```

输出
输入一个数字：55
55 是奇数

## 示例 A.4 编写一个程序，将角度值转换为弧度。

程序
```c
/*Program for demonstrating real arithmetic*/
#include <stdio.h>
#include <conio.h>

void main()
{
    float deg, radian;
    clrscr();

    printf("Enter the degrees value ");
    scanf("%f", &deg);

    radian=(deg*3.14)/180.00; /*Using a formula for converting degrees to radians*/
    printf("\nThe equivalent value in radians is %.2f", radian);

    getch();
}
```

输出
输入角度值 120

对应的弧度值为 2.09

## 示例 A.5 编写一个程序，计算速度。

程序
```c
/*Program for demonstrating mixed-mode arithmetic*/
#include <stdio.h>
#include <conio.h>

void main()
{
    int d;
    float t;
    clrscr();
    /*Reading the values of distance and time*/
    printf("\nEnter the distance travelled in Kms: ");
    scanf("%d", &d);
    printf("\nEnter the travel time in hours: ");
    scanf("%f", &t);

    printf("\nSpeed = %.2f Km/h", d/t);/*Mixed-mode arithmetic expression*/
    getch();
}
```

输出
输入以公里为单位的行驶距离：380

输入以小时为单位的行驶时间：5.5

速度 = 69.09 公里/小时

## 示例 A.6 编写一个程序，求逻辑表达式 (10/2-4)&&(7%3)||(0/10) 的值。

```c
/*Program for demonstrating the use of logical operators*/
#include <stdio.h>
#include <conio.h>

void main()
{
clrscr();
if(((10/2-4)&&(7%3))||(0/10))/*Evaluating a logical expression*/
printf("True");
else
printf("False");
getch();
}
```

输出
真

## 示例 A.7 编写一个程序，演示自增运算符的使用。

```c
/*Program for demonstrating the use of increment operator*/
#include <stdio.h>
#include <conio.h>

void main()
{
int a=10;
clrscr();

/*Using Increment Operator*/
printf("a = %d",a);
printf("\n++a = %d",++a);
printf("\na = %d",a);
printf("\na++ = %d",a++);
printf("\na = %d",a);

getch();
}
```

输出
a = 10
++a = 11
a = 11
a++ = 11
a = 12

## 示例 A.8 编写一个程序，执行按位与和按位或运算。

程序
```c
/*Program for demonstrating the use of bitwise operators*/
#include <stdio.h>
#include <conio.h>

void main()
{
    char a='A',b='B';
    clrscr();

    printf("\na & b = %c",a&b);/*Using bitwise & operator*/
    printf("\na | b = %c",a|b);/*Using bitwise | operator*/

    getch();
}
```

输出
a & b = @
a | b = C

## 示例 A.9 编写一个程序，演示 sizeof 运算符的使用。

程序
```c
/*Program for demonstrating the use of sizeof operator*/
#include <stdio.h>
#include <conio.h>

void main()
{
    char a;
    int b;
    long c;
    float d;
    clrscr();
    /*Using the sizeof operator to compute the size of different datatypes*/
    printf("Size of char a = %u",sizeof(a));
    printf("\nSize of int b = %u",sizeof(b));
    printf("\nSize of long c = %u",sizeof(c));
    printf("\nSize of float d = %u",sizeof(d));
    getch();
}
```

输出
char a 的大小 = 1
int b 的大小 = 2
long c 的大小 = 4
float d 的大小 = 4

## 示例 A.10 编写一个程序，求解方程 x = a-b/3+c*2-1。

程序
```c
/*Program for demonstrating operator precedence in expression evaluation*/
#include <stdio.h>
#include <conio.h>

void main()
{
int a=9,b=12,c=3;
int x;
clrscr();

x=a-b/3+c*2-1;/*Expression evaluation*/
printf("Value of x = %d",x);/*Printing the resultant value x*/
getch();
}
```

输出
x 的值 = 10

## 示例 A.11 编写一个程序，求表达式 A/B*C+D/A 的值。

程序
```c
/*Program for demonstrating operator precedence in expression evaluation*/
#include <stdio.h>
#include <conio.h>

