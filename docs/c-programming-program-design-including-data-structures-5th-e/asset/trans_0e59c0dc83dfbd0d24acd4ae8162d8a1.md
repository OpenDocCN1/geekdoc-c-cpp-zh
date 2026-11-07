
假设 `list[0...n - 1]` 是一个包含 n 个元素的列表，索引从 0 到 n - 1。我们希望重新排列，即按升序对 `list` 的元素进行排序。冒泡排序算法的工作方式如下。

在一系列 n - 1 次迭代中，依次比较列表中相邻的元素 `list[index]` 和 `list[index + 1]`。如果 `list[index]` 大于 `list[index + 1]`，则交换元素 `list[index]` 和 `list[index + 1]`。

由此可知，较小的元素向顶部移动，较大的元素向底部移动。

在第一次迭代中，我们考虑 `list[0...n - 1]`。正如你将看到的，第一次迭代后，列表中的最大元素被移动到列表的最后位置，即位置 n - 1。在第二次迭代中，我们考虑 `list[0...n - 2]`。第二次迭代后，列表中第二大的元素被移动到位置 n - 2，即列表的倒数第二个位置。在第三次迭代中，我们考虑 `list[0...n - 3]`，依此类推。正如你将看到的，每次迭代后，列表中未排序部分的大小都会缩小。

考虑包含五个元素的 `list[0...4]`，如图 19-6 所示。

![](img/f97f778697507bb6fdd80c5991210cba_1244_0.png)

**图 19-6** 五个元素的列表

### 第 1 次迭代：排序 `list[0...4]`

图 19-7 展示了第一次迭代中 `list` 的元素如何重新排列。

![](img/f97f778697507bb6fdd80c5991210cba_1244_1.png)

**图 19-7** 第一次迭代期间 `list` 的元素

注意，在图 19-7 的第一个示意图中，`list[0] > list[1]`。因此，交换 `list[0]` 和 `list[1]`。在第二个示意图中，比较 `list[1]` 和 `list[2]`。因为 `list[1] < list[2]`，所以它们不被交换。图 19-7 的第三个示意图比较 `list[2]` 与 `list[3]`；因为 `list[2] > list[3]`，所以交换 `list[2]` 与 `list[3]`。然后，在第四个示意图中，我们比较 `list[3]` 与 `list[4]`。因为 `list[3] > list[4]`，所以交换 `list[3]` 和 `list[4]`。

第一次迭代后，最大元素位于最后位置。因此，在下一次迭代中，我们考虑 `list[0...3]`。

### 第 2 次迭代：排序 `list[0...3]`

图 19-8 展示了第二次迭代中 `list` 的元素如何重新排列。

![](img/f97f778697507bb6fdd80c5991210cba_1245_0.png)

**图 19-8** 第二次迭代期间 `list` 的元素

元素像第一次迭代中那样进行比较和交换。这里只考虑列表元素 `list[0]` 到 `list[3]`。第二次迭代后，最后两个元素已位于正确位置。因此，在下一次迭代中，我们考虑 `list[0...2]`。

### 第 3 次迭代：排序 `list[0...2]`

图 19-9 展示了第三次迭代中 `list` 的元素如何重新排列。

![](img/f97f778697507bb6fdd80c5991210cba_1245_1.png)

**图 19-9** 第三次迭代期间 `list` 的元素

第三次迭代后，最后三个元素已位于正确位置。因此，在下一次迭代中，我们考虑 `list[0...1]`。

### 第 4 次迭代：排序 `list[0...1]`

图 19-10 展示了第四次迭代中 `list` 的元素如何重新排列。

![](img/f97f778697507bb6fdd80c5991210cba_1246_0.png)

**图 19-10** 第四次迭代期间 `list` 的元素

第四次迭代后，`list` 已排序。

以下 C++ 函数实现了冒泡排序算法。

```cpp
template <class elemType>
void bubbleSort(elemType list[], int length)
{
    for (int iteration = 1; iteration < length; iteration++)
    {
        for (int index = 0; index < length - iteration;
             index++)
        {
            if (list[index] > list[index + 1])
            {
                elemType temp = list[index];
                list[index] = list[index + 1];
                list[index + 1] = temp;
            }
        }
    }
} //end bubbleSort
```

