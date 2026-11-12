
- 等于，或
- 大于

这种树的高度对应于它所表示的算法在最坏情况下进行的比较次数，而这反过来又是该算法运行时间的一个下界。因此，对于任何解决前面章节中提到的螺母和螺栓问题的决策树，我们希望其高度 H 的下界为 Ω(n log n)。

首先，注意任何三叉树中的叶子数 L 必须满足 L ≤ 3^H。接下来，考虑下面这一类输入。

设螺母的输入数组 N 固定，由 n 个按递增排序的螺母组成，并考虑螺栓的每一种排列对应一个可能的输入。为了匹配螺母和螺栓，在这种情况下，我们的算法本质上必须对螺栓数组进行排序。

在我们的决策树中，如果这种类型的两个不同输入被映射到同一个叶节点，那么我们的算法将试图对这两个输入应用相同的螺栓相对于螺母的排列，由此可知，该算法无法为这两个输入都正确计算出匹配。

因此，我们必须将这 n! 个不同输入中的每一个都映射到一个不同的叶节点，即

$L \ge n!$

$\implies 3^H \ge n!$

$\implies H \ge \log_3 n!$

$\implies H = \Omega(n \log n)$

请注意，对数的底在复杂度中无关紧要，它只是一种常数，因此我们也忽略它。

特别地，至少需要 Ω(n log n) 次比较。这也是该问题任何随机化算法的期望比较次数的一个下界。

对随机快速排序进行简单修改即可表明，存在简单的随机化算法，其期望比较次数（以及运行时间）为 O(n log n)：

- 随机选择一个螺栓
- 将它与所有螺母比较
- 找到与它匹配的螺母，从而将螺母分成三部分：
    - 比该螺栓小的螺母
    - 与该螺栓恰好匹配的螺母
    - 比该螺栓大的螺母

- *随机化*

*确定性算法*是指在给定相同输入时总是以相同方式运行的算法：输入完全决定了该算法所执行的计算序列。

通常，当我们谈论一个算法的运行时间时，我们指的是最坏情况运行时间。它是在所有规模为某一值的问题上，该算法在该输入上的运行时间的最大值：

$T_{\text{worst-case}}(n) = \max_{X:|X|=n} T(X)$

在极少数情况下，我们也会关注最好情况运行时间：

$T_{\text{best-case}}(n) = \min_{X:|X|=n} T(X)$

因此，让我们试着理解*平均情况*的含义。平均情况运行时间最好定义为：在某一规模的所有输入 X 上，算法对 X 的运行时间的期望值：

$T_{\text{average-case}}(n) = E_{X:|X|=n}[T(X)] = \sum_{|X|=n} T(X)\Pr[X].$

另一方面，*随机化算法*的行为不仅基于输入，还基于若干随机选择。

同一个随机化算法在多次给定相同输入时，可能在每次调用中执行不同的计算。这意味着，除其他事项外，随机化算法在给定输入上的运行时间不再是固定的，而本身就是一个随机变量。

当我们分析随机化算法时，通常关注最坏情况期望运行时间。也就是说，我们考察每个输入的平均运行时间，然后在某一规模的所有输入上取最大值：

$T_{\text{worst-case expected}}(n) = \max_{X:|X|=n} E[T(X)].$

这里重要的是要注意，我们不对可能输入的概率分布做任何假设。所有随机性都在算法内部，而这是我们可以控制的。

假设我们要找到与某个特定螺栓匹配的螺母。显而易见的算法可以是：测试每一个螺母，直到找到匹配项。在最坏情况下，这恰好需要 *n − 1* 次测试。我们可能必须检查除一个之外的所有螺栓；如果检查到最后一个螺栓仍未找到匹配，我们就知道最后一个螺母就是我们要找的那个。

就这个算法的时间复杂度而言，该算法平均将查看大约 *n/2* 个螺母。

## 分区

到现在已经很清楚，这个算法的关键部分是*分区*步骤，正如它在*快速排序*中一样。因此，在我们进入*随机化部分*之前，让我们先过一遍*确定性版本*。

```text
Algorithm 69 Partitioning a sequence
1: function PARTITION(a, l, r)
2:     p ← a[r]
3:     i ← l − 1
4:     for j ← l, r − 1 do
5:         if a[j] ≤ p then
6:             i ← i + 1
7:             swap(a[i], a[j])
8:         end if
9:     end for
10:    return i + 1
11: end function
```

