
## 程序 20-6

```cpp
// 此程序演示了一个递归函数
// 计算斐波那契数。
#include <iostream>
using namespace std;

// 函数原型
int fib(int);

int main()
{
    cout << "The first 10 Fibonacci numbers:\n";
    for (int x = 0; x < 10; x++)
        cout << fib(x) << " ";
    cout << endl;
    return 0;
}

//****************************************************
// 函数 fib。接受一个 int 类型参数
// n。此函数返回第 n
// 个斐波那契数。
//****************************************************
int fib(int n)
{
    if (n <= 0)              // 边界情况
        return 0;
    else if (n == 1)        // 边界情况
        return 1;
    else
        return fib(n - 1) + fib(n - 2); // 递归情况
}
```

### 程序输出

前 10 个斐波那契数是：
0 1 1 2 3 5 8 13 21 34

另一个例子是 `Ackermann` 函数。章节末的编程挑战将要求你写一个计算 `Ackermann` 函数的递归函数。

## 20.5 关注问题解决与程序设计：递归链表操作

概念：递归可以遍历链表中的节点。

回顾第 18 章，我们讨论过一个 `NumberList` 类，它包含一个 `double` 值的列表。在本节中，我们将通过添加递归函数来修改该类。这些函数将使用递归遍历列表并执行以下操作：

- 遍历列表中的节点。
- 以反序显示列表。
- 在列表末尾添加元素。
- 删除列表中的元素。

### 程序输出

列表中的值如下：
- 1.5
- 2.6
- 3.7
- 4.8
- 5.9
- 7
- 8.1
- 9.2

倒序排列的值如下：
- 9.2 8.1 7 5.9 4.8 3.7 2.6 1.5

## 20.6 关注问题解决与程序设计：递归二分查找函数

> 概念：二分查找算法可以定义为一个递归函数。

在第 8 章中，你学习了二分查找算法并看到了一个用 C++ 编写的迭代示例。二分查找算法也可以通过递归实现。例如，该过程表示：

```cpp
如果 array[middle] 等于搜索值，则找到了该值。
否则，如果 array[middle] 小于搜索值，则对数组的上半部分执行二分查找。
否则，如果 array[middle] 大于搜索值，则对数组的下半部分执行二分查找。
```

递归二分查找算法是将一个问题分解为更小部分直到问题解决的示例。这里展示了一个递归二分查找函数：

```cpp
int binarySearch(int array[], int first, int last, int value)
{
    int middle; // 搜索的中点
    if (first > last)
        return -1;
    middle = (first + last) / 2;
    if (array[middle] == value)
        return middle;
    if (array[middle] < value)
        return binarySearch(array, middle + 1, last, value);
    else
        return binarySearch(array, first, middle - 1, value);
}
```

第一个参数 `array` 是要搜索的数组。下一个参数 `first` 存储搜索范围内第一个元素的下标。下一个参数 `last` 存储搜索范围内最后一个元素的下标。最后一个参数 `value` 存储要搜索的值。与迭代版本一样，如果找到了该值，则返回该值的下标；如果没有找到，则返回 -1。

### 程序 20-9

```cpp
// 此程序演示了递归 binarySearch 函数。
#include <iostream>
using namespace std;

// 函数原型
int binarySearch(int [], int, int, int);

const int SIZE = 20; // 数组大小

int main() 
{
    // 定义一个员工 ID 数组
    int tests[SIZE] = {101, 142, 147, 189, 199, 207, 222, 234, 289, 296, 310, 319, 388, 394, 417, 429, 447, 521, 536, 600};
    int empID; // 用于存储 ID 号
    int results; // 用于存储搜索结果

    // 获取一个要搜索的员工 ID。
    cout << "Enter要搜索的员工 ID: ";
    cin >> empID;

    // 在数组中搜索该 ID。
    results = binarySearch(tests, 0, SIZE - 1, empID);

    // 显示搜索结果。
    if (results == -1)
        cout << "数组中不存在该数字。\n";
    else
        cout << "在该 ID 位于数组的元素 " << results << " 位置\n";

    return 0;
}

// binarySearch 函数对整数元素范围执行递归二分查找。
// 参数 array 存储范围起始元素的下标，
// 参数 last 存储范围结束元素的下标。
// 参数 value 存储搜索值。
// 如果找到了搜索值，则返回其下标；否则返回 -1。
int binarySearch(int array[], int first, int last, int value)
{
    int middle; // 搜索的中点
    if (first > last)
        return -1;
    middle = (first + last) / 2;
    if (array[middle] == value)
        return middle;
    if (array[middle] < value)
        return binarySearch(array, middle + 1, last, value);
    else
        return binarySearch(array, first, middle - 1, value);
}
```

