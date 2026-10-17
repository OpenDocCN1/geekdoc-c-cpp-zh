
程序 9-1 是一个使用 `searchList` 函数的完整程序。它搜索包含五个元素的数组以寻找分数为 100 的。

# 程序 9-1

```cpp
1 // 此程序演示了 searchList 函数，
2 // 该函数在整数数组上执行线性查找。
3 #include <iostream>
4 using namespace std;
```

# 程序 9-1（续）

```cpp
6 // 函数原型
7 int searchList(const int [], int, int);
9 const int SIZE = 5;
11 int main()
{
    int tests[SIZE] = {87, 75, 98, 100, 82};
    int results; // 存储搜索结果
    // 在数组中查找值 100
    results = searchList(tests, SIZE, 100);
    // 如果 searchList 返回 -1，则未找到 100
    if (results == -1)
        cout << "You did not earn 100 points on any test.";
    else
        // 在数组中找到的第一个100分
        cout << "You earned " << (results + 1) << " points on test.";
    return 0;
}

/* searchList 在整数数组上执行线性查找。
* list 数组大小为 size 个元素，用于查找
* 存储在 value 中的数字。如果找到了该数字，则返回其
*下标。否则，返回 -1。
 */
int searchList(const int list[], int size, int value)
{
    int index = 0; // 用于搜索数组的下标
    int position = -1; // 用于记录搜索值的位置
    bool found = false; // 用于指示是否找到该值的标志
    while (index < size && !found)
        if (list[index] == value) // 如果找到了值
            found = true; // 设置标志
            position = index; // 记录值的下标
        index++; // 移动到下一个元素
    return position; // 返回位置，或 -1
}
```

程序输出

`nYou earned 100 points on test.`

# 线性查找的低效性

线性查找的优点是它的简单性。它非常容易理解和实现。此外，它不需要数组中的数据以任何顺序存储。然而，它的缺点是效率低下。如果搜索的数组有 20,000 个元素，算法必须查看所有 20,000 个元素才能找到存储在最后一个元素中的值，或者确定它不在数组中。

在通常情况下，一个项目在数组开头找到和在末尾找到概率是相等的。对于 N 个项目，线性查找平均会在 N/2 个元素中定位一个项目。如果一个数组有 20,000 个元素，线性查找平均将对其中 10,000 个元素进行比较。当然，这是在该项目始终在数组中能被找到的情况下。N/2 是平均比较次数。当线性查找未能定位某个项目时，最大比较次数总是 N；它必须与数组中的每个元素进行比较。随着失败查找尝试次数的增加，平均比较次数也会之增加。如果可以避免这种情况，且速度很重要，则不在大数组上使用线性查找。

# 二分查找

二分查找是一种智能算法，比线性查找高效得多。它唯一的要求是数组中的值是有序的。该算法不是测试数组的第一个元素，而是从中间元素开始。如果该元素恰好包含所需的值，搜索就结束。否则，中间元素的值要么大于要么小于要搜索的值。如果它大于所需值，那么该值（如果在列表中）将在数组的前半部分找到。如果它小于所需值，则该值将在数组的后半部分找到。

## 9.1 搜索算法介绍

```
Set first to 0
Set last to size - 1
Set found to false
Set position to -1
While is not true and first <= last
Set middle to subscript between first and last
If array[middle] equals the desired value
    Set found to true
    Set position to middle
Else If array[middle] is greater than the desired value
    Set last to middle - 1
Else
    Set first to middle + 1
End If
End While
Return position
```

该算法使用三个索引变量：`first`、`last` 和 `middle`。`first` 和 `last` 标记了当前搜索数组部分的边界。它们被初始化为数组第一个和最后一个元素的下标。first 和 last 中间的元素下标存储在 `middle` 变量中。如果没有精确的中心元素，用于计算中间值的整数除法会选择中点之前的元素。如果数组中间的元素不包含搜索值，则调整 `first` 或 `last` 变量，以便在下次迭代中仅搜索数组的一半。这种过程持续到找到该值。

```cpp
int binarySearch(const int array[], int size, int value)
{
    int first = 0; // 第一个数组元素
    last = size - 1; // 最后一个数组元素
    middle, // 搜索的中点
    position = -1; // 搜索值的位置
    bool found = false; // 用于指示是否找到该值的标志
    while (!found && first <= last)
    {
        middle = (first + last) / 2; // 计算中点
        if (array[middle] == value) // 如果在中点找到值
            found = true;
            position = middle;
        }
        else if (array[middle] > value) // 如果值在下半部分
        last = middle - 1;
        else
        first = middle + 1; // 如果值在上半部分
    }
    return position;
}
```

