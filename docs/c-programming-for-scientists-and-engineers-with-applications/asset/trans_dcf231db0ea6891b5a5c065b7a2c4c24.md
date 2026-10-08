

# 440 一维数组

```c
arrtemp = array1[i];
array1[i] = array1[j];
array1[j] = arrtemp;

return;
}
```

```c
void funcoutput(float array1[], int numelml1) {
    FILE *outptr;
    outptr = fopen("output.dat", "w");
    int i;

    for (i = 0; i < numelml1; i++)
        fprintf(outptr, "%.6f ", array1[i]);

    return;
}
```

输入文件：sortdata.dat
====================
14.00 .50 -7.00 45.00 6.30

输出文件：output.dat
===================
-7.00 .50 6.30 14.00 45.00

### 冒泡排序

这是一种交换排序。在这种排序中，数组元素从底到顶进行比较。当任何相邻元素顺序不对时，它们就会进行交换。这导致当数组按降序排序时，最大的元素会浮到顶部；而当数组按升序排序时，最小的元素会移动到顶部。在下次遍历中，下一个最大的（降序）或下一个最小的（升序）将移动到它的排序位置。下面的示例显示了对短列表进行降序排序所需的两次遍历的结果。

| 原始列表 | 交换 | 第1次遍历后 | 交换 | 第2次遍历后 |
|---|---|---|---|---|
| 9 | . | 15 | . | 15 |
| 15 | 9 | 9 | 12 | 12 |
| 8 | 12 | 12 | 9 | 9 |
| 7 | 12 | 8 | . | 8 |
| 12 | 7 | 7 | . | 7 |

基础冒泡排序会使用四次遍历来对一个五个元素的数组进行排序，无论是否需要所有传递。优化的冒泡排序会检查是否还需要更多传递。

基础冒泡排序和优化冒泡排序的伪代码以及流程图都使用了所有传递，无论列表在某处是否已排序。在优化的冒泡排序中，每次传递结束时都会执行一个条件测试，以查看是否发生了交换。如果最近一次传递期间没有发生交换，则列表已经处于排序状态，排序完成。这是对基础冒泡排序的微调。冒泡排序的流程图如图7.2 所示。

如果原始列表按照最糟糕的顺序排列，那么排序包含 $n$ 个元素的列表需要 $(n - 1)$ 次传递。普通冒泡排序的每次传递都涉及 $n - 1$ 次值比较。这总共有 $(n - 1) \cdot (n - 1) = n^2 - 2n + 1$ 次比较。如果经过优化，那么第一次传递有 $n - 1$ 次比较，第二次传递有 $n - 2$ 次比较，第三次传递有 $n - 3$ 次比较，总计为 $(n - 1) + (n - 2) + (n - 3) + \dots + 2 + 1 = n(n - 1)/2 \approx$ 次比较。无论冒泡排序是否经过优化，比较次数都与 $n^2$ 大正比。冒泡排序被认为阶阶为 $n^2$。

#### 伪代码

```
funcbubblesort:
  for each index i from 1 to n
    for each index j from n-1 to i
      if a[j] > a[j-1]
        temp <- a[j]
        a[j] <- a[j-1]
        a[j-1] <- temp
      end if
    end for
end for
```

# 442 一维数组

![](img/8356e6c3bfe3b10354682c60b1e74b1d_461_0.png)

图7.2 冒泡排序流程图

# 7.6 示例程序 443

### 程序

```c
/*********************************************************************/
/* main: 冒泡排序 */
/* 将一组数字按升序排列 */
/*********************************************************************/
/* 定义的常量: */
/* ARSIZE - 数组最大尺寸 */
/* 输入变量: */
/* array[ARSIZE] - 要排序的数值数组 */
/* 输出变量: */
/* array[ARSIZE] - 排序后的数值数组 */
/* 调用的函数: */
/* funcbubble: 降序冒泡排序 */
/*********************************************************************/
#include <stdio.h>
#define ARSIZE 10
void funcbubble(float array[], int n);
int main() {
    float array[ARSIZE];
    int i;
    printf("Enter ten values to be sorted:\n");
    for(i = 0; i < ARSIZE; i++)
        scanf("%f", &array[i]);
    funcbubble(array, ARSIZE);
    printf("\nSorted Array:\n");
    for(i = 0; i < ARSIZE; i++)
        printf("%.2f ", array[i]);
    printf("\n");
    return 0;
}
```

