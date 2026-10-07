
```c
scanf("%d",&n);

printf("%d elements\n",n);

for(i=0;i<n;i++)

    scanf("%d",&a[i]);

b=a[0];

l=b;

printf("\entered array is \n");

for(i=0;i<n;i++,b++)

    printf("%d",b);
    if(b>l) {
        l=b;
        p=i+1;
printf("\nLargest element is %d at position %d",l,p);
getch();
}
```
Output:
Input array size 10
10 array elements
123 654 789 741 258 963 147 852 369 520
Entered array is 
123
654
789
741
258
963
147
852
369
520
Largest element is 963 at position 6

在列表 10 中，你可以看到我们声明了一个大小为 20 的数组和一个指针变量 `b`。当你输入数组的值时，通过 `for` 循环传递值。

# 字符串指针

字符串表示一组被称为字符数组的字符。因此，字符串指针等同于整数指针。当使用指针处理字符串时，程序员需要使用字符串终止符。让我们定义 `n` 如下：

char n[] = "vishal";
| 变量名 | n[0] | n[1] | n[2] | n[3] | n[4] | n[5] |
|---|---|---|---|---|---|---|
| 值 | v | i | s | a | l | |
| 地址 | 2001 | 2002 | 2003 | 2004 | 2005 | 2006 |

让我们创建一个 C 程序使用指针字符数组。列表 11 显示了程序的代码：

## 列表 11：创建字符指针

```c
#include<stdio.h>
main() {
    char a[10]="telephone";
    char *b="ba";
    int i;
    clrscr();
    printf("%u and b = %s\n", a,b);
    printf("\na[i] = %s\n",a[i],b);
    for(i=0;b[i]='\0';i++)
        printf("\n%c\t%s",a[i],b);
}
```

Output:
a = 65516 and b = ba
a[i] = telephone
t = 65517
l = 65518
e = 65519
p = 65520
h = 65521
o = 65522
n = 65523
e = 65524

从输出可以看出，存储一个字符需要一个字节。列表 11 中的 `for()` 循环如下代码：

```c
for(i=0;b[i]='\0';i++) {
    printf("\n%c\t%s",a[i],b);
    b++;
}
```

然而，你也可以将上述代码写如下：

```c
for(i=0;a[i]='\0';i++) {
    printf("\n%c\t%u",a[i],a[i]);
    i++;
}
```

# 436 第17章

```c
getch();
int strlen(char *s) {
    int len = 0;
    while (*s != '\0') {
        len++;
        s++;
    }
    return(len);
}
```

输出：

```
string = encyclopedia and its length = 12
```

在列表 12 中，我们通过指针计算了字符串的长度。然而，结果与用于查找字符串长度的 `strlen()` 函数相似。

![](img/655987774ce63b710f1a1b263f2c84e0_455_0.png)

在 C 程序中，目的与字符串函数 `strcmp()` 相同，用于按字符比较两个字符串。编译器检查 ASCII 值，如果值相等则继续执行；否则终止执行。这意味着如果任何任何字符与另一个字符串的对应字符不匹配，`break` 语句将导致控制权转移到循环末尾。列表 13 显示了比较两个字符串的代码：

### 列表 13：使用指针比较两个字符串

```c
#include <stdio.h>
#include <conio.h>
main() {
    char a[10],b[10];
    char *p,*q;
    int i,j,status=0;
    p;
    q;
    clrscr();
    printf("\nInput two strings\n");
    gets(a);
    gets(b);
    for(p=a,q=b; *p!='\0' || *q!='\0'; p++,q++)
        if(*p!=q) {
            printf("\nGiven strings are different\n");
            status=1;
            break;
        }
    if(status==0)
        printf("\nGiven strings are same\n");
    getch();
}
```

上述列表检查相似性的输出如下：

Two strings
computer
computer

Given strings are same

上述列表检查差异的输出如下：
Input two strings
Keyboard
Keyboard
Given strings are different

如果你 de忽略忽略大小写区别，对应的大写和小写情况之间的差值为 32；因此，A+32=a 或 a-32=A。