# 第 9 章 搜索、排序与算法分析

程序 9-2 是一个使用 `binarySearch` 函数的完整程序。它在员工 ID 数组中搜索特定值。

## 程序 9-2

```cpp
1 // 此程序对整数数组执行二分查找
2 // 数组的元素是升序排列的。
3 #include <iostream>
4 using namespace std;
5
6 // 函数原型
7 int binarySearch(const int [], int, int);
8
9 const int SIZE = 20;
10
11 int main(){
12 {
13 // 创建升序排列的 ID 数字数组
14 int IDNums[SIZE] = { 101, 142, 147, 189, 199, 207, 222,
15 234, 289, 296, 310, 319, 388, 394,
16 417, 429, 447, 521, 536, 600 };
17
18 int empID; // 存储要搜索的 ID
19 int results; // 存储搜索结果
20
21 // 获取要搜索的员工 ID：
22 cout << "请输入要搜索的员工 ID: ";
23 cin >> empID;
24
25 // 搜索 ID
26 results = binarySearch(IDNums, SIZE, empID);
27
28 // 如果 binarySearch 返回 -1，说明未找到该 ID
29 if (results == -1)
30 cout << "该员工在数组中不存在。"
31 else
32 { // 否则，results 包含数组中
33 // 目标员工 ID 的子下标
34 cout << "ID " << empID << " 在数组的元素 "
35 << results << " 中找到。";
36 }
37 return 0;
38 }
39
40 *****************************************************
41 * 此函数对整数数组执行二分查找，
42 * 数组大小为 elements，其值按升序存储。
43 * 搜索 value 参数中存储的数字。
44 * 如果找到了该数字，则返回其数组下标。
45 * 否则，返回 -1。
46 *****************************************************/
47             binarySearch
```

## 9.1 搜索算法简介

```cpp
int binarySearch(const int array[], int size, int value)
{
    int first = 0, // 数组第一个元素
    int last = size - 1, // 数组最后一个元素
    int middle, // 搜索的中间点
    int position = -1; // 搜索值的位置
    bool found = false; // 标志位

    while (!found && first <= last) {
        middle = (first + last) / 2; // 计算中间点
        if (array[middle] == value) { // 如果在中间找到值
            found = true;
            position = middle;
        } else if (array[middle] == value) { // 如果值在下半部分
            last = middle - 1;
        } else {
            first = middle + 1; // 如果值在上半部分
        }
    }
    return position;
}
```

## 示例输入对应的程序输出（粗体为显示）

请输入要搜索的员工 ID: **199**

在数组的元素 4 中找到了 ID 199。

## 二分查找的效率

显然，二分查找比线性查找高效得多。每当它进行一次比较并未能找到项时，它都会排除待搜索数组的一半。例如，对于 20,000 个元素，如果二分查找在第一次尝试时未找到项，则需要搜索的元素数量为 10,000 个。如果第二次尝试未找到，则需要搜索的元素数量为 5,000 个。这个过程会一直持续，直到二分查找定位所需的值或确定其不存在。

2 的幂被用于计算二分查找对任何大小的数组可能进行的最大比较次数。（大于数组元素数量的 2 的幂将告诉您找到元素或确定其不存在所需的最大比较次数。例如，在包含 50,000 个元素的数组中找到一个项最多需要 16 次比较（$2^{16} = 65,536$），在包含 1,000,000 个元素的数组中找到一个项最多需要 20 次比较（$2^{20} = 1,048,576$）。

## 搜索对象数组

**概念：** 线性查找和二分查找也可以用于搜索对象或结构体数组中的特定条目。在程序 9-1 和 9-2 中，我们在整数数组中搜索了特定值。我们可以轻松地搜索包含其他类型（如 `double` 或 `string`）值的数组。我们甚至可以搜索对象或结构体数组。然而，在这种情况下，我们搜索的不是整个对象或结构，而是该对象或结构中特定成员变量的值。被搜索检查的成员变量有时被称为*键字段*（key field），而查找的特定值被称为*搜索键*（search key）。

