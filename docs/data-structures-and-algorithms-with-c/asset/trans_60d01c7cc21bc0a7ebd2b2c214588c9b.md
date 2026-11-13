

```c
scanf ("%d", &n);
p = (int**)malloc(m * sizeof(int*));
q = (int*)malloc(m * n * sizeof(int));
if (p==NULL || q==NULL)
{
    printf("Insufficient Memory");
    exit(1);
}
for(i=0; i<m; i++)
{
    p[i] = q;
    q += n;
}
printf("Enter the elements of the array\n");
for(i=0;i<m;i++)
    for(j=0;j<n;j++)
        scanf("%d", &p[i][j]);
printf("Elements of the array\n");
for(i=0; i<m; i++)
{
    for(j=0; j<n; j++)
    {
        printf("%5d",p[i][j]);
        printf("\n");
    }
}
```

输出：
Enter number of rows3
Enter number of columns3
Enter the elements of the array
11 12 13
21 22 23
31 32 33
Elements of the array
11 12 13
21 22 23
31 32 33

## 二维数组的非连续分配

二维数组的非连续分配用于需要创建大型二维数组（例如 1000 × 1000）和/或可能没有连续内存可用的情况。对于内存的非连续分配，每行的空间会根据需要单独分配。因此，总空间不是连续的。但是，每行的所有元素必须分配连续空间。

动态创建一个指针数组。该指针数组的大小与二维数组的行数相同，第 i 个数组元素应指向第 i 行的开头。

![](img/723fa3ef35f5102eb67dc45b74bb823d_99_0.png)

### 图 4.7：二维数组的非连续分配，但每行必须分配连续空间

### 示例：

```c
#include<stdio.h>
#include<stdlib.h>
main()
{
int **p, m, n, i, j;
printf("Enter number of rows");
scanf("%d", &m);
printf("Enter number of columns");
scanf("%d", &n);
p=(int**) malloc(m * sizeof(int*));
for(i=0; i<m; i++)
p[i] = (int*)malloc(n * sizeof(int));
printf("Enter the elements of the array");
for(i=0;i<m;i++)
{
for(j=0;j<n;j++)
scanf("%d", &p[i][j]);
}
printf("Elements of the array");
for(i=0;i<m;i++)
{
for(j=0;j<n;j++)
printf("%d", p[i][j]);
printf("\n");
}
}
```

输出：
Enter number of rows3
Enter number of columns3
Enter the elements of the array
11 12 13
21 22 23
31 32 33
Elements of the array
11 12 13
21 22 23
31 32 33

然而，二维数组动态内存分配的缺点如下：

- 额外的内存空间用于存储指针数组。
- 访问单个数组元素仅在第一级间接寻址后获得。

## 指针、数组和字符串

有时我们可以使用指针变量代替数组。假设 a 被声明为一维整型数组，p 被声明为指向整型的指针。

```c
int a[10];
```

我们可以用以下代替数组：

```c
int *p;
```

由于 p 未定义，因此 p 可能包含垃圾值，且 p 未自动分配一块内存。因此，在将指针变量用作数组替代之前，需要为其分配内存。

### 示例：

```c
p = (int *)malloc(100*sizeof(int));
```

该语句为 100 个整数值分配内存块。

### 示例：

```c
char *s;
scanf("%s",s); /* invalid */
or
char *s;
s = "Hello" /* invalid */
```

在使用指针变量之前，应分配一块内存。否则，可能会显示类似“段错误”的运行时错误。

### 示例：

```c
char *s;
s = (char*)malloc(10);
scanf("%s",s);
```

然而，在数组的情况下，内存块在编译时分配。

```c
char t[10];
scanf("%s", t); /* valid */
```

但不能给字符串变量赋值

```c
char t[10];
t = "Hello";
```

应使用库函数 strcpy() 来完成此操作

### 示例：

```c
char t[10];
strcpy(t, "Hello");
```

### 程序：如何在不使用 sizeof 运算符的情况下查找 int 数据类型的大小。

```c
#include<stdio.h>
main()
{
    int *ptr = 0;
    ptr++;
    printf("Size of int data type: %d",ptr);
}
```

## 总结

