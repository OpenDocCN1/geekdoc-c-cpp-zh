

### Example:

```
r = p;
p = r;
or
r = q;
q = r;
where p, q, and r are declared as in the previous example.
```

void 指针可用作左值或右值。因此，通过使用此概念，void 指针允许违反指针类型转换的基本规则。

### Example:

```
r = p;
q = r;
where p is an integer pointer and q is a floating point pointer. This implies,
q = p;
```

## 泛型函数

void 指针用于编写泛型函数，该函数可以接受任何类型的参数。一组外观相同的函数，除了一个或多个参数的类型不同之外。泛型函数允许定义一个函数来替换该组函数。

假设我们有一个可用于交换两个整型变量值的函数。现在我们需要另一个函数来交换两个浮点型变量的值。对于交换两个长双精度型变量的值，我们还需要一个函数。因此，对于不同的数据类型，我们需要编写不同的函数。

### 示例:

```
/* Interchange the value of two variables */
#include<stdio.h>
void swap(int *a, int *b);
void swapf(float *a, float *b);
main()
{
    int i = 10, j = 20;
    float x = 12.3, y = 53.4;
    swap(&i, &j);
    printf("%i = %d, j = %d", i, j);
    swapf(&x, &y);
    printf("x = %f, y = %f", i, j);
}
/* Function to interchange two integer type variables*/
void swap(int *a, int *b)
{
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}
```

/* Function to interchange two floating-point type variables*/
void swapf(float *a, float *b)
{
    float temp;
    temp = *a;
    *a = *b;
    *b = temp;
}
```

与其使用一组类似类型的函数，不如使用泛型函数。泛型函数允许定义一个函数来替换该组函数。

### 示例:

```
/*Interchange the value of two variable using generic function */
#include<stdio.h>
void swap(void *a, void *b, int n);
main()
{
    int i = 10, j = 20;
    float x = 12.5, y = 53.5;
    swap(&i, &j, sizeof(int));
    printf("i = %d, j = %d\n", i, j);
    swap(&x, &y, sizeof(float));
    printf("x = %f, y = %f\n", x, y);
}
/* Generic function to interchange two variables */
void swap(void *a, void *b, int n)
{
    char *p, *q, temp;
    p = (char*)a;
    q = (char*)b;
    while(n>0)
    {
        temp = *p;
        *p = *q;
        *q = temp;
        p++;
        q++;
        n--;
    }
}
Output:
i = 20, j = 10
x = 53.500000, y = 12.500000
```

需要注意的是，字符始终是一个字节，字符指针充当字节指针。sizeof 运算符计算数据类型的字节大小。泛型函数依次交换两个变量的每个字节，因为每种类型的变量都可以视为字符序列。

## 悬空指针

悬空指针是指不指向正确类型的有效变量的指针。当内存被释放但未修改指针的值时，就会创建悬空指针，因此指针仍然指向已释放内存的内存位置。当系统将先前释放的内存重新分配给另一个进程，而原始程序解引用悬空指针时，可能会产生不可预测的结果，因为内存现在可能包含完全不同的数据。

### 示例:

```
{
    int *cp;
    {
        int c;
        cp = &c;
    }
/* c is in out of scope, cp is now a dangling pointer */
}
```

上述问题的解决方案是在退出内部块之前立即将 NULL 赋值给 cp。悬空指针的另一个常见来源是 malloc() 和 free() 库函数调用的组合：当指针指向的内存块被释放时，指针就会变成悬空指针。与前面的示例一样，避免这种情况的一种方法是在释放其引用后确保将指针重置为 null。

### 示例:

```
#include <stdio.h>
{
    int *cp = malloc (100);
    free ( cp ); /* cp now becomes a dangling pointer */
    cp = NULL; /* cp is no longer dangling */
}
```

## 指针允许的操作

允许的指针操作只有少数几种。允许的指针操作如下：

- 指针变量的自增和自减操作。
- 两个指针变量的减法。
- 指针与整数值的加法和减法。
- 两个指针变量之间的关系运算。
- 赋值操作。

> 注意：不接受任何类型的两个指针变量相加。

## 指针算术运算

允许指针变量与整数值进行加法和减法。但是，指针不允许进行其他算术运算，包括乘法和除法。指针变量不接受浮点数或双精度值等非整数值的加法或减法。

将整数添加到指针或从指针减去整数的格式如下：

```
Pointer-variable + integer-value
Pointer-variable - integer-value
```

可以用同一类型的另一个指针减去一个指针，结果将是整数，而不是指针。

### 示例:

```
int a[5] = {10, 20, 30, 40, 50};
int i, *p;
p = a + 1;
q = a + 3;
printf("%d", q - p);
Output:
2
```

## 指针的自增和自减操作

自增操作可用于指针变量，类似于给指针变量加一。自减操作也可用于指针变量，类似于从指针变量减一。指针自增或自减的格式如下：

```
Pointer-variable++
Pointer-variable--
```

指针自增与间接寻址的混合用法有三种可能：

- i) *++p
- ii) ++*p
- iii) ++*p

其中 p 是指针变量。

i) *++p 返回 p 所指向位置的内容，然后将指针递增一。指针 p 将指向下一个元素。自减运算符也可以以同样的方式与指针一起使用，以移动到前一个元素。请注意，如果下一个内存位置未由程序静态或动态分配，编译器可能会发出一些警告或错误消息。

### 示例:

```
int a[5] = {10, 20, 30, 40, 50};
int *p;
p = a;
printf("%d ", *p++);
printf("%d ", p - a);
printf("%d ", *p);
Output:
10 1 20
```

应该注意的是，自增 (++) 和自减 (--) 运算符的优先级高于间接运算符 (*) 的优先级。

ii) ++*p 将指针递增一，然后返回 p 所指向位置的内容。指针 p 将指向下一个元素。自减运算符也可以以同样的方式与指针一起使用，以移动到前一个元素。请注意，如果下一个内存位置未由程序静态或动态分配，编译器可能会发出一些警告或错误消息。

### 示例:

```
int a[5] = {10, 20, 30, 40, 50};
int *p;
p = a;
printf("%d ", ++*p);
printf("%d ", p - a);
printf("%d ", *p);
Output:
20 10 20
10 1 20
```

ii) ++*p 递增 p 所指向位置的值。指针 p 将指向同一个元素。自减运算符可以以同样的方式与指针一起使用，以递减所指向位置的值。

### 示例:

```
int a[5] = {10, 20, 30, 40, 50};
int *p;
p = a;
printf("%d ", ++*p);
printf("%d ", p - a);
printf("%d ", *p);
Output:
11 0 11
```

## 指针关系运算

可以使用不同的关系运算符将指针变量与同一类型的另一个指针变量进行比较。表 4.1 描述了指针允许的关系运算。

### 表 4.1：指针关系运算符

| 运算符 | 描述 |
| :--- | :--- |
| < | 小于 |
| <= | 小于或等于 |
| > | 大于 |
| >= | 大于或等于 |
| == | 等于 |
| != | 不等于 |

指针变量还可以与 NULL 指针进行比较。

表 4.2 显示了指针表示法和数组表示法。这些表示法基于以下代码：

```
int arr[] = {10, 20, 30, 40, 50};
int *ptr;
ptr = arr;
```

