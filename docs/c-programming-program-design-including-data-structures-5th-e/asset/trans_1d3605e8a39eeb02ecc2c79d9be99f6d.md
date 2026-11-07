
```cpp
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    int seqSearch(const elemType& searchItem) const;
    void remove(const elemType& removeItem);

    void sort();
    int binSearch(const elemType& item) const;

    unorderedArrayListType(int size = 100);
    //Constructor
};
```

成员函数 `binSearch` 和 `sort` 的定义如下：

```cpp
template <class elemType>
int unorderedArrayListType<elemType>::
                         binSearch(const elemType& item) const
{
    return binarySearch(list, length, item);
}

template <class elemType>
void unorderedArrayListType<elemType>::sort()
{
    selectionSort(list, length);
}
```

我们把它留作练习：编写一个程序来测试成员函数 `sort` 和 `binSearch`。

## 选择排序：基于数组的列表

选择排序算法通过选择列表中未排序部分的最小元素，然后将这个最小元素移到未排序列表的开头来对列表排序。第一次，我们在整个列表中定位最小项；第二次，我们从列表中的第二个元素开始定位列表中的最小项，依此类推。这里描述的选择排序算法是为基于数组的列表设计的。

假设你有图 19–11 所示的列表。

![](img/f97f778697507bb6fdd80c5991210cba_1249_0.png)

**图 19–11**  8 个元素的列表

图 19-12 显示了第一次迭代中 `list` 的元素。

![](img/f97f778697507bb6fdd80c5991210cba_1250_0.png)

**图 19–12** 第一次迭代期间 list 的元素

最初，整个列表是未排序的。因此我们找到列表中的最小项。最小项位于位置 6，如图 19-12(a) 所示。因为这是最小项，所以必须将它移到位置 0。于是我们将 16（即 `list[0]`）与 5（即 `list[6]`）交换，如图 19-12(b) 所示。交换这两个元素后，得到的列表如图 19-12(c) 所示。

图 19-13 显示了第二次迭代期间 `list` 的元素。

![](img/f97f778697507bb6fdd80c5991210cba_1250_1.png)

**图 19–13** 第二次迭代期间 list 的元素

现在未排序列表是 `list[1]...list[7]`。因此我们找到未排序列表中的最小元素。最小元素位于位置 3，如图 19-13(a) 所示。因为未排序列表中的最小元素位于位置 3，所以必须将它移到位置 1。于是我们将 7（即 `list[3]`）与 30（即 `list[1]`）交换，如图 19-13(b) 所示。将 `list[1]` 与 `list[3]` 交换后，得到的列表如图 19-13(c) 所示。

现在未排序列表是 `list[2]...list[7]`。因此我们重复前面的过程：找到列表中未排序部分最小元素的位置，并将其移到列表未排序部分的开头。因此，选择排序包括以下步骤：

- a. 找到最小元素的位置。
- b. 将最小元素移到未排序列表的开头。

最初，整个列表 `list[0]...list[length - 1]` 是未排序列表。执行步骤 a 和 b 一次后，未排序列表是 `list[1]...list[length - 1]`。第二次执行步骤 a 和 b 后，未排序列表是 `list[2]...list[length - 1]`，依此类推。我们可以借助 `for` 循环跟踪列表的未排序部分并重复步骤 a 和 b，如下所示：

```
for (int index = 0; index < length - 1; index++)
{
    a. Find the location, smallestIndex, of the smallest element in
       list[index]...list[length - 1].
    b. Swap the smallest element with list[index]. That is, swap
       list[smallestIndex] with list[index].
}
```

第一次循环时，我们在 `list[0]...list[length - 1]` 中定位最小元素，并将这个最小元素与 `list[0]` 交换。第二次循环时，我们在 `list[1]...list[length - 1]` 中定位最小元素，并将这个最小元素与 `list[1]` 交换，依此类推。此过程持续到未排序列表的长度为 1。（注意，长度为 1 的列表是已排序的。）因此，要实现选择排序算法，我们需要在循环内实现步骤 a 和 b。

