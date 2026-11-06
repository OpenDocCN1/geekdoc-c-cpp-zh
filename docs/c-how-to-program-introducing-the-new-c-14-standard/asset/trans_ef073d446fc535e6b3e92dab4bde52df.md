

```cpp
32    cout << "Unsorted array:\n";
35    // output original array
36    for (size_t i{0}; i < arraySize; ++i) {
37        cout << setw(4) << data[i];
38    }
40    selectionSort(data); // sort the array
42    cout << "\nSorted array:\n";
44    // output sorted array
45    for (size_t i{0}; i < arraySize; ++i) {
46        cout << setw(4) << data[i];
47    }
49    cout << endl;
50 }
```

```text
Unsorted array:
  34  56   4  10  77  51  93  30   5  52
Sorted array:
   4   5  10  30  34  51  52  56  77  93
```

图 20.5 使用选择排序将数组按升序排列。

## 选择排序算法

算法的第一次迭代选择最小的元素值，并将其与第一个元素的值交换。第二次迭代选择第二小的元素值（即剩余元素中最小的），并将其与第二个元素的值交换。算法继续下去，直到最后一次迭代选择第二大的元素，并将其与倒数第二个元素的值交换，使最大的值留在最后一个元素中。经过第 *i* 次迭代后，最小的 *i* 个值将被排序为递增顺序，位于数组的前 *i* 个元素中。

### 第一次迭代

第 31 行声明并初始化名为 `data` 的 `array`，其值如下：

```text
34    56    4    10    77    51    93    30    5    52
```

选择排序首先确定数组中的最小值（4），它位于元素 2。算法将 4 与元素 0 中的值（34）交换，结果为

```text
4    56    34    10    77    51    93    30    5    52
```

### 第二次迭代

然后，算法确定剩余元素（除 4 以外的所有元素）中的最小值，即 5，位于元素 8。程序将 5 与元素 1 中的 56 交换，结果为

```text
4    5    34    10    77    51    93    30    56    52
```

### 第三次迭代

在第三次迭代中，程序确定下一个最小值 10，并将其与元素 2 中的值（34）交换。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2408_0.png)

该过程持续进行，直到数组完全排序。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2408_1.png)

第一次迭代后，*最小*的元素位于*第一个*位置；第二次迭代后，*两个最小的*元素按*顺序*位于*前两个*位置，依此类推。

### 函数模板 `selectionSort`

函数模板 `selectionSort` 在第 12–26 行执行排序。循环迭代 `size − 1` 次。第 13 行声明并初始化变量 `indexOfSmallest`，它存储 `array` 未排序部分中最小元素的索引。第 16–20 行遍历剩余的数组元素。对于每个元素，第 17 行将当前元素的值与 `indexOfSmallest` 处的值进行比较。如果当前元素更小，第 18 行将当前元素的索引赋给 `indexOfSmallest`。当此循环结束时，`indexOfSmallest` 包含 `array` 中剩余最小元素的索引。然后第 23–25 行交换位置 `i` 和 `indexOfSmallest` 处的元素，使用临时变量 `hold` 存储 `items[i]` 的值，同时该元素被赋值为 `items[indexOfSmallest]`。

### *选择排序的效率*

选择排序算法迭代 \(n - 1\) 次，每次将剩余的最小元素交换到其已排序的位置。定位剩余最小元素在第一次迭代时需要 \(n - 1\) 次比较，第二次迭代时需要 \(n - 2\) 次，然后是 \(n - 3, \ldots, 3, 2, 1\)。这导致总共 \(n(n - 1)/2\) 或 \((n^2 - n)/2\) 次比较。用大 O 表示法表示，较小的项被省略，常数被忽略，留下大 O 复杂度 \(O(n^2)\)。我们能开发出比 \(O(n^2)\) *更优*的排序算法吗？

## 20.3.3 归并排序（递归实现）

**归并排序**是一种*高效*的排序算法，但在概念上比插入排序和选择排序*更复杂*。归并排序算法通过将 `array` *拆分*成两个大小相等的子 `array`，对每个子 `array` 进行排序，然后将它们*合并*成一个更大的 `array`。当元素个数为奇数时，算法创建两个子 `array`，其中一个比另一个多一个元素。

归并排序通过查看每个子 `array` 的第一个元素来执行合并，该元素也是该子 `array` 中的最小元素。归并排序取这些元素中最小的一个，并将其放入已合并排序 `array` 的第一个元素位置。如果子 `array` 中仍有元素，归并排序会查看该子 `array` 中的第二个元素（现在是剩余的最小元素），并将其与另一个子 `array` 中的第一个元素进行比较。归并排序继续此过程，直到合并后的 `array` 被填满。一旦某个子 `array` 没有更多元素，合并操作就会将另一个 `array` 的剩余元素复制到合并后的数组中。

### 合并示例

假设算法已经合并了较小的 `arrays` 以创建已排序的 `arrays` A：

```text
A = [
  4  10  34  56  77
]
```

和 B：

```text
B = [
  5  30  51  52  93
]
```

归并排序将这些 `arrays` 合并成一个已排序的 `array`。A 中的最小值是 4（位于 A 的第零个元素）。B 中的最小值是 5（位于 B 的第零个元素）。为了确定较大 `array` 中的最小元素，算法比较 4 和 5。来自 A 的值更小，因此 4 成为合并后 `array` 中第一个元素的值。算法继续将 A 中第二个元素的值 10 与 B 中第一个元素的值 5 进行比较。来自 B 的值更小，因此 5 成为较大 `array` 中第二个元素的值。算法继续比较 10 和 30，10 成为 `array` 中第三个元素的值，依此类推。

### 递归实现

我们的归并排序实现是*递归*的。基本情况是只有一个元素的 `array`。这样的 `array` 当然是有序的，因此当使用单元素 `array` 调用归并排序时，它会立即返回。*递归*步骤将包含两个或更多元素的 `array` 拆分为两个大小相等的子 `array`，递归地对每个子 `array` 排序，然后将它们合并成一个更大的、已排序的 `array`。[同样，如果元素个数为奇数，一个子 `array` 比另一个多一个元素。]

### 演示归并排序

**图 20.6** 实现并演示了归并排序算法。在程序执行过程中，我们使用函数模板 `displayElements`（第 10–22 行）显示当前正在拆分和合并的 `array` 部分。函数模板 `mergeSort`（第 25–48 行）和 `merge`（第 51–98 行）实现了归并排序算法。函数 `main`（第 100–125 行）创建一个 `array`，用随机整数填充它，执行算法（第 120 行）并显示已排序的数组。该程序的输出显示了归并排序执行的拆分和合并，展示了排序在算法每一步的进展。

```cpp
// Fig 20.6: Fig20_06.cpp
// Sorting an array into ascending order with merge sort.
#include <array>
#include <ctime>
#include <iostream>
#include <random>
using namespace std;

// display array elements from index low through index high
template <typename T, size_t size>
void displayElements(const array<T, size>& items,
    size_t low, size_t high) {
    for (size_t i{0}; i < items.size() && i < low; ++i) {
        cout << "  "; // display spaces for alignment
    }

    for (size_t i{low}; i < items.size() && i <= high; ++i) {
        cout << items[i] << " "; // display element
    }

    cout << endl;
}

// split array, sort subarrays and merge subarrays into sorted array
template <typename T, size_t size>
void mergeSort(array<T, size>& items, size_t low, size_t high) {
    // test base case; size of array equals 1
    if ((high - low) >= 1) { // if not base case
        size_t middle1{(low + high) / 2}; // calculate middle of array
        size_t middle2{middle1 + 1}; // calculate next element over
```

