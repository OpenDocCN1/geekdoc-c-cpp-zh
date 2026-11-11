
赋给一个指针变量，该指针将存储所分配内存的地址。
如果内存分配失败（例如内存不足），`malloc` 将返回一个 `NULL` 指针。

## 示例

创建包含十个 `int` 对象数组的标准方法：
`int array[10];`
若要动态分配类似的数组，可以使用以下代码：

```c
/* 为包含十个 int 类型元素的数组分配空间。 */
int *ptr = malloc(10 * sizeof (int));
if (ptr == NULL) {
    /* 内存无法分配，程序应在此处适当处理错误。 */
} else {
    /* 如果 ptr 不为 NULL，则分配成功。 */
}
```

`malloc` 返回 `NULL` 表示没有可用内存，或者发生了其他阻止内存分配的错误。

## 编程问题

### 问题 1

编写一个程序，输入有多少个数字，然后输入这些数字，并借助 `malloc` 函数打印出它们之间的最大值。

#### 解决方案

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, max;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) malloc(n*sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    max=p[0];
    for(i=1;i<n;i++)
    {
        if(max<p[i])
            max=p[i];
    }
    printf("\n the maximum number is %d",max);
    getch();
}
```

### 问题 2

编写一个程序，输入有多少个数字，然后输入这些数字，并借助 `malloc` 函数打印出它们之间的最小值。

#### 解决方案

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, min;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) malloc(n*sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    min=p[0];
    for(i=1;i<n;i++)
    {
        if(min>p[i])
            min=p[i];
    }
    printf("\n the minimum number is %d", min);
    getch();
}
```

### 问题 3

编写一个程序，输入有多少个数字，然后输入这些数字，并借助 `malloc` 函数打印所有数字的总和。

#### 解决方案

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, sum=0;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) malloc(n*sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    for(i=0;i<n;i++)
    {
        sum=sum+p[i];
    }
    printf("\n the sum is %d",sum);
    getch();
}
```

## (b) calloc() 函数

`calloc` 函数为一个包含 `n` 个对象的数组分配空间，每个对象的大小为 `size`。该空间被初始化为所有位均为零。

标准 C 库将 `calloc()` 函数声明如下：

`void * calloc(size_t elements, size_t sz);`

我们也可以将 `calloc()` 函数的语法定义如下：

`<指针变量> = (<数据类型*>) calloc (元素个数, sizeof(数据类型));`

`calloc()` 为一个数组分配空间，每个元素占用 `sz` 字节的存储空间。每个元素的空间被初始化为二进制零。换句话说，`calloc()` 与 `malloc()` 类似，不同之处在于它处理的是对象数组而不是单个存储块，并且它会对所分配的存储进行初始化。以下示例使用 `calloc()` 分配了一个包含 100 个 `int` 的数组：

`int *p = (int*) calloc (100, sizeof(int));`

## 编程问题

### 问题 1

编写一个程序，输入有多少个数字，然后输入这些数字，并借助 `calloc` 函数打印出它们之间的最大值。

#### 解决方案

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, max;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) calloc(n,sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    max=p[0];
    for(i=1;i<n;i++)
    {
        if(max<p[i])
            max=p[i];
    }
    printf("\n the maximum number is %d", max);
    getch();
}
```

### 问题 2

编写一个程序，输入有多少个数字，然后输入这些数字，并借助 `calloc` 函数打印出它们之间的最小值。

#### 解决方案

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, min;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) calloc(n,sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    min=p[0];
    for(i=1;i<n;i++)
    {
        if(min>p[i])
            min=p[i];
    }
    printf("\n the minimum number is %d", min);
    getch();
}
```

### 问题 3

编写一个程序，输入有多少个数字，然后输入这些数字，并借助 `calloc` 函数打印所有数字的总和。

#### 解决方案

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, sum=0;
    clrscr();
    printf("\n enter how many elements");
    scanf ("%d", &n);
    p=(int *) calloc(n, sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    for(i=0;i<n;i++)
    {
        sum=sum+p[i];
    }
    printf("\n the Sum is %d",sum);
    getch();
}
```

## malloc() 与 calloc() 函数的区别

`malloc()` 和 `calloc()` 函数都用于分配动态内存。两者的运作方式略有不同。`malloc()` 接受一个大小并返回一个指向内存块的指针，该内存块至少为指定大小：`void *malloc( size_t size );` `calloc()` 接受元素个数以及每个元素的大小，并返回一个指向内存块的指针，该内存块至少足以容纳所有这些元素：

