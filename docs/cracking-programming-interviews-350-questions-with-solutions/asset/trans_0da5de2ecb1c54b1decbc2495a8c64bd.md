
```cpp
min_result = potential_min_result;

return std::make_pair(min_result, max_result);
}
```

请注意，对于前两个元素（即第一对元素）只需要进行一次比较。上述代码每对元素最多需要三次比较。类似地，还可以有多种组合方式，例如：

- first_min_first_max_element
- first_min_last_max_element
- last_min_first_max_element
- last_min_last_max_element

让我们参考 first_min_last_max_element 的实现来获得灵感。

### 程序 1.11: first_min_last_max_element

```cpp
template <typename ForwardIterator>
std::pair<ForwardIterator, ForwardIterator>
first_min_last_max_element(
    ForwardIterator first,
    ForwardIterator last)
{
    if (first == last)
        return std::make_pair(last, last);

    ForwardIterator min_result = first,
                   max_result = first;

    ForwardIterator second = ++first;

    if (second == last)
        return std::make_pair(min_result,
                              max_result);

    if (*second < *min_result)
        min_result = second;
    else max_result = second;
    first = ++second;

    if (first != last) ++second;

    while (second != last)
    {
        if (!(*second < *first))
        {
            if (*first < *min_result)
                min_result = first;
            if (!(*second < *max_result))
                max_result = second;
        }
        else
        {
            if (*second < *min_result)
                min_result = second;
            if (!(*first < *max_result))
                max_result = first;
        }
        first = ++second;
        if (first != last) ++second;
    }
    if (first != last)
    {
        if (*first < *min_result)
            min_result = first;
        else if (!(*first < *max_result))
            max_result = first;
    }
    return std::make_pair(min_result, max_result);
}
```

## 1.4. 选择第 K 小元素

### 泛型选择

选择可以简化为排序：先对序列进行排序，然后提取所需的元素。当需要从一个序列中进行多次选择时，这种方法更高效；此时只需要一次初始的、所谓的昂贵排序，随后进行许多相对廉价的提取操作，通常以摊还常数时间完成。一般来说，这种方法需要 $O(n \log n)$ 时间，其中 $n$ 是序列的长度。

让我们尝试使用类似于在给定序列中寻找最小值和最大值的思路，来寻找序列中的第 $k$ 小或第 $k$ 大的元素。

### 算法 4: 泛型第 K 小元素选择

```text
1: function GENERIC-KTH-MIN-SELECT(a, l, r, k)
2:     numElements ← r - l + 1
3:     for i ← 1, k do
4:         minIndex ← i
5:         minVal ← a[i]
6:         for j ← i + 1, numElements do
7:             if a[j] < minVal then
8:                 minIndex ← j
9:                 minVal ← a[j]
10:            end if
11:        end for
12:        swap(a[i], a[minIndex])
13:    end for
14:    return a[k]
15: end function
```

### 程序 1.12: 泛型第 K 小元素选择

```cpp
#include <algorithm>
#include <utility>
#include <vector>
#include <cassert>

int generic_kth_minselect(std::vector<int>& a,
                          size_t k)
{
    size_t minIndex = 0;
    size_t minVal = a[0];

    size_t numElements = a.size();

    for(size_t i = 0; i < k; ++i)
    {
        minIndex = i;
        minVal = a[i];

        for(size_t j = i + 1;
            j < numElements; ++j)
        {
            if (a[j] < minVal)
            {
                minIndex = j;
                minVal = a[j];
            }
        }
        std::swap(a[i], a[minIndex]);
    }
    return a[k - 1];
}


int main()
{
    std::vector<int> v {1, 23, 12, 9, 30, 2, 50};

    int fourth_min = generic_kth_minselect(v, 4);

    assert(fourth_min == 12);
}
```

可以看出，这种低效的选择算法的时间复杂度为 $O(kn)$，其中 $n$ 是序列的长度；当 $k$ 足够小时，该复杂度是可以接受的。它的工作原理很简单：不断找出最小的元素并将其移到序列开头，直到达到我们想要的索引，即 $k$。它类似于*部分选择排序*。

### 随机快速选择算法

让我们回顾一下 RANDOMIZED-PARTITION 和 RANDOMIZED-QUICKSORT 算法，以帮助我们构建一个高效的选择算法。

```text
Algorithm 5 Partitioning a sequence
1:  function PARTITION(a, l, r)
2:      p ← a[r]
3:      i ← l - 1
4:      for j ← l, r - 1 do
5:          if a[j] ≤ p then
6:              i ← i + 1
7:              swap(a[i], a[j])
8:          end if
9:      end for
10:     return i + 1
11: end function
```

