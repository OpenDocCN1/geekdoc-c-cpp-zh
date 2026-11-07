

要确定顺序搜索算法在成功情况下的平均比较次数：

- 1. 考虑所有可能的情况。
- 2. 找出每种情况下的比较次数。
- 3. 将比较次数相加，再除以情况总数。

如果搜索项（称为**目标项**）是列表中的第一个元素，则需要进行一次比较。如果目标项是列表中的第二个元素，则需要进行两次比较。类似地，如果目标项是列表中的第 *k* 个元素，则需要进行 *k* 次比较。我们假设目标项可以是列表中的任意元素；也就是说，列表中的所有元素成为目标项的可能性相同。假设列表中有 *n* 个元素。下面的表达式给出了平均比较次数：

$$\frac{1+2+\cdots+n}{n}$$

已知：

$$1+2+\cdots+n=\frac{n(n+1)}{2}.$$

因此，下面的表达式给出了顺序搜索在成功情况下所进行的平均比较次数：

$$\frac{1+2+\cdots+n}{n}=\frac{1}{n}\frac{n(n+1)}{2}=\frac{n+1}{2}.$$

该表达式表明，平均而言，成功的顺序搜索会搜索列表的一半。因此，如果列表大小为 1,000,000，则顺序搜索平均需要进行 500,000 次比较。由此可见，顺序搜索对于大型列表来说效率不高。

## 二分搜索

如你所见，顺序搜索对于大型列表来说效率不高，因为平均要搜索列表的一半。因此，我们介绍另一种称为**二分搜索**的搜索算法，它的速度非常快。但是，二分搜索只能在已排序的列表上执行。因此，我们假设列表已经排序。在本章后面，我们将介绍几种排序算法。

二分搜索算法使用“分而治之”技术来搜索列表。首先，将搜索项与列表的中间元素进行比较。如果搜索项小于列表的中间元素，则将搜索范围限制在列表的前半部分；否则，搜索列表的后半部分。

考虑图 18-1 中长度为 *12* 的已排序列表。

![](img/b217c421655b51e7494cf3b89bb5432d_1333_0.png)

**图 18-1** 长度为 12 的列表

假设我们想确定列表中是否包含 75。最初，整个列表都是搜索列表（见图 18-2）。

![](img/b217c421655b51e7494cf3b89bb5432d_1333_1.png)

**图 18-2** 搜索列表，list[0] . . . list[11]

首先，我们将 75 与该列表的中间元素 list[5]（即 39）进行比较。由于 75 ≠ list[5] 且 75 > list[5]，因此我们将搜索范围限制为列表 list[6] . . . list[11]，如图 18-3 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1333_2.png)

**图 18-3** 搜索列表，list[6] . . . list[11]

现在，在列表 list[6] . . . list[11] 上重复此过程，该列表的长度为 *6*。

由于我们需要频繁确定列表的中间元素，因此二分搜索算法通常针对基于数组的列表来实现。要确定列表的中间元素，我们将搜索列表的起始索引 first 和结束索引 last 相加，然后除以 2 来计算中间元素的索引。也就是说，

mid = (first + last) / 2。

### 示例 18-1

考虑图 18-4 中给出的列表。

![](img/b217c421655b51e7494cf3b89bb5432d_1335_0.png)

该列表的大小为 12，也就是说，长度为 12。假设我们正在搜索项 89。表 18-1 显示了每次循环执行过程中 `first`、`last` 和 `mid` 的值。表中还显示了每次循环执行过程中，该项与列表元素进行比较的次数。

**表 18-1** 搜索项 89 时 `first`、`last` 和 `mid` 的值及比较次数

| 迭代次数 | `first` | `last` | `mid` | `list[mid]` | 比较次数 |
|---|---|---|---|---|---|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 6 | 11 | 8 | 66 | 2 |
| 3 | 9 | 11 | 10 | 89 | 1（`found` 为 `true`） |

该项在位置 10 处找到，总比较次数为 5。

接下来，我们搜索列表中的项 34。表 18-2 显示了每次循环执行过程中 `first`、`last` 和 `mid` 的值。表中还显示了每次循环执行过程中，该项与列表元素进行比较的次数。

**表 18-2** 搜索项 34 时 `first`、`last` 和 `mid` 的值及比较次数

| 迭代次数 | `first` | `last` | `mid` | `list[mid]` | 比较次数 |
|---|---|---|---|---|---|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 4 | 4 | 4 | 34 | 1（`found` 为 `true`） |

该项在**位置 4** 处找到，总比较次数为 7。

现在，让我们搜索项 22，如表 18-3 所示。

**表 18-3** 搜索项 22 时 `first`、`last` 和 `mid` 的值及比较次数

| 迭代次数 | `first` | `last` | `mid` | `list[mid]` | 比较次数 |
|---|---|---|---|---|---|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 3 | 2 |  | 循环停止（因为 `first > last`） |  |

这是一次不成功的搜索。总比较次数为 6。

示例 18-2 说明了如何在程序中使用二分搜索算法。

### 示例 18-2

```cpp
#include <iostream>                         //Line 1
#include "searchSortAlgorithms.h"            //Line 2

using namespace std;                          //Line 3

int main()                                      //Line 4
{
    int intList[] = {2, 16, 34, 45, 53,       //Line 5
                     56, 69, 70, 75, 96};     //Line 6

    int pos;                                    //Line 7

    pos = binarySearch(intList, 10, 45);       //Line 8

    if (pos != -1)                              //Line 9
        cout << "Line 10: " << 45 << " found"
             << " at position " << pos << endl; //Line 10
    else                                        //Line 11
        cout << "Line 12: " << 45
             << " is not in intList " << endl; //Line 12

    return 0;                                   //Line 13
}                                               //Line 14
```

## 二分搜索算法与 `class orderedArrayListType`

第 13 章中设计的 `class orderedArrayListType` 不包含二分搜索算法。现在，既然你已经了解如何实现二分搜索算法，就可以学习如何在 `class orderedArrayListType` 中使用它。

要在 `class orderedArrayListType` 中使用二分搜索算法，我们向该类添加函数 `binSearch`，并使用适当的参数调用函数 `binarySearch`。

```cpp
#include "arrayListType.h"
#include "searchSortAlgorithms.h"

template <class elemType>
class orderedArrayListType: public arrayListType<elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    void seqSearch(const elemType& searchItem) const;
    void insert(const elemType& insertItem);
    void remove(const elemType& removeItem);

    int binSearch(const elemType& searchItem);

    orderedArrayListType(int size = 100);
        //Constructor
};
```

成员函数 `binSearch` 的定义如下：

```cpp
template <class elemType>
int orderedArrayListType<elemType>::
                         binSearch(const elemType& item) const
{
    return binarySearch(list, length, item);
}
```

## 渐近记号：大 O 记号

正如在编写算法和计算机程序之前需要对问题进行分析一样，算法设计完成后，也应该对其进行分析。通常，设计某一特定算法的方法有多种。有些算法执行时占用的计算机时间非常少，而另一些算法则需要相当长的时间。请考虑下面的示例。

