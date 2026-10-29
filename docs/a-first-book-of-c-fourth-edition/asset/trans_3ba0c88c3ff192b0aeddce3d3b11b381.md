

## 7.6 章节总结

1. 一维数组是一种可用于存储相同数据类型的值列表的数据结构。这些数组必须通过给出存储在数组中的值的的数据类型和数组大小来声明。例如，声明

```cpp
int num[100];
```

创建了一个包含 100 个整数的数组。更可取的方法是先使用符号常量设置数组大小，然后在数组定义中使用该常量，如以下示例所示：

```cpp
const int MAXSIZE = 100;
```

和

```cpp
int num[MAXSIZE];
```

2. 数组元素存储在内存中的连续位置，并通过使用数组名和下标（或索引）来引用，例如 `num[22]`。任何非负整数值表达式都可以用作下标，且下标 0 总是指数组中的第一个元素。

3. 二维数组通过列出行大小和列大小以及数据类型和数组名来声明。例如，以下声明创建了一个由五个行和七列整数值组成的二维数组：

```cpp
const int ROWS = 5;
const int COLS = 7;
int mat[ROWS][COLS];
```

4. 数组可以在声明时进行初始化。对于二维数组，可以在花括号内按行列出初始值并用逗号分隔。例如，声明

```cpp
int vals[3][2] = { {1, 2},
                   {3, 4},
                   {5, 6} };
```

产生以下三行二列的数组：

```text
1  2
3  4
5  6
```

由于 C++ 使用按行顺序初始化的约定，可以省略内部花括号。因此，以下语句是等价的初始化：

```cpp
int vals[3][2] = {1, 2, 3, 4, 5, 6};
```

5. 数组通过将数组名作为参数传递给函数来传递。实际传递的值是第一个数组存储位置的地址。因此，被调用的函数
接收到对原始数组的直接访问，而不是数组元素的副本。必须在被调用函数中声明一个参数来接收传递的数组名。参数的声明可以省略一维和二维数组的数组行大小。

## 7.7 章节补充：搜索和排序方法

大多数程序员在编程生涯中某个时候都会遇到需要对数据项列表进行排序和搜索的需求。例如，你可能需要将实验结果按升序（递增）或降序（递减）排列以进行统计分析，或将姓名列表按字母顺序排序并搜索该列表以查找特定姓名。同样，你可能需要将日期列表按升序或降序排列并搜索该列表以定位特定日期。本节介绍排序和搜索列表的基础知识。注意，在搜索之前对列表进行排序并非必要，尽管如果列表已排序，则可以进行更快的搜索，如你将看到的。

### 搜索算法

许多程序的常见需求是在列表中搜索给定元素。例如，在姓名和电话号码列表中，你可能搜索特定姓名以便打印对应的电话号码，或可能只是为了确定姓名是否存在于列表中。执行这些搜索的两种最常见方法是线性搜索算法和二分搜索算法。

### 线性搜索

在线性搜索中，也称为顺序搜索，列表中的每个项目按其出现的顺序进行检查，直到找到所需项目或到达列表末尾为止。这种搜索方法类似于查看电话目录中的每个姓名，从 Aardvark、Aaron 开始，直到找到你想要的姓名或到达 Zzxgy、Zora。显然，这不是搜索长字母排序列表的最有效方法。然而，线性搜索具有以下优点：

- 算法简单。
- 列表不必按特定顺序排列。

在线性搜索中，搜索从列表中的第一个项目开始并按顺序逐项继续。执行线性搜索的函数的伪代码如下：

```
For all items in the list
  Compare the item with the desired item
  If the item is found
    Return the index value of the current item
  EndIf
EndFor
Return -1 if the item is not found
```

请注意，函数的返回值指示是否找到该项目。如果返回值是 -1，则该项目不在列表中；否则，for 循环中的返回值提供了该项目在列表中的索引位置。linearSearch() 函数以 C++ 函数的形式说明了此过程：

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

在回顾 linearSearch() 时，请注意 for 循环只是用于访问列表中的每个元素，从第一个到最后一个，直到找到与所需项目的匹配为止。如果找到该项目，则返回当前项目的索引值，这会导致循环终止；否则，搜索将继续直到遇到列表末尾。

为了测试此函数，已编写了一个 main() 驱动函数来调用 linearSearch() 并显示其返回的结果。程序 7.9 显示了完整的测试程序。

### 程序 7.9

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

if (location > -1)
    cout << "The item was found at index location "
         << location << endl;
else
    cout << "The item was not found in the list\n";

return 0;
}

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

程序 7.9 的示例运行如下：

```
Enter the item you are searching for: 101
The item was found at index location 9

and

Enter the item you are searching for: 65
The item was not found in the list
```

如前所述，线性搜索的一个优点是列表不必按排序顺序即可执行搜索。另一个优点是如果搜索项位于列表的前部，则只进行少量比较。当然，最坏的情况是搜索项位于列表末尾。平均而言，假设项目在列表中任何位置出现的可能性相等，则所需的比较次数为 n/2，其中 n 是列表的大小。因此，对于 10 个元素的列表，线性搜索平均需要的比较次数为 5，对于 10,000 个元素的列表，平均需要的比较次数为 5000。正如你接下来看到的，使用二分搜索算法可以大幅减少这个数字。

### 二分搜索

在二分搜索中，列表必须按排序顺序排列。从有序列表开始，所需项目首先与列表中间的元素进行比较。 （对于元素数量为偶数的列表，可以使用两个中间元素中的任意一个。）比较后有三种可能性：所需项目可能等于中间元素，可能大于中间元素，或可能小于中间元素。

在第一种情况下，搜索已成功，无需进一步搜索。在第二种情况下，由于所需项目大于中间元素，如果找到它，则它必须在列表的后半部分。这意味着列表的第一部分，从第一个元素到中点，可以从任何进一步的搜索中丢弃。在第三种情况下，由于所需项目小于中间元素，如果找到它，则它必须在列表的前半部分。对于这种情况，列表的后半部分，包含从中点到最后一个元素的所有元素，可以从任何进一步的搜索中丢弃。

此搜索策略的算法如图 7.11 所示，并由以下伪代码定义：

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
