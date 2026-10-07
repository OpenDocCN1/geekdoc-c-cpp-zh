

# 抽象数据结构

因此，可以在常数时间内获取已知内存位置内容的（随机）访问。对于在 `dArray` 对象的末尾添加新条目也是如此，但对象已经满满的情况除外。具体而言，我们对 `append` 方法的定义如下：

```
void dArray::append(int value){
  if (Size < containerSize){
    p[Size] = value;
    Size++;
  }
  else{
    resize();
    p[Size] = value;
    Size++;
  }
}
```

数组中最后一个对象的位置始终可以通过成员变量 `Size` 的值获取；即其索引为 `Size - 1`。只要存在空闲内存位置，`append` 操作就需要常数时间。否则，在创建新的 `int` 对象之前，必须调用 `resize` 函数。

虽然数组适用于访问和添加新元素，但根据新数据对象必须放置的位置，插入操作可能会非常慢。算法 9.1 描述了在具有现有条目 $A[1],....A[m]$（其中 $m < n$）的 $n$ 元素数组的第 $k$ 个槽位插入新条目的过程。

# 算法 9.1 insert(k, a): 插入新数组条目

```
tempLow = A[k]
A[k] = a
for j = k to m - 1 do
  tempUp = A[j+1]
  A[j+1] = tempLow
  tempLow = tempUp
end
A[m+1] = tempLow
```

因此，完成插入所需的时间取决于发生的位置，平均时间复杂度与存储中元素的数量成正比。

我们为 `dArray` 类实现的 `insert` 方法使用了算法 9.1 的变体。

```
void dArray::insert(int k, int value){
  if (k > Size){
    std::cout << "This is not a valid index!" << std::endl;
    exit(1);
  }

  if (Size == containerSize){
    resize();
    Size++;
  }
  for (int j = Size; j > k; j--)
    p[j] = p[j-1];
  }
  p[k] = value;
}
```

# ADT 字典 (DICTIONARY)

算法 9.1 的修改在于当数组变满时调用 `resize` 以容纳另一个存储的条目。另一种方式是数组起始元素的移动方式。`Size` 的第一个值增加。这允许我们从索引为 `Size - 1` 的槽位开始，并在移动每个条目一个数组的位置的同时后移动。这种方法的优点是避免了临时存储。

插入的另一端是删除。从 `dArray` 对象中移除元素可能是很有用的，如果删除多次删除后 `Size` 变得足够小，那么调整大小可能作为节省内存的有效手段。这些操作的实现是练习 9.3-9.4 的主题。

以下代码为我们的 `dArray` 类提供了测试。

```cpp
//dArrayDriver.cpp
#include <iostream>
#include "darray.h"

int main() {
    int* pa;
    pa = new int[2];
    pa[0] = 2; pa[1] = 4;

    dArray v(2);
    v.append(14); v.append(14);
    std::cout << v.getSize() << " " << v.getContainerSize() << "";
    std::cout << std::endl;
    v.insert(1, 9);
    std::cout << v.getSize() << " " << v.getContainerSize() << "";
    std::cout << std::endl;
    for(int i = 0; i < v.getSize(); i++) {
        std::cout << v[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

`dArray` 对象用一个指向 `int` 的指针初始化，该指针对应两个整数对象。因此，初始 `Size` 值应为 2，`containerSize` 的初始值应为 4。数组中追加了一对整数，并检查了 `Size` 和 `containerSize` 的值。插入一个 `int` 以强制调用 `resize` 方法，之后再次检查 `Size` 和 `containerSize`，并将 `dArray` 对象的的内容打印到标准输出。程序产生：

```
4 4
Resize called
5 8
2 9 7 14
```

有必要用数值方法对元素进行排序，以获得例如感兴趣的统计数据。我们已经在泡沫排序算法 3.1 和第 6.4 节的选择排序方法中见过排序方法的示例。这些排序方案速度较慢，且排序一个 $n$ 元素数组平均需要 $n^2$ 次操作。更好的选择是快速排序算法，它平均需要 $O(n \log n)$ 次操作来对元素进行排序。

快速排序背后的思想很简单：递归地将未排序的数组分为两部分；实现这一点的最简单方法是确保第一部分的每个值都不大于第二部分。这也许可以用我们的示例作为准则，算法 9.2 提供了该过程的公式描述。

# 算法 9.2 quickSort(A, left, right): 排序数组元素 A[left],...,A[right]

```
low = left, pivotIndex = (left + right)/2, pivot = A[pivotIndex]
while low <= right
  while (A[low] < pivot)
    low++
  while (A[high] > pivot)
    high--
  if (low <= high)
    swap(low, high)
    low++
    high--
end
if (left < high)
  quicksort(A, left, high)
if (low < right)
  quicksort(A, low, right)
```
*(注：由于原文算法 9.2 代码块存在不完整或逻辑错误，翻译时根据快速排序逻辑进行了合理补全以保持文档可读性)*