*分区*总是选择序列 a[l..r] 中的最后一个元素 a[r] 作为*枢轴*：分区元素。它将序列分成四个区域，其中一些可能为空。

**循环不变式：**

- ∀x ∈ a[l..i] : x ≤ *枢轴*
- ∀x ∈ a[i + 1..j − 1] : x ≥ *枢轴*
- a[r] = *枢轴*。

第四个区域是 a[j..r − 1]，尚待评估。*分区*的时间复杂度为 Θ(n)，其中 n = r − l + 1。

程序 6.8：C++ 中的分区

```cpp
#include <algorithm>
#include <cassert>

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

int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};
    int aref[] = {1, 4, 0, 3, 5, 8, 9, 6};

    int p = partition(a, 0, 7);

    assert(std::equal(std::begin(a),
                      std::end(a),
                      std::begin(aref)));

    assert(p == 4);
    assert(a[p] == 5);
}
```

### STL 风格分区

程序 6.9：STL 风格的分区实现

```cpp
#include <iostream>
#include <algorithm>

template <typename RandomIter>
RandomIter partition(RandomIter l,
                     RandomIter r)
{
    for (RandomIter j = l; j != r; j++)
    {
        if (*j <= *r)
        {
            std::iter_swap(l++, j);
        }
    }
    std::iter_swap(l, r);

    return l;
}

int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};

    int *p = partition(a, a + 7);

    std::cout << "Array after partition"
              << std::endl;

    for (auto e : a)
        std::cout << e << " ";

    std::cout << std::endl;

    std::cout << "partition index: "
              << std::distance(std::begin(a), p) << ","
              << " partitioning element: " << *p
              << std::endl;
}
```

输出如下：

```text
Array after partition
1 4 0 3 5 8 9 6
partition index: 4, partitioning element: 5
```

### std::partition

STL 还提供了分区算法的一个版本，如下所示：

程序 6.10：std::partition

```cpp
template <typename BidirectionalIterator,
          typename Predicate>
BidirectionalIterator
partition(BidirectionalIterator first,
          BidirectionalIterator last,
          Predicate pred)
{
    while (true)
    {
        while (true)
        {
            if (first == last)
                return first;
            if (!pred(*first))
                break;
            ++first;
        }
        do
        {
            if (first == last)
                return first;
            --last;
        } while (!pred(*last));
        std::iter_swap(first, last);
        ++first;
    }
}
```

它将范围 [first,last) 中满足谓词的所有元素放在所有不满足谓词的元素之前，并返回一个迭代器 i，使得对于范围 [first,i) 中的任意迭代器 j，pred(*j) != false，并且对于范围 [i,last) 中的任意迭代器 k，pred(*k) == false。时间复杂度至多为 (last − first) / 2 次交换。

## 快速排序

快速排序是一种基于分治的两步排序算法，用于对序列进行排序。

- **分解**：将序列 *a[l...r]* 分区为两个子序列 *a[l...p−1]* 和 *a[p+1...r]*，使得 *a[l...p−1]* 中的每个元素 ≤ *a[p]*，且 *a[p+1...r]* 中的每个元素 ≥ *a[p]*，即
  ∀x ∈ *a[l...p−1]* 且 ∀y ∈ *a[p+1,r]*：*x* ≤ *a[p]* ≤ *y*。
- 递归调用快速排序，以原地对得到的两个子序列进行排序，即 *a[l...p−1]* 和 *a[p+1,r]*。

```text
Algorithm 70 Quicksort to sort a sequence
1: function QUICKSORT(a, l, r)
2:     p ← PARTITION(a, l, r)
3:     QUICKSORT(a, l, p − 1)
4:     QUICKSORT(a, p + 1, r)
5: end function
```

很容易看出，快速排序的运行时间取决于序列的分区方式。

最坏情况下，分区（例如，当输入为有序序列时）将得到长度分别为 *n − 1* 和 0 的两个子序列。

$T(n) = T(n − 1) + \Theta(0) + \Theta(n) = T(n − 1) + \Theta(n) = \Theta(n^2)$

最好情况的分区每次都会得到大小几乎相等的子序列。

$T(n) = 2T(n/2) + \Theta(n) = \Theta(n \log n)$

QUICKSORT 的平均情况更接近最好情况而不是最坏情况。

为了更好地理解，让我们假设分区总是得到比例为 9:1 的子序列：

$T(n) = T(9n/10) + T(n/10) + \Theta(n) = \Theta(n \log n)$