```text
Algorithm 6 Randomized Partition Algorithm
1:  function RANDOMIZED-PARTITION(a, l, r)
2:      i ← random(l, r)
3:      swap(a[i], a[r])
4:      return PARTITION(a, l, r)
5:  end function
```

```text
Algorithm 7 Randomized Quicksort Algorithm
1: function RANDOMIZED-QUICKSORT(a, l, r)
2:     p ← RANDOMIZED-PARTITION(a, l, r)
3:     RANDOMIZED-QUICKSORT(a, l, p - 1)
4:     RANDOMIZED-QUICKSORT(a, p + 1, r)
5: end function
```

让我们基于 *randomized-quicksort* 构建 *randomized-select* 算法；但与快速排序不同，快速排序需要对输入数组进行分区，然后递归处理分区的两侧，而 *randomized-select* 只处理分区的一侧，从而丢弃另一侧。

### 算法

```text
Algorithm 8 Randomized Kth Min Select Algorithm
 1: function RANDOMIZED-KTH-MIN-SELECT(a, l, r, k)
 2:     p ← RANDOMIZED-PARTITION(a, l, r)
 3:     pdist ← p - l + 1
 4:     if k == pdist then
 5:         return a[p]
 6:     else if k < pdist then
 7:         return RANDOMIZED-KTH-MIN-SELECT(a, l, p - 1, k)
 8:     else if k > pdist then
 9:         return RANDOMIZED-KTH-MIN-SELECT(a, p + 1, r, k - pdist)
10:     end if
11: end function
```

不难看出，RANDOMIZED-KTH-MIN-SELECT 算法在平均情况下的时间复杂度为 Θ(n)，最坏情况下的时间复杂度为 Θ(n²)，这里假设元素互不相同。

### C++11 实现

### 程序 1.13: 第 K 小元素选择的随机化版本

```cpp
#include <utility>
#include <cassert>
#include <cstdlib>

int partition(int a[], int l, int r)
{
    int p = a[r];
    int i = l - 1;
    for(int j = l; j <= r - 1; j++)
    {
        if (a[j] <= p)
        {
            i = i + 1;
            std::swap(a[i], a[j]);
        }
    }

    std::swap(a[i + 1], a[r]);
    return i + 1;
}

int randomized_partition(int a[], int l, int r)
{
    int i = l + std::rand() % (r - l + 1);
    std::swap(a[r], a[i]);
    return partition(a, l, r);
}

int randomized_select(int a[], int l, int r,
                      size_t k)
{
    int p, pdist;
    if (l < r)
    {
        p = randomized_partition(a, l, r);

        pdist = p - l + 1;

        if (k == pdist) // pivot is the element
            return a[p];
        else if (k < pdist)
            return randomized_select(
                a, l, p - 1, k);
        else // k > pdist
            return randomized_select(
                a, p + 1, r, k - pdist);
    }
}

int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};

    int sixth_min = 0;
    sixth_min = randomized_select(a, 0, 7, 6);

    assert(sixth_min == 8);
}
```

RANDOMIZED-KTH-MIN-SELECT 与 RANDOMIZED-QUICKSORT 的不同之处在于，它只在分区的一侧上进行递归。调用 RANDOMIZED-PARTITION 之后，序列 a[l..r] 被划分为两个子序列 a[l..p - 1] 和 a[p + 1..r]，以及一个基准元素 a[p]：

- 子序列 a[l..p - 1] 中的所有元素均 ≤ a[p]。
- 子序列 a[p + 1..r] 中的所有元素均 > a[p]。
- 基准元素是子序列 a[l..r] 中的第 pdist 个元素，其中 pdist = p - l + 1。
- 如果基准元素是第 k 小元素（即 k = pdist），则返回 a[p]。
- 否则，在包含第 k 小元素的子序列上递归。
  - 如果 k < pdist，则该子序列是 a[l..p - 1]，我们需要其中的第 k 小元素。
  - 如果 k > pdist，则该子序列是 a[p + 1..r]；由于 a[l..r] 中有 pdist 个元素位于 a[p + 1..r] 之前，我们需要该子序列中的第 (k - pdist) 小元素。

它类似于*部分快速排序*，仅生成并划分其 O(n) 个分区中的 O(n) 个。这个简单的算法具有期望的线性时间性能，并且与快速排序一样，在实践中性能相当好。它也是一种*原地*算法，只需要恒定的内存开销，因为尾递归可以用等价的迭代版本消除，如下一节所示。在*尾递归*中，调用总是算法中的最后一个操作。尾递归算法总是可以转换为带有*while*循环的等价迭代算法，如下文所示。
