
原则上，索引表可以基于任何排序算法构建。由于其概念直接、通用性强、并且稳定，我们基于插入排序实现了两种索引算法（参见第 4.3 节）。清单 4.5 中给出的例程 `Index` 代表了其单键实现。我们实现中的第一步是通过索引 `i` 本身初始化索引数组的组件 `ind[i]`，就像已排序的序列一样。例程然后执行一个通用的插入排序，但是，任何涉及分量 `x[i]` 的操作都被替换为对索引数组 `ind[i]` 的对应分量的操作。对已排序分量的具体引用是通过索引数组间接引用完成的，`x[ind[i]]`。这种

### 清单 4.4 基于 Quicksort 的排序（Python 编码）

```
#================================================================================
def QuickSort(x, l, n):
#--------------------------------------------------------------------------------
# Ascending sort of array x[l..n] by Quicksort
#--------------------------------------------------------------------------------
    if (l >= n): return                         # pivot = x[n]; create "<" and ">=" lists
    m = l                                       # upper index in "<"-list
    for i in range(l,n):                        # scan entire list, excepting pivot
        if (x[i] < x[n]):                       # compare current value with pivot
            t = x[i]; x[i] = x[m]; x[m] = t     # swap < value to end of "<"-list
            m += 1                              # extend "<"-list: increase upper index
    t = x[m]; x[m] = x[n]; x[n] = t              # swap pivot between "<" and ">=" lists
    QuickSort(x,l,m-1)                          # sort "<"-list
    QuickSort(x,m+1,n)                          # sort ">="-list
```

间接引用在枢轴 `x[ipiv]` 的情况下是不必要的，因为 `ind[ipiv]` 仍然包含初始值 `ipiv`，并且在之前的步骤中，只有分量 `ind[i]` 与 `i<ipiv` 被修改。

在许多应用中，构建元素相对于排序标准的秩的数组可能很有用。秩简单地表示元素在排序序列中将拥有的序号。对于长度为 `n` 的序列，秩为 1 到 `n` 的整数：秩 1 对应最小元素，而秩 `n` 对应最大元素。秩数组可以很容易地从现有的索引数组获得。具体来说，例程 `Rank`（清单 4.6）将秩 `i` 分配给具有索引 `ind[i]` 的元素。

### 清单 4.5 基于直接插入的索引（Python 编码）

```
#================================================================================
def Index(x, ind, n):
#--------------------------------------------------------------------------------
# Ascending indexing of array x[1..n] in ind[] by insertion sort
#--------------------------------------------------------------------------------
    for i in range(1,n+1): ind[i] = i                # initialize index array
    for ipiv in range(2,n+1):                       # loop over pivots
        xpiv = x[ipiv]                              # save pivot to free its location
        i = ipiv - 1                                # initialize sublist counter
        while ((i > 0) and (x[ind[i]] > xpiv)):     # scan to the left of pivot
            ind[i+1] = ind[i]                       # item > pivot: shift to the right
            i -= 1
        ind[i+1] = ipiv                             # insert pivot into last freed location
```

### 清单 4.6 基于索引数组的排名（Python 编码）

```
#===============================================================================
def Rank(ind, rnk, n):
#-------------------------------------------------------------------------------
# Returns the ranks rnk[1..n] for a list indexed in ind[1..n]
#-------------------------------------------------------------------------------
    for i in range(1,n+1): rnk[ind[i]] = i
```

### 清单 4.7 排序和索引的简单应用（Python 编码）

```
# Ascending sort and indexing of an array
from sort import *

#### main

n = 6                                         # number of values to be sorted
x = [0., 30., 60., 50., 20., 10., 40.]        # array to be sorted
ind = [0]*(n+1); rnk = [0]*(n+1)               # arrays of indexes and ranks

print("Original array:")
for i in range(1,n+1): print("{0:6.2f}".format(x[i]),end="")
print()

Index(x,ind,n)
print("Indexes:")
for i in range(1,n+1): print("{0:6d}".format(ind[i]),end="")
print()

Rank(ind,rnk,n)
print("Ranks:")
for i in range(1,n+1): print("{0:6d}".format(rnk[i]),end="")
print()

print("Indexed array:")
for i in range(1,n+1): print("{0:6.2f}".format(x[ind[i]]),end="")
print()

InsertSort(x,n)
print("Sorted array:")
for i in range(1,n+1): print("{0:6.2f}".format(x[i]),end="")
print()
```

### 清单 4.8 基于直接插入的双键索引例程（Python 编码）