给定列表的起始索引 `first` 和结束索引 `last`，以下 C++ 函数返回 `list[first]...list[last]` 中最小元素的索引。

```cpp
template <class elemType>
int minLocation(elemType list[], int first, int last)
{
    int loc, minIndex;

    minIndex = first;
    for (loc = first + 1; loc <= last; loc++)
        if (list[loc] < list[minIndex])
            minIndex = loc;

    return minIndex;
} //end minLocation
```

给定要交换元素在列表中的位置，以下 C++ 函数 `swap` 交换这些元素。

```cpp
template <class elemType>
void swap(elemType list[], int first, int second)
{
    elemType temp;

    temp = list[first];
    list[first] = list[second];
    list[second] = temp;
} //end swap
```

现在我们可以完成函数 `selectionSort` 的定义。

```cpp
template <class elemType>
void selectionSort(elemType list[], int length)
{
    int loc, minIndex;

    for (loc = 0; loc < length; loc++)
    {
        minIndex = minLocation(list, loc, length - 1);
        swap(list, loc, minIndex);
    }
} //end selectionSort
```

我们把它留作练习：编写一个程序来测试选择排序算法。  
（参见本章末尾的编程练习 6。）

> **注意**
>
> 1. 选择排序也可以通过选择列表中未排序部分的最大元素并将其移到列表末尾来实现。你可以通过修改函数 `minLocation` 中的 `if` 语句，并向相应函数和函数 `swap` 传递适当的参数（当这些函数在函数 `selectionSort` 中被调用时），轻松实现这种形式的选择排序。
>
> 2. 选择排序也可以应用于链表。一般算法相同，细节留作练习。参见本章末尾的编程练习 7。

## 分析：选择排序

假设要用选择排序算法对长度为 *n* 的列表 *L* 进行排序。函数 `swap` 执行三次元素赋值，并被执行 *n − 1* 次。因此，元素赋值的次数为 3(*n − 1*) = *O*(*n*)。

关键字比较由函数 `minLocation` 完成。对于长度为 *k* 的列表，函数 `minLocation` 进行 *k − 1* 次关键字比较。此外，函数 `minLocation` 被执行 *n − 1* 次（由函数 `selectionSort` 执行）。第一次，函数 `minLocation` 找到整个列表中最小关键字项的索引，因此进行 *n − 1* 次比较。第二次，函数 `minLocation` 找到长度为 $n-1$ 的子列表中最小元素的索引，因此进行 $n-2$ 次比较，依此类推。因此，关键字比较的次数如下：

$$(n-1)+(n-2)+\cdots+2+1=\frac{n(n-1)}{2}$$

$$=\frac{1}{2}n^2-\frac{1}{2}n$$

$$=\frac{1}{2}n^2+O(n)$$

$$=O(n^2).$$

由此可知，如果 $n=1000$，选择排序算法进行的关键字比较次数为：

$$\frac{1}{2}(1000)^2-\frac{1}{2}(1000)=499500\approx500000.$$

注意，选择排序算法不依赖于数据的初始排列。比较次数始终为 $O(n^2)$，赋值次数为 $O(n)$。一般来说，该算法仅适用于小列表，因为 $O(n^2)$ 随着 $n$ 的增长而快速增长。然而，如果数据移动代价高而比较次数代价不高，那么该算法可能比其他算法是更好的选择。

## 插入排序：基于数组的列表

上一节描述并分析了选择排序算法。已经表明，如果 $n=1000$，关键字比较次数约为 500,000，这相当高。本节描述称为**插入排序**的排序算法，它试图改善——也就是减少——关键字比较次数。

插入排序算法通过将每个元素移到列表中已排序部分的适当位置来对列表排序。考虑图 19-14 给出的列表。

![](img/f97f778697507bb6fdd80c5991210cba_1253_0.png)

**图 19–14**  列表

列表的长度为 8。在这个列表中，元素 `list[0]`、`list[1]`、`list[2]` 和 `list[3]` 是有序的。也就是说，`list[0]...list[3]` 是已排序的（见图 19-15）。