示例 19-11 说明了如何在程序中使用冒泡排序算法。

### 示例 19-11（冒泡排序）

```cpp
#include <iostream>
#include "searchSortAlgorithms.h"

using namespace std;

template <class elemType>
void print(elemType list[], int length);

int main()
{
    int intList[] = {2, 56, 34, 25, 73,
                     46, 89, 10, 5, 16};                 //Line 1

    cout << "Line 2: Before sorting, intList: ";        //Line 2

    print(intList, 10);                                  //Line 3

    cout << endl;                                         //Line 4

    bubbleSort(intList, 10);                              //Line 5

    cout << "Line 6: After sorting, intList: ";         //Line 6

    print(intList, 10);                                   //Line 7

    return 0;
}

template <class elemType>
void print(elemType list[], int length)
{
    for (int i = 0; i < length; i++)
        cout << list[i] << " ";

    cout << endl;
}
```

### 示例运行结果：

```
Line 2: Before sorting, intList: 2 56 34 25 73 46 89 10 5 16

Line 6: After sorting, intList: 2 5 10 16 25 34 46 56 73 89
```

第 1 行的语句声明并初始化 `intList` 为一个包含 10 个 int 类型分量的数组。第 3 行的语句在对数组 `intList` 排序之前输出其值。第 5 行的语句使用函数 `bubbleSort` 对列表进行排序。注意，`intList` 及其长度（元素个数）都作为参数传递给函数 `bubbleSort`。第 7 行的语句输出排序后的 `intList`。

## 分析：冒泡排序

对于搜索算法，我们只关心关键字（项）比较的次数。排序算法既要进行关键字比较，也要移动数据。因此，在分析排序算法时，我们既关注关键字比较的次数，也关注数据移动的次数。

假设一个长度为 $n$ 的列表 $L$ 要用冒泡排序进行排序。考虑本章给出的函数 `bubbleSort`。该函数包含嵌套的 `for` 循环。因为 $L$ 的长度为 $n$，所以外层循环执行 $n-1$ 次。对于外层循环的每次迭代，内层循环执行一定次数。让我们考虑外层循环的第一次迭代。在外层循环的第一次迭代期间，内层循环的迭代次数为 $n-1$。因此有 $n-1$ 次比较。类似地，在外层循环的第二次迭代期间，内层循环的迭代次数为 $n-2$，依此类推。因此，比较的总次数为：

$$(n-1)+(n-2)+\cdots+2+1=\frac{n(n-1)}{2}=\frac{1}{2}n^2-\frac{1}{2}n=O(n^2).$$

在最坏情况下，`if` 语句的主体总是执行。因此，在最坏情况下，赋值次数为：

$$\frac{3n(n-1)}{2}=\frac{3}{2}n^2-\frac{3}{2}n=O(n^2).$$

如果列表已经有序，即最好情况，则赋值次数为 0。可以证明，平均而言，冒泡排序大约进行 $\frac{n(n-1)}{4}$ 次项赋值。然而，如本章所述，冒泡排序的比较次数始终为 $\frac{n(n-1)}{2}$。因此，要对大小为 1000 的列表进行排序，冒泡排序大约进行 500,000 次关键字比较和约 250,000 次项赋值。下一节将介绍选择排序算法，它可以减少项赋值的次数。

> **注意** 本章末尾的练习 7 给出了冒泡排序算法的一个版本，在最好情况下比较次数为 $O(n)$。

## 冒泡排序算法与类 `unorderedArrayListType`

第 14 章设计的 `class unorderedArrayListType` 不包含任何排序算法。既然你已经知道如何实现冒泡排序算法，就可以学习如何在 `class unorderedArrayListType` 中使用它。

为了在 `class unorderedArrayListType` 中使用二分搜索算法，我们将函数 `sort` 添加到该类中，并用适当的参数调用函数 `bubbleSort`。（注意，我们还添加了使用二分搜索算法的函数。）

```cpp
template <class elemType>
class unorderedArrayListType: public arrayListType<elemType>
```