#### 程序输出

```text
输入要搜索的员工 ID: 521
该 ID 位于数组的元素 17
```

## 20.7 汉诺塔

> 概念：解决汉诺塔游戏中的重复步骤可以很容易用递归算法实现。

汉诺塔是一种经常用于计算机科学教科书中演示递归能力的数学游戏。该游戏使用三个柱子和一组圆盘，如图 20-4 所示。

**图 20-4** 汉诺塔的柱子和圆盘 ![](img/191adf328469956a7b1008ce9bdb5_127.png)

圆盘堆在左侧柱子上，最大的在底部。该游戏基于一个传说：汉诺塔有 64 个圆盘。僧的任务是将圆盘从第一个柱移动到第三个柱。中间的柱可以作为临时位置。此外，僧在移动圆盘时遵循以下规则：

- 每次只能移动一个圆盘。
- 圆盘不能放在较小的圆盘之上。
- 除了移动中的，圆盘必须存储在柱子上。

根据传说，当僧将所有圆盘从第一个柱移动到最后一个柱时，世界将终结。遵循相同的规则，让我们看看针对不同数量圆盘的某些解决方案。如果你只有一个圆盘，游戏的解决方案很简单：将圆盘从第一个柱移动到第三个柱。如果你有两个圆盘，解决方案需要三步：

- 将圆盘 1 移动到第二个柱。
- 将圆盘 2 移动到第三个柱。
- 将圆盘 1 移动到第三个柱。

注意这种方法使用第二个柱作为临时位置。随着圆盘数量的增加，移动复杂度持续增加。移动三个圆盘需要七步，如图 20-5 所示。

**图 20-5** 移动三个圆盘 ![](img/191adf328469956a7b1008ce9bdb5_1277.png)

初始设置 ![](img/191adf328469956a7b1008ce9bdb5_1277_1.png)
第一步：将圆盘 1 移动到第三个柱 ![](img/191adf328469956a7b1008ce9bdb5_1277_2.png)
第二步：将圆盘 2 移动到第二个柱 ![](img/191adf328469956a7b1008ce9bdb5_1277_3.png)
第三步：将圆盘 1 移动到第二个柱 ![](img/191adf328469956a7b1008ce9bdb5_1277_4.png)
第四步：将圆盘 3 移动到第三个柱 ![](img/191adf328469956a7b1008ce9bdb5_1277_5.png)
第五步：将圆盘 1 移动到第一个柱 ![](img/191adf328469956a7b1008ce9bdb5_1277_6.png)
第六步：将圆盘 2 移动到第三个柱 ![](img/191adf328469956a7b1008ce9bdb5_1277_7.png)
第七步：将圆盘 1 移动到第三个柱。

以下陈述描述了问题的整体解决方案：将 `n` 个圆盘从第一个柱移动到第三个柱，使用第二个柱作为临时柱。

以下伪代码算法可以作为模拟游戏解决方案递归函数的基础。注意在算法中，我们使用变量 `A`、`B` 和 `C` 来存储柱的编号。

```text
将 n 个圆盘从柱 A 移动到 C，使用柱 B 作为临时柱
如果 n > 0 则
  将 n-1 个圆盘从柱 A 移动到 B，使用柱 C 作为临时柱
  将剩余的圆盘从柱 A 移动到 C
  将 n-1 个圆盘从柱 B 移动到 C，使用柱 A 作为临时柱
结束
```

当没有更多圆盘可以移动时，到达算法的基础情况。以下代码是实现该算法的函数。注意该函数并没有实际移动任何东西，而是显示指令。

```cpp
void moveDiscs(int num, int fromPeg, int toPeg, int tempPeg)
{
    if (num > 0)
    {
        moveDiscs(num - 1, fromPeg, tempPeg, toPeg);
        cout << "Move a disc from " << fromPeg
             << " to peg " << toPeg << endl;
        moveDiscs(num - 1, tempPeg, toPeg, fromPeg);
    }
}
```

该函数接收以下参数：