- 指针是可以指向另一个变量的变量。
- 该变量可以是整型、字符型或浮点型。
- 指针也可以指向另一个指针变量，此时该指针称为指向指针的指针。
- void 指针是一种指针，可以存储任何类型变量的地址。
- 有时在程序运行时需要分配内存空间。这种内存分配称为动态内存分配。
- malloc() 和 calloc() 函数用于在运行时分配内存空间。
- realloc() 函数用于修改先前分配的内存空间。
- free() 函数用于释放先前通过 malloc()、calloc() 或 realloc() 函数调用分配的内存空间。

## 练习

- 1. 什么是指针？
- 2. 间接运算符的用途是什么？如何使用间接运算符访问多维数组元素？
- 3. 什么是指向指针的指针？
- 4. 什么是 void 指针？什么是泛型函数？
- 5. 什么是悬空指针？
- 6. 如何使用指针访问数组中的元素？请用合适的示例说明。
- 7. 指向函数的指针如何工作？
- 8. 函数如何返回指向其调用函数的指针？请用合适的示例说明。
- 9. 什么是动态内存分配？动态内存分配相对于静态内存分配有什么优势？
- 10. malloc() 和 calloc() 函数有什么区别？
- 11. 编写一个使用指针计算数组中所有元素之和的程序。
- 12. 编写一个使用指针确定字符串长度的程序。
- 13. 编写一个使用指针交换内存中两个位置存储值的函数。
- 14. 编写一个程序动态生成 N 个元素的数组并按升序排序。
- 15. 编写一个使用动态内存分配进行矩阵乘法的程序。
- 16. 以下 C 程序的输出是什么？
  - (i)
    ```c
    main()
    {
    const int x = 5;
    int *ptr;
    ptr = &x;
    *ptr = 10;
    printf("%d", x);
    }
    ```
  - (ii)
    ```c
    main()
    {
    int a=2, *f1, *f2;
    f1 = f2 = &a;
    *f1=*f2+=a+=2.5;
    printf("%d %d %d", a, *f1, *f2);
    }
    ```
  - (iii)
    ```c
    main()
    {
    register int i =5;
    printf("Address of a=%u", &i);
    printf("Value of a=%d", i);
    }
    ```
  - (iv)
    ```c
    main()
    {
    int a=10;
    void *j;
    j=&a;
    j++;
    printf("%u", j);
    }
    ```
  - (v)
    ```c
    main()
    {
    char *p="Hello";
    printf("%c", *p);
    }
    ```
  - (vi)
    ```c
    main()
    {
    int i=320;
    char *ptr=(char *)&i;
    printf("%d",*ptr);
    }
    ```
  - (vii)
    ```c
    main()
    {
    static char str[]="Limericks";
    char *s;
    s=&str[6];
    while(*s)
    printf("%c", *s++);
    }
    ```

## 链表

> “整体等于其各部分之和”。- 欧几里得

- 单链表
- 双链表
- 循环链表
- 链式栈
- 链式队列
- 多项式表示

顾名思义，链表是由链接元素组成的线性列表。与数组一样，链表表示另一种线性数据结构。数组在大多数编程语言中是非常常用的数据结构。由于它存在若干局限性和缺点，因此需要一种替代方法。这些局限性可以通过使用链表数据结构来克服。

Allen Newell、Cliff Shaw 和 Herbert A. Simon 在 RAND 公司于 1955–1956 年为其信息处理语言开发了链表，将其作为主要数据结构。

### 数组的局限性

数组是用于存储同类元素集合的最常见数据结构。在大多数语言中，数组声明方便，且可在常数时间内快速访问任何元素。元素的地址是作为数组起始位置的偏移量计算的，这只需要一次乘法和一次加法。

在许多应用中，数组并不合适，因为它存在一些缺点。数组的缺点如下：

- 数组的最大尺寸需要事先预测。分配内存后无法更改数组大小，但许多应用需要调整大小。通常，此大小在编译时通过简单声明指定。数组大小可以推迟到运行时创建数组时确定，但之后保持固定。当数组从堆中动态分配时，可以使用 realloc() 动态调整其大小，但这需要程序员付出实际努力。
- 当程序员分配大尺寸数组时，数组中的大部分空间会被浪费。另一方面，当程序需要处理超过指定大小的数据时，代码就会崩溃。
- 数组的存储必须是连续可用的。所需存储空间并不总是立即可用。
- 插入和删除操作可能非常慢。最坏情况发生在需要删除或插入第一个元素时。几乎所有数组元素都需要移动。平均而言，大约一半的数组元素需要移动。因此，时间复杂度取决于元素总数，而非实际操作。
- 连接或拆分两个或多个数组比较困难。

