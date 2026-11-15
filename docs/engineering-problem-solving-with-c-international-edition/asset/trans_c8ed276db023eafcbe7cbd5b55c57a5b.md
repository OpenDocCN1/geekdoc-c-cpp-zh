

快速排序函数也通过一条语句递归调用，该语句指定从 x[break_pt+1] 开始的总共 n-break_pt-1 个值应被排序：

```
quicksort(&x[break_pt+1], n-break_pt-1);
```

请注意，实际参数使用 &x[break_pt+1]，即对 x[break_pt+1] 地址的引用。此地址引用是必要的，因为使用 x[break_pt+1] 会产生按值调用，而非按引用调用。快速排序函数和 separate 函数使用在第 6.2 节中开发的 switch2 函数。由于快速排序算法是一个复杂的算法，一个好的开始方法是使用手动示例，并利用该数据逐步执行这些语句。

/*---------------------------------------------*/
/* Program chapter6_9 */
/* */
/* This program tests the quicksort function. */
/*---------------------------------------------*/
#include <stdio.h>

int main(void)
{
/* Declare and initialize variables. */
int x[8]={4,10,3,6,-1,0,2,6}, npts=8, k;
void quicksort(int w[],int n);
int separate(int y[],int m);
void switch2(int *a,int *b);

/* Sort and print the array. */
printf("Before: ");
for (k=0; k<7; k++)
printf("%d ",x[k]);
printf("\n");
quicksort(x,npts);
printf("After: ");
for (k=0; k<7; k++)
printf("%d ",x[k]);
printf("\n");

/* Exit program. */
return 0;
}

/*---------------------------------------------*/
/* This function implements a quicksort algorithm. */
/*---------------------------------------------*/
void quicksort(int w[],int n)
{
/* Declare variables and function prototypes. */
int break_pt;
int separate(int y[],int m);
void switch2(int *a,int *b);

/* If only two elements, order them correctly. */
if (n == 2)
{
    if (w[0] > w[1])
        switch2(&w[0],&w[1]);
}
else
/* If more than two elements, separate into those */
/* greater than and those less than a breakpoint. */
if (n > 2)
{
    break_pt = separate(w,n);
    quicksort(w,break_pt);
    quicksort(&w[break_pt+1],n-break_pt-1);
}
/* Void return. */
return;
}

/*------------------------------------------------------*/
/* This function reorders the array such that y[0] is   */
/* correctly positioned and the values less than it are */
/* to the right and the values greater are to the left. */
int separate(int y[],int m)
{
    /* Declare variables and function prototypes. */
    int k1=1, k2=1, count=0, pivot;
    void switch2(int *a,int *b);

    /* Separate values into two groups. */
    pivot = y[0];
    while (k1<m && k2<m)
    {
        while ((k1<m) && (y[k1]>pivot))
            k1++;
        while ((k2<m) && (y[k2]<pivot))
            k2++;
        if ((k1<m) && (k2<m))
        {
            switch2(&y[k1],&y[k2]);
            count++;
        }
    }
}

/* Put pivot value in correct position. */
if (count > 0)
    switch2(&y[0],&y[count]);
else
{
    k1 = 0;
    while (((k1<m-1) && (y[k1]>y[k1+1])))
    {
        switch2(&y[k1],&y[k1+1]);
        k1++;
    }
    count = k1;
}
/* Return count. */
return count;
}
/*--------------------------------------------------*/
/* Correct function to switch values in two variables. */
/*--------------------------------------------------*/
void switch2(int *a,int *b)
{
    /* Declare variables. */
    int hold;
    /* Switch values in a and b. */
    hold = *a;
    *a = *b;
    *b = hold;
    /* void return. */
    return;
}
/*--------------------------------------------------*/

本章的重点是指针与其所指向变量之间的关系。示例展示了如何定义指针以及如何初始化它们。列出了可用于指针的有效操作类型，并更新了运算符的优先级关系，以包含地址运算符和间接运算符。给出了指针用作函数参数以及在数组引用中的示例。我们还介绍了一组用于处理字符串的函数；其中许多函数将指针用作函数参数。最后，我们介绍了允许使用指针进行动态内存分配的 C 语句。

![](img/02c4582f051c5b51776411c92b079035_350_0.png)

## 关键术语

- 地址
- 地址运算符
- 字节
- 字符串
- 连接
- 解引用
- 动态内存分配
- 间接
- NULL 字符
- 偏移量
- 指针
- 空指针

## C 语句摘要

指针声明：

```
int *ptr1;
double a, *ptr_2=&a;
```

动态内存分配：