# 444 一维数组

```c
****************************************************
/*
 * funcbubble: 冒泡排序
 */
****************************************************
/* 局部变量: */
 *   temp            - 存储数组元素
/* 输入/输出参数: */
 *   array[n]        - 数组
 *   n               - 数组尺寸 */
************************************
void funcbubble(float array[], int n) {
    float temp;
    int i, j;
    for (i = 1; i < n; i++) {
        for(j = n - 1; j >= i; j--) {
            if(array[j] > array[j-1]) {
                temp = array[j];
                array[j] = array[j-1];
                array[j-1] = temp;
            }
        }
    }
    return;
}
```

输入和输出
====================
Enter ten values to be sorted:
12.0 56.0 76.0 98.0 34.5 65.3 76.2 81.5 95.7 86.9
Sorted Array:
98.00 95.70 86.90 81.50 76.20 76.00 65.30 56.00 34.50 12.00

# 优化的冒泡排序

#### 伪代码

```
Function funcbubble(optimized bubble sort)
set flag to false
i <- 1
while(i <= n and not flag)
  set flag to true
  for each element j from n-1 to i
    if array[j] > array[j-1]
      temp <- array[j]
      array[j] <- array[j-1]
      array[j-1] <- temp
      flag <- false
  end for
  i <- i + 1
end while
return
```

优化的冒泡排序流程图如图7.3。

### 程序

```c
*********************************************************************/
/*  main: 优化的冒泡排序 */
/*  将一组数字按升序排列 */
/*********************************************************************/
/*  定义的常量: */
/*  ARSIZE - 数组最大尺寸 */
/*  输入变量: */
/*  array[ARSIZE] - 要排序的数值数组 */
/*  输出变量: */
/*  array[ARSIZE] - 排序后的数值数组 */
/*  调用的函数: */
/*  funcoptbubble: 降序冒泡排序 */
/*
```

# 446 一维数组

![](img/8356e6c3bfe3b10354682c60b1e74b1d_465_0.png)

图7.3 优化的冒泡排序流程图

```c
*********************************************************************/
#include <stdio.h>
#define ARSIZE 5
void funcoptbubble(float array[], int n);
int main() {
    float array[ARSIZE];
    int i;
    printf("Enter five values to be sorted:\n");
    for(i = 0; i < ARSIZE; i++)
        scanf("%f", &array[i]);

    funcoptbubble(array, ARSIZE);
    printf("Sorted array:\n");
    for(i = 0; i < ARSIZE; i++)
        printf("%.2f ", array[i]);

    return 0;
}
```

```c
*********************************************************************/
/*
/* funcoptbubble: 优化的冒泡排序
/*
*************************************************/
```

```c
*********************************************************************/
/* 输入/输出参数:
/* array[n] - 数组
/* n       - 数组尺寸 */
/*************************************************/
```

```c
void funcoptbubble(float array[], int n) {
    int i = 1, j, flag = 0;
    float temp;

    while(!flag && i <= n) {
        flag = 1;      /* *假设已排序 */
        for(j = n - 1; j >= i; j--) {
            if(array[j] > array[j - 1]) {
                temp = array[j];
                array[j] = array[j - 1];
                array[j - 1] = temp;
                flag = 0;      /* *表示尚未排序 */
            }
        }
        i++;
    }
    return;
}
```

### 输入和输出

Enter five values to be sorted:
34.5 12.5 67.3 89.4 19.4

Sorted array:
89.40 67.30 34.50 19.40 12.50

# 7.6.6 搜索

当需要从列表中查找值以访问关联数据时，搜索方法取决于所搜索的列表是有序还是未排序的。如果列表未排序，则必须使用线性搜索。如果列表是有序的，可以使用线性搜索或二分搜索来查找特定值。二分搜索比线性搜索快得多。

线性搜索 线性搜索是顺序搜索，直到找到所需的值。如果该值是数组中的第一个元素，只需要一次比较；如果该值是数组中的第十个元素，则需要十次比较；如果该值是数组中的最后一个元素，则需要比较数组的所有元素。如果该值不在数组中，则必须搜索整个数组。线性搜索算法返回找到值的位置，如果未找到则返回 -1。

#### 伪代码

```
main:
输入数组
输入要查找的元素
调用函数 search
输出搜索结果
停止
```

```
functionsearch:
  i← 0
set location to -1
while i < n and location < 0
```

