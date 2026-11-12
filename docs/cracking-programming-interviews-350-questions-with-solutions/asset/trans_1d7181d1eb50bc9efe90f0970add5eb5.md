
程序 6.11：C++ 中的快速排序

```cpp
#include <iostream>

void swap(int *a, int *b)
{
    int t;
    t = *a;
    *a = *b;
    *b = t;
}

int partition(int a[], int l, int r)
{
    int p = a[r];
    int i = l - 1;

    for(int j = l; j <= r - 1; j++)
    {
        if(a[j] <= p)
        {
            i = i + 1;
            swap(&a[i], &a[j]);
        }
    }
    swap(&a[i + 1], &a[r]);

    return i + 1;
}


void quicksort(int a[], int l, int r)
{
    int p;
    if(l < r)
    {
        p = partition(a, l, r);
        quicksort(a, l, p - 1);
        quicksort(a, p + 1, r);
    }
}


int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};

    quicksort(a, 0, 7);

    std::cout << "Array after sorting"
              << std::endl;

    for(auto e : a)
        std::cout << e << " ";

    std::cout << std::endl;
}
```

输出如下：

| 排序后的数组 |
|---|
| 0 1 3 4 5 6 8 9 |

## STL 风格的快速排序

程序 6.12：快速排序的 STL 风格实现

```cpp
#include <iostream>
#include <algorithm>

template <typename RandomIter>
void quicksort(RandomIter first,
               RandomIter last)
{
    RandomIter left = first, right = last,
               pivot = left++;
    if( first != last )
    {
        while(left != right)
        {
            if(*left < *pivot)
            {
                ++left;
            }
            else
            {
                while((left != right)
                      && (*pivot < *right))
                    --right;
                std::iter_swap(left, right);
            }
        }
        --left;
        std::iter_swap(pivot, left);
        quicksort(first, left);
        quicksort(right, last);
    }
}
int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};
    quicksort(a, a + 7);

    std::cout << "Array after sorting"
              << std::endl;

    for (auto e : a)
      std::cout << e << " ";

    std::cout << std::endl;
}
```

## 使用 std::partition 的快速排序

程序 6.13：实现快速排序

```cpp
#include <algorithm>
#include <iterator>

template <typename RandomAccessIterator>
void quicksort(RandomAccessIterator begin,
               RandomAccessIterator end)
{
    if (begin != end)
    {
        RandomAccessIterator pivot =
            std::partition(begin, end, bind2nd(
                std::less<typename std::iterator_traits<
                RandomAccessIterator>::value_type>(), *begin));

        quicksort(begin, pivot);
        RandomAccessIterator new_pivot = begin;
        quicksort(++new_pivot, end);
    }
}
```

## 随机化快速排序

到目前为止，我们假设所有输入排列都是等可能的，而这并不总是成立，因此我们向快速排序加入随机化。我们可以随机打乱输入序列，但随机化快速排序采用随机采样，即随机选择元素来实现这一点。因此，不是选取 a[l] 的最后一个元素作为枢轴，而是从序列中随机选取枢轴。

算法 71 随机化划分算法

| 行 | 伪代码 |
|---:|---|
| 1 | `function RANDOMIZED-PARTITION(a, l, r)` |
| 2 | `i ← random(l, r)` |
| 3 | `swap(a[p], a[r])` |
| 4 | `return PARTITION(a, l, r)` |
| 5 | `end function` |

程序 6.14：C++ 中的随机化划分

```cpp
#include <iostream>

void swap(int *a, int *b)
{
    int t;
    t = *a;
    *a = *b;
    *b = t;
}

int partition(int a[], int l, int r)
{
    int p = a[r];
    int i = l - 1;

    for(int j = l; j <= r - 1; j++)
    {
        if(a[j] <= p)
        {
            i = i + 1;
            swap(&a[i], &a[j]);
        }
    }

    swap(&a[i + 1], &a[r]);

    return i + 1;
}

int randomized_partition(int a[], int l, int r)
{
    int p = l + std::rand() % (r - l + 1);
    swap(&a[r], &a[p]);
    return partition(a, l, r);
}

int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};

    int p = randomized_partition(a, 0, 7);

    std::cout <<
    "Array after randomized_partition"
    << std::endl;

    for(auto e : a)
    std::cout << e << " ";

    std::cout << std::endl;
    std::cout
    << "partition_index : " << p << ","
    << "partitioning_element: "
    << a[p] << std::endl;
}
```

该程序的输出为：

```text
Array after randomized partition
1 4 0 3 5 8 9 6
partition index : 4, partitioning element : 5
```

随机选择枢轴元素平均而言会使划分后的子序列相当均衡。