| 参数 | 说明 |
| :--- | :--- |
| `num` | 要移动的圆盘数量。 |
| `fromPeg` | 移动圆盘的柱。 |
| `toPeg` | 移动圆盘的目标柱。 |
| `tempPeg` | 用作临时使用的柱。 |

如果 `num` 大于 0，则有圆盘需要移动。第一次递归调用是：

```cpp
moveDiscs(num - 1, fromPeg, tempPeg, toPeg);
```

这条语句是将除一个以外的所有圆盘从 `fromPeg` 移动到 `tempPeg`，使用 `toPeg` 作为临时柱。下一条语句是：

```cpp
cout << "Move a disc from " << fromPeg
     << " to peg " << toPeg << endl;
```

这只是显示一条消息，说明应该从 `fromPeg` 移动圆盘到 `toPeg`。接着执行另一个递归调用：

```cpp
moveDiscs(num - 1, tempPeg, toPeg, fromPeg);
```

这条语句是将除一个以外的所有圆盘从 `tempPeg` 移动到 `toPeg`，使用 `fromPeg` 作为临时柱。

### 程序 20-10

```cpp
// 此程序演示了汉诺塔
// 游戏的一种解决方案。
#include <iostream>
using namespace std;

// 函数原型
void moveDiscs(int, int, int, int);

int main()
{
    const int NUM_DISCS = 3; // 要移动的圆盘数量
    const int FROM_PEG = 1; // 初始“起始”柱
    const int TO_PEG = 3; // 初始“目标”柱
    const int TEMP_PEG = 2; // 初始“临时”柱

    // 玩游戏。
    moveDiscs(NUM_DISCS, FROM_PEG, TO_PEG, TEMP_PEG);
    cout << "所有的柱子都移动完毕!\n";
    return 0;
}

//******************************************************
// moveDiscs 函数显示汉诺塔游戏中的一次
// 盘子移动。
// 参数为：
// num: 要移动的盘子数量。
// fromPeg: 移出的柱子。
// toPeg: 移动到的柱子。
// tempPeg: 临时柱子。
//******************************************************
void moveDiscs(int num, int fromPeg, int toPeg, int tempPeg)
{
    if (num > 0)
    {
        moveDiscs(num - 1, fromPeg, tempPeg, toPeg);
        cout << "Move a disc from " << fromPeg
            << " to peg " << toPeg << endl;
        moveDiscs(num - 1, tempPeg, toPeg, fromPeg);
    }
}
```

#### 程序输出

```text
Move a disc from peg 1 to peg 3
Move a disc from peg 1 to peg 2
Move a disc from peg 3 to peg 2
Move a disc from peg 1 to peg 3
Move a disc from peg 2 to peg 1
Move a disc from peg 2 to peg 3
Move a disc from peg 1 to peg 3
All the pegs are moved!
```

## 20.8 关注问题解决与程序设计：快速排序算法

概念：快速排序算法使用递归来高效地排序列表。

快速排序算法是由 C.A.R. Hoare 在 1960 年开发的一种流行的通用排序程序。它可以用于对数组或链表中的列表进行排序。它通过将列表分为两个子列表来对其排序。子列表之间有一个选定的值，称为基值（`pivot`）。这如图 20-6 所示。

**图 20-6** 分区的数据集 ![](img/191adf3284699566e6a7b1008ce9bdb_1280_0.png)

注意，在第一个子列表中，元素位于基值的左侧（之前），而子列表 2 位于基值的右侧（之后）。一旦选定了基值，算法就会交换列表中的其他值，直到子列表 1 中的所有元素都小于基值，而子列表 2 中的所有元素都大于基值。

完成后，算法对子列表 1 重复该过程，然后对子列表 2 重复。当子列表中仅剩元素时，递归停止。此时，原始列表已完全排序。

该算法主要由两个函数编写：`quickSort` 和 `partition`。`quickSort` 是一个递归函数。其伪代码所示：

```text
quickSort:
  If Starting Index < Ending Index
    围绕 Pivot 对列表进行分区
      quickSort Sublist 1
      quickSort Sublist 2
  End If
```

这里是 `quickSort` 函数的 C++ 代码：

```cpp
void quickSort(int set[], int start, int end)
{
  if (start < end)
  {
    // 获取基值点。
    pivotPoint = partition(set, start, end);
    // 排序第一个子列表。
    quickSort(set, start, pivotPoint - 1);
    // 排序第二个子列表。
    quickSort(set, pivotPoint + 1, end);
  }
}
```
