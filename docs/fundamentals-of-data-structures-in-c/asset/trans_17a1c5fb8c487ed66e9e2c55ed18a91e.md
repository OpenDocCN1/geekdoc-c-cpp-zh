

## 27. 什么是图的遍历？说明图的不同遍历方式。

图的遍历是指访问图中的所有节点。在许多实际应用中，遍历图非常重要，即通过最少的路径系统地访问每个顶点一次。图的两种重要遍历方法是

- 深度优先遍历（或）深度优先搜索（DFS）。
- 广度优先遍历（或）广度优先搜索（BFS）。

## 28. 确定下图所示无向图的关联矩阵。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_306_0.png)

上图所示无向图的关联矩阵如下，

| | E1 | E2 | E3 | E4 | E5 | E6 | E7 | E8 | E9 | E10 |
|---|---|---|---|---|---|---|---|---|---|---|
| A | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| B | 1 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| C | 0 | 1 | 1 | 0 | 0 | 0 | 1 | 0 | 1 | 0 |
| D | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 1 | 0 | 1 |
| E | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 |
| F | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 |

## 29. 确定下图所示有向图的关联矩阵。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_306_1.png)

上图所示有向图的关联矩阵如下，

| | E1 | E2 | E3 | E4 | E5 | E6 | E7 | E8 |
|---|---|---|---|---|---|---|---|---|
| A | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| B | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| C | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| D | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| E | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 |
| F | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 |

## 第 5 章

## 搜索和排序算法

### 5.1 引言

在本章中，我们将讨论编程中使用的两种最重要的技术：排序和搜索。**排序**一组或一序列的元素或数据项是指根据组中数据项之间的关系，将它们重新排列为升序或降序。**搜索**是一种编程技术，用于确定某个元素或数据项是否存在于列表中。

毫无疑问，排序是最基本的算法问题。许多不同的方法都能得出有用的排序算法，这些思想可用于解决许多其他问题。在计算机科学领域，寻找对给定数据集进行排序的更好算法是一个持续性的问题。简单的排序技术可以将数据按升序或降序排列。同一算法可用于递增或递减排序，我们只需根据需要在比较算法中将 $\le$ 改为 $\ge$ 即可。在本章中，我们将看到一些排序技术，且数据仅按升序排列。选择排序技术时需考虑的因素有，

- 排序技术的编程时间。
- 排序技术的执行时间。
- 对列表进行排序所需的比较次数。
- 排序技术所需的主存或辅助存储空间。

排序如此重要的一个原因是，一旦一组项目被排序，许多其他问题就会变得容易。加速搜索或许是排序最重要的应用。一旦元素在数组中按排序顺序排列，只需查看数组的第 k$^{th}$ 位置，即可在常数时间内找到第 k$^{th}$ 大的元素。

所有数据处理都需要高效、快速地访问记录。只有当数据项已根据某些指定键排序时，搜索技术才最高效。如果列表未排序，在列表较大时搜索记录会花费更多时间。因此，排序成为一种必要的技术。当排序方法具有最少的交换次数时，即如果算法进行过程中，两个值相等的数据项保证不会相互重新排列，则该排序方法被认为是稳定的。

一些重要的排序技术有

- 冒泡排序
- 插入排序
- 快速排序
- 归并排序。

一些重要的搜索技术有

- 线性搜索
- 二分搜索。

### 5.2 线性搜索

线性搜索（也称为顺序搜索）是最简单的搜索技术。搜索从列表的一端开始，逐个查找所需元素，直到找到该元素或到达列表末尾。如果找到搜索元素，则搜索成功；如果在列表中未找到搜索元素，则搜索不成功。线性搜索技术中，列表中的数据项不需要按顺序排列。

```
Algorithm for Linear Search
LINEAR_SEARCH (ARR, N, FIND)
where ARR is an array of N elements in which the element FIND is to be searched.
Step 1 : Repeat For I = 0, 1, 2, ..., N-1
Step 2 : If (ARR[I] = FIND) Then
    RETURN I
    [End of If structure]
Step 3 : [End of Step 1 For loop]
Step 4 : Return -1
END LINEAR_SEARCH()
```

### 程序 5.1：

```
/* Program to search an element using linear search. */
/* linear.c */
#include<stdio.h>
int linear_search(int [], int, int);
void main()
{
int i, n, pos, find, list[100];
printf("Enter the limit : ");
scanf("%d", &n);
printf("Enter the elements : ");
for(i = 0 ; i < n ; i++)
    scanf("%d", &list[i]);
printf("Enter the element to be searched : ");
scanf("%d", &find);
if((pos = linear_search(list, n, find)) == -1)
    printf("The element is not present");
else
    printf("The element is in the %d position", pos+1);
}
int linear_search(int list[], int n, int find)
{
    int i;
    for(i = 0 ; i < n ; i++)
    if(list[i] == find)
        return i;
    return -1;
}
```

**程序显示以下输出**
RUN1
Enter the limit : 5
Enter the elements : 78 88 89 98 65
Enter the element to be searched : 65
The element is in the 5 position
RUN2
Enter the limit : 5
Enter the elements : 90 8 3 2 1
Enter the element to be searched : 5
The element is not present

给定列表可以是任意顺序，要查找的元素出现在第一个位置或最后一个位置的可能性相同。最佳情况是 1，即当要搜索的元素出现在列表的第一个位置时发生。最坏情况是 n，即当要搜索的元素出现在列表的最后一个位置时发生。更坏的情况是 n+1，即当要搜索的元素不在列表中时发生。平均而言，线性搜索算法进行的比较次数是列表中元素数量的一半，公式为 (n+1) / 2。线性搜索方法对小型无序数组效果良好，但当列表大小较大时会变得低效。

### 5.3 二分搜索

*二分搜索算法*是最高效的搜索技术之一，它要求列表按升序排序。要在列表中*搜索元素*，二分搜索算法将列表分割并定位列表的中间元素。然后将其与搜索元素进行比较。如果搜索元素小于中间元素，则搜索列表的第一部分，否则搜索第二部分。算法再次将列表减为两半，定位中间元素，并与搜索元素比较。如果搜索列表小于中间元素，则搜索列表的第一部分。此过程持续进行，直到搜索元素等于中间元素，或列表仅包含一个不等于搜索元素的元素。

```
Algorithm for Binary Search
BINARY_SEARCH (ARR, FIND, BEG, END)
where ARR is an array in which the element FIND is to be searched, BEG refers
to the initial index position of the list, END refers to the final position of the list.
Step 1 : If (BEG > END) Then
    RETURN -1
    [End of If structure]
Step 2 : Assign MID = (BEG + END) / 2
Step 3 : If (FIND = ARR(MID)) Then
    RETURN MID
Else If (FIND < ARR(MID)) Then
    RETURN BINARY_SEARCH (ARR, FIND, BEG, MID-1)
Else
    RETURN BINARY_SEARCH (ARR, FIND, MID+1, END)
    [End of If structure]
END BINARY_SEARCH()
```

### 程序_5.2：

```
/* Program to search an element using binary search. */
/* binary.c * /
#include<stdio.h>
int binary_search(int [], int, int, int);
void main()
{
int i, n, find, pos = 0, list[100];
printf("Enter the limit : ");
scanf("%d", &n);
```