```
x = (double *)malloc(npts*sizeof(double));
x = (double *)calloc(npts,sizeof(double));
```

## 注释

- 1. 为指针选择标识符，这些标识符应清楚地表明它们与指针变量相关联。
- 2. 如果指针最初未分配给内存位置，则赋予其 NULL 值，以指示它尚未被分配。

## 调试注释

- 1. 确保程序在其他语句中使用变量的值之前先初始化该变量。
- 2. 确保指针变量在用于引用值之前先被初始化。
- 3. 函数中与指针参数对应的实际参数必须是地址或指针。

## 问题

### 简答问题

### 判断题

指示以下陈述是正确 (T) 还是错误 (F)。

- 1. 地址运算符和间接运算符都是一元运算符。T F
- 2. 指针提供了一种访问特定数据项值的间接方式。T F
- 3. 在指针指向变量之前，必须始终先声明并初始化该变量。T F
- 4. 分配给动态内存空间的内存位置在程序编译时确定。T F

### 选择题

圈出完成每个陈述或每个问题正确答案的最佳选项字母。

- 5. 内存中的一个位置
- (a) 每当声明变量时都会保留。
- (b) 当变量在程序中使用时保留。
- (c) 可以同时保存多个不同的值。
- (d) 一旦被赋值，就不能再次使用。

- 6. 指针变量
- (a) 包含存储在内存位置中的数据。
- (b) 包含内存位置的地址。
- (c) 可用于输入语句，但不可用于输出语句。
- (d) 可以在输入和输出语句中更改为不同的值。

- 7. 如何将指针 a 引用的变量的值赋给变量名 name？
- (a) a = &name;
- (b) name = &a;
- (c) a = *name;
- (d) name = *a;

- 8. 假设 a 和 b 是指向整数的指针，且 a 指向变量 name。选择最能描述语句 b = a; 效果的句子：
- (a) name 的值被复制到 b。
- (b) a 中存储的内存地址被复制到 b。
- (c) b 中存储的内存地址被复制到 a。
- (d) 指针 a 现在指向另一个变量。

### 内存快照问题

- 9. 假设 name 的地址是 10，x 的地址是 14（即 name 存储在内存位置 10，x 存储在内存位置 14），执行以下语句集后，给出相应的内存快照：
- float name, x=20.5;
- float *a = &x;
- ...
- name = *a;

### 程序分析

问题 10-13 参照以下语句：

```
int i1, i2;
int *p1, *p2;
...
i1 = 5;
p1 = &i1;
i2 = *p1/2 + 10;
p2 = p1;
```

- 10. i1 的值是多少？
- 11. i2 的值是多少？
- 12. p1 的值是多少？
- 13. p2 的值是多少？

## 编程问题

### 通用函数

当我们希望从函数返回多个值时，指针常被用作函数参数。在以下每个问题中，编写指示的函数，然后开发一个 main 函数来测试该函数。

- 14. 编写一个函数，将圆的半径、直径和面积从英寸和平方英寸单位转换为英尺和平方英尺单位。假设相应的函数原型语句为

```
void convert_ft(double *r,double *d,double *a);
```

其中 r、d 和 a 分别是半径、直径和面积变量的指针。

- 15. 编写一个函数，重新排序三个整数变量中的值，使值按升序排列。假设相应的函数原型语句为

```
void reorder(int *a,int *b,int *c);
```

其中 a、b 和 c 分别是三个变量的指针。

- 16. 编写一个函数，从一维整数数组中确定最大值和最小值。假设相应的函数原型语句为

```
void ranges(int x[],int npts,int *max_ptr, int *min_ptr);
```

其中 npts 包含数组 x 中的值的数量，max_ptr 和 min_ptr 是指向用于存储数组中最大值和最小值的变量的指针。

- 17. 编写一个函数，返回一维整数数组的 double 类型平均值，同时确定数组中大于平均值的值的数量。假设相应的函数原型语句为

```
double average(int x[], int npts, int *gtr);
```

其中 npts 包含数组 x 中的值的数量，gtr 是指向存储 x 中大于平均值的值的数量的变量的指针。

- 18. 编写一个函数，返回整数数组中正值、零值和负值的数量。假设相应的函数原型语句为

```
void signs(int x[], int npts, int *npos, int *nzero, int *nneg);
```

其中 npts 包含数组 x 中的值的数量，npos、nzero 和 nneg 是指向用于存储数组中正值、零值和负值数量的变量的指针。

### 向量函数

向量是一组可以用一维数组表示的数值。这些问题开发用于操作向量中值的函数。然后请求对函数的引用，以展示如何使用函数来操作向量中的值组，而不是操作完整的集合中的