算法 72 随机化快速排序算法

1. `function RANDOMIZED-QUICKSORT(a, l, r)`
2. `p ← RANDOMIZED-PARTITION(a, l, r)`
3. `RANDOMIZED-QUICKSORT(a, l, p − 1)`
4. `RANDOMIZED-QUICKSORT(a, p + 1, r)`
5. `end function`

快速排序的随机化可阻止任何特定类型的序列导致最坏情况行为。例如，已排序的数组会在非随机化快速排序中导致最坏情况行为，但在随机化快速排序中不会。

在递归的每一层，由 RANDOMIZED-PARTITION 得到的划分将任意常数比例的元素放在划分的一侧，于是递归树的深度为 θ(log n)，并且每一层执行 O(n) 的工作。即使我们在这些层级之间加入尽可能最不平衡划分的深度层级，总时间仍保持 O(n log n)。

我们可以先理解划分过程如何运作，然后利用这种理解推导出期望运行时间的 O(n log n) 界，从而精确分析 RANDOMIZED-QUICKSORT 的期望运行时间。这个期望运行时间的上界，结合我们之前看到的 θ(n log n) 最佳情况界，得出 Θ(n log n) 的期望运行时间。

因此，随机化快速排序的时间复杂度为 O(n log n)。

程序 6.15：C++ 中的随机化快速排序

```cpp
#include <iostream>

void swap(int *a, int *b)
{
    int t;
    t = *a;
    *a = *b;
    *b = t;
}

int partition(int a[], int l, int r)
{
    int p = a[r];
    int i = l - 1;

    for (int j = l; j <= r - 1; j++)
    {
        if (a[j] <= p)
        {
            i = i + 1;
            swap(&a[i], &a[j]);
        }
    }

    swap(&a[i + 1], &a[r]);

    return i + 1;
}

int randomized_partition(int a[], int l,
                         int r)
{
    int j = l + std::rand() % (r - l + 1);
    swap(&a[r], &a[j]);
    return partition(a, l, r);
}

void randomized_quicksort(int a[], int l,
                          int r)
{
    int p;
    if(l < r)
    {
        p = randomized_partition(a, l, r);
        randomized_quicksort(a, l, p - 1);
        randomized_quicksort(a, p + 1, r);
    }
}

int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};
    randomized_quicksort(a, 0, 7);

    std::cout << "Array after sorting"
              << std::endl;

    for(auto e : a)
      std::cout << e << " ";

    std::cout << std::endl;
}
```

该程序的输出为：

```text
Array after sorting
0 1 3 4 5 6 8 9
```

## 螺母与螺栓问题的确定性算法

遗憾的是，为螺母与螺栓问题找到高效的确定性算法似乎要困难得多。首个 O(n log(log n)) 时间的确定性算法由 Alon 等人 [?] 提出，它同样基于快速排序，耗时 Θ(n log⁴ n)。为了找到一个良好的枢轴元素，将问题划分为两个规模几乎相同的子问题，他们运行一个过程的 log n 次迭代；该过程在每次迭代中淘汰一半的螺母，同时保持至少一个良好的枢轴：由于最后只剩一个螺母，因此这个螺母必定是良好的枢轴。该过程使用度为 Θ(log² n) 的高效扩展器的边来定义其比较。因此，找到一个良好的枢轴需要 Θ(n log³ n) 时间，而整个快速排序需要 Θ(n log⁴ n) 时间。Alon 等人 [?] 提到了螺母与螺栓问题的两个潜在应用：

1. 给定图中节点的局部排序
2. 带有少量读写内存的只读存储器的选择

Phillip G. Bradford 给出了一个简单的确定性算法 [?]，用于解决螺母与螺栓问题，该算法进行 O(n log n) 次螺母与螺栓比较。该算法基于某些基于扩展器的比较器网络，并证明了存在一棵深度为 O(n log n) 的决策树可以解决此问题。他们通过证明对于螺母与螺栓存在作为 ε − 半化器的比较器网络来做到这一点。一个 ε − 半化器以 O(n) 的复杂度近似划分一个含 n 个元素的集合。这种近似划分足以使该算法在几何级缩小的螺母与螺栓集合上迭代 ε − 半化器时选择良好的枢轴。构建这些 ε − 半化器的难点在于：在保持 ε − 半化性质的同时，确保螺母从不与螺母比较，螺栓从不与螺栓比较。设 S = s₁, …, sₙ 是一组不同尺寸的螺母，B = b₁, …, bₙ 是一组对应的螺栓。对于螺母 s ∈ S，定义 rank(s) 为 |{t ∈ B|s ≥ t}|。螺栓的秩为