```
# =================================================================================
def Index2(x, y, ind, n):
# --------------------------------------------------------------------------------
#  Ascending indexing of correlated arrays x[1..n] and y[1..n] in ind[] by
#  insertion sort using x[] as primary key and y[] as secondary key
# --------------------------------------------------------------------------------
    for i in range(1,n+1): ind[i] = i                 # initialize index array

    for ipiv in range(2,n+1):                         # loop over pivots
        xpiv = x[ipiv]; ypiv = y[ipiv]
        i = ipiv - 1                                  # initialize sublist counter
        while ((i > 0) and                              # scan to the left of pivot
               (x[ind[i]] > xpiv or (x[ind[i]] == xpiv and y[ind[i]] > ypiv))):
            ind[i+1] = ind[i]                         # item > pivot: shift to the right
            i -= 1

        ind[i+1] = ipiv                               # insert pivot into last freed location
```

### 清单 4.9 两个相关数组的索引（Python 编码）

```
# Ascending indexing of two correlated arrays
from sort import *

#### main

n = 6                                                   # number of values to be sorted
x = [0., 40., 60., 40., 20., 60., 20.]                  # primary array
y = [0., 2., 2., 1., 2., 1., 1.]                        # secondary array
ind = [0]*(n+1)                                         # array of indexes

print("Original arrays:")
print("x",end="")
for i in range(1,n+1): print("{0:6.2f}".format(x[i]),end="")
print()
print("y",end="")
for i in range(1,n+1): print("{0:6.2f}".format(y[i]),end="")
print()

Index2(x,y,ind,n)
print("Indexes:")
for i in range(1,n+1): print("{0:6d}".format(ind[i]),end="")
print()

print("Indexed arrays:")
print("x",end="")
for i in range(1,n+1): print("{0:6.2f}".format(x[ind[i]]),end="")
print()
print("y",end="")
for i in range(1,n+1): print("{0:6.2f}".format(y[ind[i]]),end="")
print()
```

基于本章介绍的技术，可以通过实际排序，例如使用例程 `InsertSort`，或通过使用例程 `Index` 对序列进行索引并间接引用分量，来按升序处理数组 `x[]` 的分量。

## Listing 4.10 Output of Program 4.9.

```
Original arrays:
x 40.00 60.00 40.00 20.00 60.00 20.00
y 2.00 2.00 1.00 2.00 1.00 1.00
Indexes:
6 4 3 1 5 2
Indexed arrays:
x 20.00 20.00 40.00 40.00 60.00 60.00
y 1.00 2.00 1.00 2.00 1.00 2.00
```

使用创建的索引数组 `ind[]`，即 `x[ind[i]]`。Program 4.7 举例说明了这两种选项。然而，由于例程 `InsertSort` 会不可逆地重新排序序列 `x[]`，程序实际上首先通过调用例程 `Index` 和 `Rank` 对原始序列进行索引和排序。

让我们最后处理两个相关数组 `x[]` 和 `y[]` 的同时索引问题，其中 `y[]` 在层级上从属于 `x[]`。在这种情况下，`x[]` 和 `y[]` 的对应分量的值分别充当主键和次要键。Listing 4.8 中提供的例程 `Index2` 代表了单键例程 `Index` 的直接推广。主要区别在于，移动不仅针对大于当前主键枢轴 `xpiv` 的主键数组 `x[]` 的分量，还针对主键值相等且次要数组 `y[]` 的分量大于次要枢轴 `ypiv` 的情况。

例程 `Index2` 的使用在 Program 4.9 中进行了说明，结果输出显示在 Listing 4.10 中。除了 `Index2` 为两个数组 `x[]` 和 `y[]` 返回的索引表 `ind[]` 外，该程序还列出了实际排序后的值 `x[ind[i]]` 和 `y[ind[i]]`。

## 4.6 Implementations in C/C++

Listing 4.11 显示了文件 `sort.h` 的内容，其中包含与正文中开发的 Python 函数等价的 C/C++ 实现，并包含在模块 `sort.py` 中。相应的例程具有相同的名称、参数和功能。

## Listing 4.11 Sorting, Indexing, and Ranking Routines (sort.h)

```
//------------------------------------------- sort.h -------------------------------------------
// Contains routines for sorting, indexing and ranking numeric sequences.
// Part of the numxlib numerics library. Author: Titus Beu, 2013
//-----------------------------------------------------------------------------------------------
#ifndef _SORT_
#define _SORT_

//================================================================================================
void BubbleSort0(double x[], int n)
//-----------------------------------------------------------------------------------------------
// Ascending sort of array x[1..n] by bubble sort
//-----------------------------------------------------------------------------------------------
{
    double xi;
    int i, ipass;

    for (ipass=1; ipass<=(n-1); ipass++)                 // loop of passes
        for (i=1; i<=n-ipass; i++)                      // loop over unsorted sublists
            if (x[i] > x[i+1])                          // compare neighbors
                { xi = x[i]; x[i] = x[i+1]; x[i+1] = xi; }  // swap neighbors
}
```