让我们创建一个 C 程序，使用指针将字符串的字符转换为大写字母。列表 14 显示了该代码：

### 列表 14：将字符串转换为大写

```c
#include<stdio.h>
main() {
    char a[20];
    char *p;
    int i;
    p=a;
    clrscr();
    printf("input string \n");
    gets(a);
    puts("entered string is \n");
    puts(a);
    printf("\nentered string in UPPERCASE is \n");
    for(*p=a;*p<='z';*p++) {
        if(*p>='A') *p-=32;
    }
    puts(a);
    getch();
}
```

输出：
input a string
computer engineering
entered string is
computer engineering

Entered string in UPPERCASE is
COMPUTER ENGINEERING

接下来，让我们创建一个 C 程序，使用指针合并两个字符串并将存储在第三个字符串中。列表 15 显示了该程序的代码：

### 列表 15：使用指针合并字符串

```c
#include<stdio.h>
#include<conio.h>
main() {
    char a[10],b[20], c[30];
    char *p,*q;
    int i,j;
    p=a;
    q=b;
    clrscr();
    printf("\ntwo strings \n");
    gets(a);
    gets(b);
    for(i=0;*p!='\0';*p++,i++) {
        c[i]=*p;
    }
    for(j=0;*q!='\0';*q++,j,i++) {
        c[i]=*q;
    }
    c[i]='\0';
    puts("entered strings are \n");
    puts(a);
    puts(b);
    printf("\nAfter combining \n");
    puts(c);
    getch();
}
```

输出：
input two strings computer
science
entered strings are
computer
science

After combining computerscience

在列表 15 中，程序代码：

```c
for(i=0;*p!='\0';*p++,i++) {
    c[i]=*p;
}
for(j=0;*q!='\0';*q++,j,i++) {
    c[i]=*q;
}
```

也可以写成：

```c
for(i=0;*p!='\0';c[i]=*p++,i++);
for(j=0;*q!='\0';c[i]=*q++,j,i++);
```

在前面的代码中，注意我们在循环声明中初始化了 `c[i]`。接下来，创建一个 C 程序查找给定字符串中的总空格数。列表 16 显示了该程序的代码：

### 列表 16：查找字符串中空白字符的次数

```c
#include<conio.h>
#include<stdio.h>
#include<string.h>
void main() {
    char ch[];
    int i=0;
    clrscr();
    printf("enter string \n");
    gets(ch);
    for(i=0;ch[i]!='\0';i++) {
        if(ch[i]==' ')
            i++;
    }
    printf("\nNumber of white spaces: %d\n", i);
    getch();
}
```

输出：
enter string
hello world
Number of white spaces: 1

```c
ptr = realloc(ptr,newsize);
```

上述语句为 `ptr` 指针变量分配了一个大小为 `newsize` 的新内存空间，并返回指向新内存第一个字节的指针。`newsize` 可能比原来的尺寸小，也可能大。新的内存块可能与旧内存块不在相同位置。如果该函数未能成功找到额外的内存，它将返回一个 `NULL` 值，且原始内存块将丢失。

让我们创建一个 C 程序来学习这些函数如何用于内存管理。列表 17 显示了该程序的代码：

```c
#include <stdio.h>
#include <conio.h>
#include <alloc.h>
main() {
    int *x, y, z;
    int i, num;
    clrscr();
    printf("Enter the number of elements you want in each array \n");
    scanf("%d",&num);
    x = (int*)malloc(num*sizeof(int));
    y = (int*)malloc(num*sizeof(int));
    z = (int*)malloc(num*sizeof(int));
    printf("\nEnter the elements of first array \n");
    for (i=0; i<num; i++) {
        scanf("%d",&x[i]);
    }
    printf("\nEnter the elements of second array \n");
    for (i=0; i<num; i++) {
        scanf("%d",&y[i]);
    }
    printf("\nThe new array is \n");
    for (i=0; i<num; i++) {
        *(z+i) = *(x+i) + *(y+i);
        printf("%d \n",*(z+i));
    }
}
getch();
```

