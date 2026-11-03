
函数调用也可以嵌套。例如，像下面这样的语句

```
p = mul(mul(5,2),6);
```

是合法的。这表示两次顺序函数调用。内层函数调用先被求值，返回的值又作为外层函数调用的实际参数使用。如果 mul 返回其参数的乘积，那么 p 的值将是 60（= 5 × 2 × 6）。

## 10.13 递归

当一个被调用的函数又调用另一个函数时，就发生了“链式”调用过程。递归是这一过程的特殊情况，即函数调用自身。下面给出一个非常简单的递归示例：

```
main()
{
    printf("This is an example of recursion\n");
    main();
}
```

执行时，该程序将产生类似下面的输出：

This is an example of recursion
This is an example of recursion
This is an example of recursion
This is an ex

执行会突然终止；否则执行将无限继续下去。

递归的另一个有用示例是计算给定数字的阶乘。数字 n 的阶乘可表示为如下一系列重复乘法：

n 的阶乘 = n(n-1)(n-2)....1。

例如，

4 的阶乘 = 4 × 3 × 2 × 1 = 24

计算 n 的阶乘的函数如下：

```
factorial(n)
int n;
{
    int fact;
    if (n==1)
        return(1);
    else
        fact = n*factorial(n-1);
        return(fact);
}
```

让我们看看递归是如何工作的。假设 n = 3。由于 n 的值不是 1，因此语句

```
fact = n * factorial(n-1);
```

将在 n = 3 时执行。也就是说，

```
fact = 3 * factorial(2);
```

将被求值。右侧的表达式包含一次以 n = 2 调用 factorial 的调用。该调用将返回以下值：

```
2 * factorial(1)
```

factorial 再次以 n = 1 被调用。这一次，函数返回 1。操作序列可总结如下：

```
fact = 3 * factorial(2)
= 3 * 2 * factorial(1)
= 3 * 2 * 1
= 6
```

递归函数可以有效地用于求解那些其解可表示为对问题子集相继应用同一解法的问题。当我们编写递归函数时，必须在某处有一个 if 语句，强制函数在不执行递归调用的情况下返回。否则，函数将永远不会返回。

## 10.14 带数组的函数

与简单变量的值一样，也可以将数组的值传递给函数。要将数组传递给被调用函数，只需列出数组名（不带任何下标）以及数组大小作为参数。例如，调用

```
largest(a,n);
```

将传递大小为 n 的数组 a 中包含的所有元素。接受此调用的被调用函数必须被适当地定义。largest 函数的头部可能如下所示：

```
float largest(array, size)
float array[];
int size;
```

函数 largest 被定义为接受两个参数：数组名和数组大小（用于指定数组中元素的数量）。形式参数 array 的声明如下：

```
float array[];
```

这对括号告诉编译器，参数 array 是一个数字数组。此处不必指定数组的大小。

让我们考虑一个在元素数组中查找最大值的问题。程序如下：

```
main()
{
    float largest();
    static float value[4] = {2.5, -4.75, 1.2, 3.67};
    printf("%f\n", largest(value,4));
}
float largest(a,n)
float a[];
int n;
{
int i;
float max;
max = a[0];
for(i = 1; i < n; i++)
if(max < a[i])
max = a[i];
return(max);
}
```

当进行函数调用 largest(value, 4) 时，数组 value 的所有元素的值都被传递给被调用函数中数组 a 的对应元素。largest 函数找到数组中的最大值，并将结果返回给 main。

### 例 10.5

编写一个程序来计算一组值的标准差。数组元素从终端读取。使用函数计算标准差和平均值。

S.D. = \sqrt{\frac{1}{n} \sum_{i=1}^n (\bar{x} - x_i)^2}
其中 \bar{x} 是这些值的平均值。

图 10.11 展示了一个由 main、std-dev 和 mean 函数组成的多功能程序。main 从终端读取数组 value 的元素，并调用函数 std-dev 打印数组元素的标准差。std-dev 又调用另一个函数 mean 来提供数组元素的平均值。std-dev 和 mean 都被定义为 float，因此它们在各自调用函数的声明部分被声明为 float。

处理数组参数时，我们应记住一个主要区别。如果函数改变了数组元素的值，那么这些改变将作用于传递给该函数的原始数组。当整个数组作为参数传递时，数组的内容不会被复制到形式参数数组中；相反，有关数组元素地址的信息被传递给函数。因此，对数组元素所做的任何更改都会真实反映在调用函数中的原始数组里。

```
Program
/*
 FUNCTIONS WITH ARRAYS
 */
#include <math.h>
#define SIZE 5
main()
{
float value[SIZE], std_dev();
int i;
printf("Enter %d float values\n", SIZE);
for(i=0; i < SIZE; i++)
scanf("%f", &value[i]);
printf("Std deviation is %f\n", std_dev(value, SIZE));
}
float std_dev(a,n)
float a[];
int n;
{
int i;
float mean(), x = 0.0;
x = mean(a,n);
for(i=0; i < n; i++)
sum += (x-a[i])*(x-a[i]);
return(sqrt(sum/(float)n));
}
float mean(a,n)
float a[];
int n;
{
int i;
float sum = 0.0;
for(i=0; i < n; i++)
sum = sum + a[i];
return(sum/(float)n);
}
```

```
Output
Enter 5 float values
35.0 67.0 79.5 14.20 55.75
Std.deviation is 23.231582
```

图 10.11 将数组传递给函数

然而，当传递单个元素作为参数时，这并不适用。例 10.6 强调了这些概念。

### 例 10.6

编写一个使用函数对整数数组进行排序的程序。

图 10.12 给出了一个使用函数 sort() 对整数数组进行排序的程序。其输出清楚地表明，函数可以改变作为参数传递的数组中的值。

```
Program
/------------------------------------------------------------
/ SORTING OF ARRAY ELEMENTS
------------------------------------------------------------
main()
{
int i ;
static int marks[5] = {40, 90, 73, 81, 35};
printf("Marks before sorting\n");
for(i = 0; i < 5; i++)
    printf("%d", marks[i]);
printf("\n");
sort(5, marks);
printf("Marks after sorting\n");
for(i = 0; i < 5; i++)
    printf("%4d", marks[i]);
printf("\n");
}
sort(m,x)
int m, x[];
{
    int i, j, t;
    for(i = 1; i < m-1; i++)
        for(j = 1; j <= m-i; j++)
            if(x[j-1]>x[j])
            {
                t = x[j-1];
                x[j-1] = x[j];
                x[j] = t;
            }
}
Output
Marks before sorting
40 90 73 81 35
Marks after sorting
35 40 73 81 90
```

图 10.12 使用函数对数组元素进行排序

## 10.15 函数中变量的作用域和生命周期——存储类

C 中变量的行为与大多数其他语言中的变量不同。例如，在 BASIC 程序中，变量在整个程序期间都保留其值。在 C 中并非总是如此。这完全取决于变量可能采用的“存储”类。

如前所述，C 中的变量可以具有以下四种存储类中的任意一种：

- 1. 自动变量
- 2. 外部变量
- 3. 静态变量
- 4. 寄存器变量

我们将简要讨论上述每一类变量的作用域和生命周期。变量的作用域决定变量在程序的哪些部分实际可用于使用（活动）。生命周期指变量在程序执行期间保留给定值的时间段（存活）。因此，生命周期对给定变量的用途有直接影响。

根据声明位置的不同，变量也可以大致分为内部（局部）变量或外部（全局）变量。内部变量是在特定函数内声明的变量，而外部变量是在任何函数之外声明的变量。