`void *calloc( size_t numElements, size_t sizeOfElement );`

这两个函数之间有一个主要区别和一个次要区别。主要区别在于 `malloc()` 不会初始化所分配的内存。第一次 `malloc()` 给你一个特定的内存块时，内存可能满是零。如果内存已被分配、释放和重新分配，那么它很可能没有被保留为零。这意味着，不幸的是，程序在简单情况下（内存从未被重新分配时）可能正常运行，但在更复杂的使用中（内存被重用时）可能会出问题。`calloc()` 将所分配的内存全部填充为零位。这意味着，任何你将用作 `char` 或任意长度的 `int`（无论有符号还是无符号）的内容都保证为零。任何你将用作指针的内容都被设置为全零位。这通常是一个空指针，但并不保证。任何你将用作 `float` 或 `double` 的内容都被设置为全零位；在某些类型的机器上这是一个浮点零，但并非在所有机器上都是如此。

这两个函数之间的次要区别是 `calloc()` 返回一个对象数组；`malloc()` 返回一个对象。有些人使用 `calloc()` 来明确表示他们想要一个数组。

## (c) free() 函数

当你使用 `malloc()` 或 `calloc()` 分配内存时，内存取自可用于程序的动态内存池。这个池有时被称为堆（heap），并且是有限的。当你的程序用完特定一块动态分配的内存时，你应该释放（deallocate）或释放（free）该内存，以便将来可以再次使用。要释放动态分配的内存，请使用 `free()`。其原型为

`void free(void *ptr);`

`free()` 函数释放由 `ptr` 指向的内存。这块内存必须是通过 `malloc()`、`calloc()` 或 `realloc()` 分配的。如果 `ptr` 为 `NULL`，`free()` 不执行任何操作。

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_266_0.png)

从上述图 (a) 中可以清楚地看到，栈的大小为 4 个位置，`Sp = -1` 表示栈为空，我们可以将新元素压入栈中。图 (b) 展示了当我们依次将元素 12、13 和 14 压入栈时栈的增长情况。图 (c) 展示了弹出 2 次后栈的状态。此时再对该栈执行一次弹出操作将导致一个称为“栈下溢”的错误。图 (d) 展示了在依次压入 16、17、18 和 19 后栈的内容。如果你试图再添加一个元素，栈将产生一个“栈上溢”错误。

**注意：** 我们也可以将 `SP` 称为栈指针。

## 栈的操作

栈上有两种操作，它们是：

- 压栈（Push）
- 弹栈（Pop）

### 1. 压栈（Push）

压栈操作用于向栈中插入一个新元素。在插入时，首先检查栈是否已满。如果栈已满，则生成错误消息“栈上溢”。

### 2. 弹栈（Pop）

弹栈操作用于从栈中删除一个元素。在删除时，首先检查栈是否为空。如果栈为空，则生成错误消息“栈下溢”。

### Push 和 Pop 函数的算法

#### 假设

- `sp` 为栈指针，其初始值为 -1
- `max_stack` 为栈的大小
- `stack[]` 为一个数组
- `element` 为要添加或删除的元素

#### 向栈中压入一个元素的算法

```
Step: 1) 开始
Step: 2) 获取要压入栈中的元素
Step: 3) 如果 (Sp == max_stack)
显示“栈已满”
否则
{
    Sp = Sp + 1
    stack[Sp] = item
}
Step: 4) 返回主程序
```

#### 从栈中弹出一个元素的算法

```
Step: 1) 开始
Step: 2) 如果 (Sp == -1)
显示“栈为空”
否则
{
    element = stack[Sp]
    Sp = Sp - 1
}
Step: 3) 返回元素
```

### 编程问题

#### 问题 1

下面给出的程序使用数组实现了栈数据结构。在该程序中，元素通过 `push()` 函数压入数组 `stack[]`。传递给 `push()` 的参数是数组的基地址、元素在栈中要放置的位置以及元素本身。`push()` 函数会注意确保用户不会试图将元素放置在超出栈边界的位置。这是通过检查存储在 `pos` 中的值来实现的。`pop()` 函数弹出存储在 `stack[]` 中的最后一个元素。因为 `top` 保存的是栈中最后一个元素的位置。

该问题也被称为栈的静态实现或栈的数组实现。

```c
/* 在栈中弹出和压入元素 */
#include<stdio.h>
```