输出：

Enter the number of elements you want in each array.
5
Enter the elements of first array
2 4 6 8 10
Enter the elements of second array
1 3 5 7 9
The new array is
3 7 11 15 19

在列表 17 中，我们创建了三个一维数组 `x`、`y` 和 `z`。其中前两个数组接收元素，并通过通过相加创建一个新数组。由前两个数组元素相加得到的结果存储在第三个数组中。

## 总结

在本章中，你学习了 C 语言中的指针。然后，你学习了如何声明指针变量、使用地址运算符、初始化指针变量以及对指针进行解引用。此外，你还学习了在指针上执行操作，如赋值、算术运算和比较。最后，你学习了如何在函数和数组中使用指针，以及在运行时分配内存。

## 快速复习

- Q1. 什么是指针？
- 答. 指针是一个变量，它存储了计算机内存中另一个变量的地址。指针变量只包含被引用变量的地址，而不包含存储在该地址的值。

- Q2. 按值调用和按引用调用的区别是什么？
- 答. 当你对调用函数的形式参数进行修改时，按值调用方法不会影响调用函数中实际参数的值。另一方面，当你按引用传递值时，调用函数中对形式参数的修改会改变实际参数。

- Q3. 列出内存管理中使用的不同函数。
- 答. 内存管理中使用的不同函数是：
  a. `malloc()` b. `calloc()` c. `free()` d. `realloc()`

- Q4. 你对解引用指针的理解是什么？
- 答. 解引用操作遵循指针的引用来获取它指向的变量的值。指针解引用是指通过指针间接对变量的值进行解引的过程。要存储变量的地址，你需要使用引用运算符 `&`。你可以如下方式获取变量的值：

现在，如果你想使用变量 `p` 所指向的值，可以使用解引用运算符 `*`：

```c
int i = 10;
int *p = &i;
```

printf("value at %p", *p);
```

- Q5. 写一个 C 程序使用指针创建一个变量。

- 答.

```c
#include <stdio.h>
#include <stdlib.h>
main() {
    int x, *p;
    clrscr(); /* 初始化指针 * */
    p = &x; /* 将 x 设为 0 */
    *p = 0;
    printf("x is %d\n", x);
    printf("p is %p\n", p);
    *p++; /* 增加 p 指向的内容 */
    printf("x is %d\n", x);
}
```

```c
(*p)++; /* 增加 p 指向的 * */
printf("x is %d\n", x);
getch();
}
```

输出：

```
x is 0
*p is 0
*x is 1
x is 2
```

- Q6. 写一个使用指针的 C 程序来反序打印字符串。答。

```c
#include <stdio.h>
#include <conio.h>
#include <string.h>
main() {
    char str1[] = "Reverse string";
    char str2[80], *ptr1;
    clrscr();
    ptr1 = str1 + strlen(str1) - 1;
    while (ptr1 >= '\0') {
        printf("%c", *ptr1);
        ptr1--;
    }
    getch();
}
```

输出：

The original string: Reverse string

- Q7. 使用指针写一个 C 程序交换两个变量的值。答。

```c
#include <stdio.h>
#include <conio.h>
main() {
    int a = 10, b = 20, temp;
    int *p1, *p2;
    clrscr();
    p1 = &a;
    p2 = &b;
    temp = *p1;
    *p1 = *p2;
    *p2 = temp;
    printf("a = %d, b = %d", a, b);
    getch();
}
```

输出：

a = 20, b = 10

- Q8. 下列程序的输出是什么？

```c
#include <stdio.h>
#include <conio.h>
main() {
    int x[] = {4,5,9,10};
    int y;
    clrscr();
    y = x[2];
    printf("%d", y);
}
```

答：9

- Q9. 下列程序的输出是什么？

```c
#include <stdio.h>
#include <conio.h>
main() {
    int x = 0;
    int y;
    clrscr();
    y = ++x;
    printf("%d", y);
}
```

答：17

- Q10. 下列程序的输出是什么？
