
假设你想确定 27 是否在列表中。顺序查找的工作方式如下：首先，将 27 与 `list[0]` 比较，也就是将 27 与 35 比较。因为 `list[0] ≠ 27`，接着将 27 与 `list[1]` 比较，也就是与列表中的第二个项 12 比较。因为 `list[1] ≠ 27`，再将 27 与列表中的下一个元素比较，也就是将 27 与 `list[2]` 比较。因为 `list[2] = 27`，查找停止。这次查找成功。

现在让我们查找 10。和之前一样，查找从列表中的第一个元素开始，也就是从 `list[0]` 开始。按之前的方式继续进行，我们看到，这一次查找项 10 会与列表中的每一项进行比较。最终，列表中没有更多数据可与查找项比较。这是一次不成功的查找。

由此可知，一旦在列表中找到与查找项相等的元素，就必须停止查找并报告成功。（在这种情况下，通常还要报告在列表中查找到查找项的位置。）否则，在查找项与列表中的每个元素都比较过且未找到之后，必须停止查找并报告失败。

假设包含列表元素的数组名为 `list`。前面的讨论可转化为以下顺序查找算法：

```text
found is set to false
loc = 0;

while (loc < listLength and not found)
    if (list[loc] is equal to searchItem)
        found is set to true
    else
        increment loc

if (found)
    return loc;
else
    return -1;
```

下面的函数对一个列表执行顺序查找。具体来说，为了便于说明，我们假设列表元素类型为 `int`。

```cpp
int seqSearch(const int list[], int listLength, int searchItem)
{
    int loc;
    bool found = false;

    loc = 0;

    while (loc < listLength && !found)
        if (list[loc] == searchItem)
            found = true;
        else
            loc++;
```

如果函数 `seqSearch` 返回大于或等于 0 的值，则查找成功；否则，查找不成功。

从这段代码可以看出，查找开始时将 searchItem 与列表中的第一个元素比较。如果 searchItem 等于列表中的第一个元素，就退出循环；否则，loc 递增 1，指向列表中的下一个元素。然后将 searchItem 与列表中的下一个元素比较，依此类推。

## 示例 8-8

```cpp
// This program illustrates how to use a sequential search in a
// program.

#include <iostream>                              //Line 1

using namespace std;                             //Line 2

const int ARRAY_SIZE = 10;                       //Line 3

int seqSearch(const int list[], int listLength,
              int searchItem);                   //Line 4

int main()                                         //Line 5
{
    int intList[ARRAY_SIZE];                      //Line 7
    int number;                                   //Line 8

    cout << "Line 9: Enter " << ARRAY_SIZE
         << " integers." << endl;                //Line 9

    for (int index = 0; index < ARRAY_SIZE; index++) //Line 10
        cin >> intList[index];                    //Line 11

    cout << endl;                                 //Line 12

    cout << "Line 13: Enter the number to be "
         << "searched: ";                        //Line 13
    cin >> number;                                //Line 14
    cout << endl;                                 //Line 15

    int pos = seqSearch(intList, ARRAY_SIZE, number); //Line 16

    if (pos != -1)                                //Line 17
        cout << "Line 18: " << number
             << " is found at index " << pos
             << endl;                             //Line 18
    else                                          //Line 19
        cout << "Line 20: " << number
             << " is not in the list." << endl;   //Line 20

    return 0;                                     //Line 21
}                                                 //Line 22
//Place the definition of the function seqSearch
//given previously here.
```

**示例运行 1：** 在此示例运行中，用户输入以底纹显示。

```text
Line 9: Enter 10 integers.
2 56 34 25 73 46 89 10 5 16

Line 13: Enter the number to be searched: 25

Line 18: 25 is found at index 3
```

**示例运行 2：**

```text
Line 9: Enter 10 integers.
2 56 34 25 73 46 89 10 5 16

Line 13: Enter the number to be searched: 38

Line 20: 38 is not in the list.
```

## 排序

上一节讨论了一种查找算法。本节讨论如何使用一种称为**选择排序**的算法对数组进行排序。更多查找和排序算法将在第 16 章讨论。

顾名思义，在**选择排序**算法中，我们通过选择列表中的一个元素并将其移动到正确位置来重新排列列表。该算法找到列表未排序部分中最小元素的位置，并将其移动到列表未排序部分的开头。第一次，我们在整个列表中定位最小项。第二次，我们从列表的第二个元素开始，在列表中定位最小项，依此类推。

![](img/d0be7fc6d804b63484835c6c8bc67a07_595_0.png)

**图 8-9**  八个元素的列表

假设你有图 8-9 所示的列表。

![](img/d0be7fc6d804b63484835c6c8bc67a07_596_0.png)

**图 8-10** 第一次迭代期间列表的元素

图 8-10 显示了第一次迭代时列表的元素。

最初，整个列表都是未排序的。因此，我们找到列表中的最小项。最小项位于位置 6，如图 8-10(a) 所示。因为这是最小项，所以必须将其移动到位置 0。于是，我们将 16（即 list[0]）与 5（即 list[6]）交换，如图 8-10(b) 所示。交换这些元素后，得到的列表如图 8-10(c) 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_596_1.png)

**图 8-11** 第二次迭代期间列表的元素

图 8-11 显示了第二次迭代期间列表的元素。

现在未排序列表是 list[1]...list[7]。因此，我们找到未排序列表中的最小元素。最小元素位于位置 3，如图 8-11(a) 所示。因为未排序列表中的最小元素位于位置 3，所以必须将其移动到位置 1。于是，我们将 7（即 list[3]）与 30（即 list[1]）交换，如图 8-11(b) 所示。将 7（即 list[3]）与 30 交换后，得到的列表如图 8-11(c) 所示。

现在，未排序列表是 list[2]...list[7]。因此，我们重复前面的过程：找到列表未排序部分中最小元素（的位置），并将其移动到列表未排序部分的开头。因此，选择排序涉及以下步骤。

- 在列表的未排序部分中：
  - a. 找到最小元素的位置。
  - b. 将最小元素移动到未排序列表的开头。

最初，整个列表（即 list[0]...list[length − 1]）就是未排序列表。执行步骤 a 和 b 一次后，未排序列表为 list[1]...list[length − 1]。第二次执行步骤 a 和 b 后，未排序列表为 list[2]...list[length − 1]，依此类推。这样，我们可以跟踪列表的未排序部分，并借助 for 循环重复步骤 a 和 b，如下面的伪代码所示：

```text
for (index = 0; index < length − 1; index++)
{
    a. Find the location, smallestIndex, of the smallest element in
       list[index]...list[length − 1].
    b. Swap the smallest element with list[index]. That is, swap
       list[smallestIndex] with list[index].
}
```

第一次执行循环时，我们在 list[0]...list[length − 1] 中定位最小元素，并将该最小元素与 list[0] 交换。第二次执行循环时，我们在 list[1]...list[length − 1] 中定位最小元素，并将该最小元素与 list[1] 交换，依此类推。

步骤 a 类似于本章前面讨论的查找列表中最大项索引的算法。（另见本章末尾的编程练习 2a。）这里，我们查找列表中最小项的索引。步骤 a 的一般形式为：

```text
smallestIndex = index;    //assume first element is the smallest

for (location = index + 1; location < length; location++)
    if (list[location] < list[smallestIndex])
        smallestIndex = location;    //current element in the list
                                      //is smaller than the smallest so
                                      //far, so update smallestIndex
```

步骤 b 将 list[smallestIndex] 的内容与 list[index] 的内容交换。以下语句完成此任务：