假设我们有一个名为 `Inventory` 的类。 （由于后续文本在 `Inventory` 之后出现了严重乱码和重复，已根据上下文逻辑进行了截断。）

# 排序算法介绍

## 检查点

9.1 描述线性搜索和二分查找之间的区别。

9.2 在平均情况下，对于一个包含 1,000 个元素的数组，线性搜索会执行多少次比较？（假设要查找的项目在数组中总能找到。）

9.3 对于一个包含 1,000 个元素的数组，二分查找执行的最大比较次数是多少？

9.4 如果对一个数组进行线性搜索，且已知某些项的搜索频率比其他项高，应该如何重新排列数组的内容以提高搜索的平均性能？

# 排序算法介绍

概念：排序算法用于将数据按照某种顺序排列。

通常，数组中的数据必须按照某种顺序进行排序。例如，客户列表通常按字母顺序排序。学生成绩可能按从高到低排序。邮寄标签可以按邮政编码排序。要对数组进行排序，程序员必须使用适当的排序算法。排序算法扫描数组并按照特定顺序重新排列其内容的技术。本节将介绍两种简单的排序算法：冒泡排序和选择排序。

![](img/1c095ef63c71a34f9802f104f947be57_647_0.png)

# 冒泡排序

冒泡排序是一种按升序或降序排列数据的方法。按升序排序数据意味着将值从低到高排列。按降序排序意味着将其从高到低排列。冒泡排序将每个元素与其相邻元素比较，如果它们不符合所需的顺序，则交换它们。让我们看看它是如何按升序顺序排列以下元素的：

| 7 | 2 | 3 | 8 | 9 | 1 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

冒泡排序从比较数组的前两个元素开始。如果元素 0 大于元素 1，则交换它们。交换后，数组显示为：

| 2 | 7 | 3 | 8 | 9 | 1 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

该过程对元素 1 和 2 重复。如果元素 1 大于元素 2，则交换它们。数组现在显示为：

| 2 | 3 | 7 | 8 | 9 | 1 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

接下来，比较元素 2 和 3。然而，在数组中，这两个元素已经处于正确的顺序（元素 2 小于元素 3），因此没有发生交换。

# 第9章 搜索、排序与算法分析

随着循环继续，比较元素 3 和 4。一旦放置好，由于它们已经处于正确的顺序，因此不需要交换。当比较元素 4 和 5 时，必须发生交换，因为元素 4 大于元素 5。数组现在显示为：

```
2 7 8 1 9
Element 0 Element 1 Element 2 Element 3 Element 4 Element 5
```

此时，整个数组已经扫描完毕。这是排序的第一轮。注意，最大值现在被正确地放置在数组的末尾。然而，数组的其余部分尚未排序。排序从元素 0 和 1 重新。因为它们处于正确的顺序，所以没有发生交换。比较元素 1 和 2，但再次没有发生交换。这种情况一直持续到比较元素 3 和 4。因为元素 3 大于元素 4，它们被交换。数组现在显示为：

```
2 7 1 8 9
Element 0 Element 1 Element 2 Element 3 Element 4 Element 5
```

注意，对数组的第二次遍历已经将第二大的数字放置在数组的最后。这个过程将持续进行，排序将反复遍历数组，并在每轮中至少放置一个顺序正确的数字，直到数组被完全排序。最终，数组将显示为：

```
1 2 7 8 9
Element 0 Element 1 Element 2 Element 3 Element 4 Element 5
```

这是一个伪代码形式的冒泡-while 循环。注意它使用了一对嵌套循环。外层循环是一个 do-while 循环，在排序的每轮迭代一次。内层循环是一个 for 循环，包含了在该轮中进行所有比较和所需交换的代码。

```
Do
  Set madeASwap to false
  For count = 0 to next-to-last
    If array[count] > array[count + 1]
      Swap array[count] and array[count + 1]
      Set madeASwap to true
  End
While madeASwap
```

9.3 排序算法简介 651

# 程序 9-4（续）

```
****************************************************
* showArray
* 此函数显示数组的内容。
* 参数 size 存储数组中元素的数量。
****************************************************
void showArray(const int array[], int size)
{
    for (int count = 0; count < size; count++)
        cout << array[count] << " ";
}
```

程序输出

未排序的值为：

2 7 3 8 9 1

已排序的值为：

1 2 3 7 8 9

# 选择排序
