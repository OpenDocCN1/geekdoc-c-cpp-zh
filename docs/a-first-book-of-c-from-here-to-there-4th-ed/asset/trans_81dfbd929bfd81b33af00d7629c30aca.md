
直接访问的是原始数组，而不是数组元素的副本。在被调函数中必须声明一个形参来接收所传入的数组名。对于一维和二维数组，该形参的声明都可以省略数组的行大小。

## 7.7 本章补充：搜索与排序方法

大多数程序员在编程生涯中都会遇到需要对数据项列表进行排序和搜索的情况。例如，你可能需要将实验结果按递增（升序）或递减（降序）顺序排列以进行统计分析，或者将姓名列表按字母顺序排序并搜索该列表以找到某个特定姓名。类似地，你可能需要将日期列表按升序或降序排列，并搜索该列表以定位某个特定日期。本节介绍排序和搜索列表的基本原理。请注意，在搜索之前对列表进行排序并非必需，尽管如果列表有序，搜索速度会快得多，这一点你很快就会看到。

## 搜索算法

许多程序的一个常见需求是在列表中搜索给定元素。例如，在姓名和电话号码列表中，你可能要搜索某个特定姓名以便打印对应的电话号码，或者你可能只需要搜索列表以确定某个姓名是否存在。执行这些搜索最常见的两种方法是线性搜索算法和二分搜索算法。

## 线性搜索

线性搜索，也称为顺序搜索，按列表中每一项出现的顺序依次检查，直到找到所需项或到达列表末尾。这种搜索方法类似于在电话簿中逐个查看每个姓名，从 Aardvark、Aaron 开始，直到找到你想要的姓名或到达 Zzxgy、Zora。显然，这不是搜索长字母顺序列表的最有效方法。然而，线性搜索有以下优点：

- 算法简单。
- 列表不必按任何特定顺序排列。

在线性搜索中，搜索从列表的第一项开始，逐项顺序继续，直到遍历整个列表。执行线性搜索的函数的伪代码如下：

```
For all items in the list
  Compare the item with the desired item
  If the item is found
    Return the index value of the current item
  Endif
EndFor
Return -1 if the item is not found
```

请注意，函数的返回值指示是否找到了该项。如果返回值为 -1，则该项不在列表中；否则，for 循环中的返回值提供了该项在列表中的索引位置。`linearSearch()` 函数以 C++ 函数的形式说明了这一过程：

```
// this function returns the location of key in the list
// a -1 is returned if the value is not found
int linearSearch(int list[], int size, int key)
{
    int i;

    for (i = 0; i < size; i++)
    {
        if (list[i] == key)
            return i;
    }

    return -1;
}
```

在检查 `linearSearch()` 时，请注意 for 循环仅用于访问列表中的每个元素，从第一个到最后一个，直到找到与所需项匹配的元素。如果找到该项，则返回当前元素的索引值，这将导致循环终止；否则，搜索将继续，直到到达列表末尾。

为了测试该函数，编写了一个 `main()` 驱动函数来调用 `linearSearch()` 并显示其返回的结果。程序 7.9 显示了完整的测试程序。

![](img/e9bf940282dfb289356f077151cc69dd_345_0.png)

## 程序 7.9

```
#include <iostream>
using namespace std;

int linearSearch(int [], int, int); // function prototype

int main()
{
    const int NUMEL = 10;
    int nums[NUMEL] = {5,10,22,32,45,67,73,98,99,101};
    int item, location;

    cout << "Enter the item you are searching for: ";
    cin >> item;

    location = linearSearch(nums, NUMEL, item);
```

```
if (location > -1)
    cout << "The item was found at index location "
         << location << endl;
else
    cout << "The item was not found in the list\n";

return 0;
}
```

```
// this function returns the location of key in the list
// a -1 is returned if the value is not found
int linearSearch(int list[], int size, int key)
{
    int i;

    for (i = 0; i < size; i++)
    {
        if (list[i] == key)
            return i;
    }
    return -1;

}
```

以下是程序 7.9 的示例运行结果：

```
Enter the item you are searching for: 101
The item was found at index location 9
```

以及

```
Enter the item you are searching for: 65
The item was not found in the list
```

如前所述，线性搜索的一个优点是搜索时列表不必有序。另一个优点是，如果搜索项位于列表靠前的位置，则只需进行少量比较。当然，最坏情况发生在搜索项位于列表末尾时。然而，平均而言，假设该项在列表中出现的位置概率相等，所需的比较次数为 n/2，其中 n 是列表的大小。因此，对于包含 10 个元素的列表，线性搜索平均需要 5 次比较；对于包含 10,000 个元素的列表，平均需要 5000 次比较。接下来你将看到，使用二分搜索算法可以大幅减少这一数字。

## 二分搜索

在二分搜索中，列表必须有序。从有序列表开始，首先将所需项与列表中间的元素进行比较。（对于包含偶数个元素的列表，可以使用两个中间元素中的任意一个。）比较后存在三种可能：所需项可能等于中间元素、大于中间元素或小于中间元素。

在第一种情况下，搜索成功，不需要进一步搜索。在第二种情况下，由于所需项大于中间元素，如果它确实存在，则必须在列表的后半部分。这意味着列表的前半部分（从第一个元素到中间点的所有元素）可以在后续搜索中丢弃。在第三种情况下，由于所需项小于中间元素，如果它确实存在，则必须在列表的前半部分。在这种情况下，列表的后半部分（包含从中间点到最后一个元素的所有元素）可以在后续搜索中丢弃。

该搜索策略的算法如图 7.11 所示，并由以下伪代码定义：

```
Set the left index to 0
Set the right index to 1 less than the size of the list
Begin with the first item in the list

While the left index is less than or equal to the right index
Set the midpoint index to the integer average of the left and right index values
Compare the desired item with the midpoint element
If the desired element equals the midpoint element
Return the index value of the current item
Else If the desired element is greater than the midpoint element
Set the left index value to the midpoint value plus 1
Else If the desired element is less than the midpoint element
Set the right index value to the midpoint value less 1
EndIf
EndWhile
Return -1 if the item is not found
```

## 第 7 章

本章补充：搜索与排序方法

![](img/e9bf940282dfb289356f077151cc69dd_348_0.png)

**图 7.11** 二分搜索算法

在图 7.11 的伪代码和流程图中，都使用 while 循环来控制搜索。初始列表通过将左索引值设置为 0、右索引值设置为列表中元素数目减 1 来定义。然后，将中间点索引取为左右索引值的整数平均值。

与中间点元素进行比较后，搜索随后被限制在更小的范围内：将左索引移动到中间点之上的一个整数值，或将右索引移动到中间点之下的一个整数值。此过程持续进行，直到找到该元素或左右索引值相等为止。`binarySearch()` 函数给出了该算法的 C++ 版本：

```
// this function returns the location of key in the list
// a -1 is returned if the value is not found
int binarySearch(int list[], int size, int key)
{
    int left, right, midpt;
    left = 0;
    right = size - 1;

    while (left <= right)
    {
        midpt = (int) ((left + right) / 2);
        if (key == list[midpt])
        {
            return midpt;
        }
        else if (key > list[midpt])
            left = midpt + 1;
        else
            right = midpt - 1;
    }

    return -1;
}
```

为测试该函数，使用了程序 7.10。程序 7.10 的一次示例运行结果如下：

```
Enter the item you are searching for: 101
The item was found at index location 9
```
