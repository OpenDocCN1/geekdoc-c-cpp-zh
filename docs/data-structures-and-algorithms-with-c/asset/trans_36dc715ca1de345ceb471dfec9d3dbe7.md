

黑色方块代表障碍物。开发一个算法，使老鼠能够通过对角退出迷宫。清楚地解释迷宫的表示方法以及用于算法的任何特定数据结构。

*****

## SEARCHING AND SORTING

> "当你学习时，你以为你知道；当你能写出来时，更加确定；当你能教别人时，更加确定；但只有当你能编程时，才真正确定。" -Alan J. Perlis

### KEY FEATURES

- 线性搜索
- 二分搜索
- 插值搜索
- 冒泡排序
- 选择排序
- 插入排序
- 快速排序
- 归并排序
- 希尔排序
- 堆排序

搜索项目和对项目进行排序是我们每天都要做的任务。我们在文件中搜索单词的所有出现位置，以便用另一个单词替换它。我们将列表中的项目按字母顺序或数字顺序排序。搜索和排序也是计算机程序中最常见的操作。

### SEARCHING

搜索是指在某些数据结构中查找所需键元素位置的操作。数据结构可以包括链表、数组、搜索树或哈希表。如果找到项目，则搜索成功，并返回其位置；否则，搜索不成功。合适的搜索算法通常取决于正在搜索的数据结构。

- 线性搜索
- 二分搜索
- 插值搜索

#### Linear Search

线性搜索，或顺序搜索，是一种在列表中查找特定键值位置的方法，搜索从列表开头开始，按顺序逐个检查每个元素，直到找到所需键或到达列表末尾。

##### Algorithm of Linear Search

```
Algorithm: LINEAR_SEARCH (A, N, KEY, LOC)
{A is an array of N elements, Key is the searching key}
1. Set I = 0
2. Repeat while I < N and A[I] != KEY
   Set I = I + 1
   [End of loop]
3. If I < N then Set LOC = I
   ELSE LOC = -1
4. Return
```

线性搜索是最简单的搜索技术。假设 A 是一个包含 N 个元素的数组，从 A[0] 到 A[N–1]。查找 KEY 项目的线性搜索算法如下执行。

首先，算法将 KEY 与列表的第一个元素 A[0] 进行比较。如果 KEY = A[0]，则搜索成功并返回位置。否则，将 KEY 与第二个元素 A[1]、第三个元素 A[2] 等进行比较，直到找到 KEY 或到达列表末尾。最后，在搜索成功后，通过引用返回 KEY 的位置；否则，在搜索不成功的情况下返回 -1。

现在，对于不成功的搜索，最坏情况下总共需要 2n 次比较，但对于最佳情况，只需两次。可以使用哨兵元素来减少比较次数。单词 sentinel 源自 sentry（意为卫兵）。额外的内存位置用于哨兵元素。开始时，将搜索键作为哨兵放在列表末尾（A[N] = KEY），在有效数组区域之外。现在成功有保证，但需要检查成功发生的时间。当搜索键在第 N 个位置找到时，实际上是不成功的搜索。否则，键在第 i 个位置找到。

##### Algorithm of Modified Linear Search

```
Algorithm: LINEAR_SEARCH (A, N, KEY, LOC)
[A is an array of N elements, Key is the searching key, LOC is the location of the KEY]
1. Set A[N] = KEY
2. Set I = 0
3. Repeat while A[I] != KEY
   Set I = I + 1
   [End of loop]
4. If I < N then Set LOC = I
   ELSE Set LOC = -1
5. Return
```

因此，在修改后的算法中，最坏情况下的比较次数变为 n+1，而不是 2n。元素可以在第 N 个位置找到不成功搜索的最坏情况，因此不需要数组边界检查。

##### Time complexity of Linear Search

线性搜索在最坏情况下运行时间最长，因为它最多进行 n 次比较，其中 n 是列表的长度。在平均情况下，比较次数由所有可能实例的平均值计算得出：

```
f(n) = [1 + 2 + 3 + ... + (n–1)] / n = 1/n Σ(i=1 to n-1) i = (n(n–1)/2) / n = (n–1)/2 = O(n)
```

最佳情况发生在键在第一个位置找到时，只需要一次比较；最坏情况发生在键在最后一个位置找到时，因此需要 n+1 次比较。

| 线性搜索算法 | 最佳情况 | 平均情况 | 最坏情况 |
|---|---|---|---|
| | O(1) | O(n) | O(n) |

### Binary Search

二分搜索是一种在有序列表上运行的高效搜索技术。二分搜索也称为对数搜索或二分法。二分搜索或半区间搜索算法是在有序列表中查找特定键值位置的一种方法。

假设 A 是一个按升序排序的数组。变量 I 和 J 分别表示数组的第一个和最后一个位置。现在使用二分搜索在有序列表中查找 KEY 项目：

```
A[J], A[I + 1], A[I + 2]...A[J - 1], A[J]
```

二分搜索算法如下执行：

首先，算法将 KEY 与列表的中间元素 A(MID) 进行比较，其中 MID 通过 MID = (I + J) / 2 得到。如果 KEY = A(MID)，则搜索成功并返回位置。否则，子数组如下获得：

- i) 如果 KEY < A(MID)，则 KEY 元素只能出现在数组的下半部分：A[I], A[I + 1], A[I + 2]...A[MID - 2], A[MID - 1]。因此，我们使用 J = MID - 1 重置 J 的值，并开始搜索数组的下半部分。
- ii) 如果 KEY > A(MID)，则 KEY 项目只能出现在数组的上半部分：A[MID + 1], A[MID + 2], A[MID + 3]...A[J - 1], A[J]。因此，我们使用 I = MID+1 重置 I 的值，并开始搜索数组的上半部分。

最后，在搜索成功后，通过引用返回 KEY 的位置；否则，在搜索不成功的情况下返回 -1。

#### Example:

我们要搜索 31

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] |
|---|---|---|---|---|---|---|---|---|
| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 |

(a)

首先，我们将使用以下公式确定数组的中间位置：

```
MID = (I + J) / 2 = (0 + 8) / 2 = 4
```

观察到要搜索的值大于 A[MID] = 27，其中 MID = 4。

由于该值大于 27，因此搜索区域在区域的上半部分。

| [5] | [6] | [7] | [8] |
|---|---|---|---|
| 31 | 33 | 35 | 42 |

(b)

现在，修改子数组的起始索引：

```
I = MID + 1 = 4 + 1 = 5
```

```
MID = (I + J) / 2 = (5 + 8) / 2 = 6
```

目标值是 31，小于 A[MID] = 33，因此搜索区域将在 MID 的左侧，其中 J = MID - 1 = 6 - 1 = 5

#### Figure 10.1 (a-c): Binary Search

现在，MID = (I + J) / 2 = (5 + 5) / 2 = 5

项目在 A[MID] 处找到。在此，搜索过程成功结束。

#### Algorithm of Binary Search

```
Algorithm: BINARY_SEARCH (A, N, KEY, LOC)
[A is an array of N elements, Key is the searching key, LOC is the location of the KEY]
1. Set I = 0, J = N-1
2. Repeat steps 3 and 4 while I<=J
3. MID = (I+J) / 2
4. If KEY = A[MID] then Goto step 5
   Else If KEY < A[MID] Then Set J = MID-1
   Else Set I = MID+1
   [End of If]
   [End of Loop]
5. If A[MID] = KEY then Set LOC = MID
   Else Set LOC = -1
   [End of If]
6. Return
```

#### Time complexity of Binary Search

在二分搜索中，每次迭代后，我们尝试丢弃数组的一半元素。假设数组大小为 10，且 A[0] ≤ A[1] ≤ A[2] ≤ A[3] ≤ A[4] ≤ A[5] ≤ A[6] ≤ A[7] ≤ A[8] ≤ A[9]

最初 I = 0 且 J = 9，因此 MID = (I+J)/2 = 4

![](img/723fa3ef35f5102eb67dc45b74bb823d_273_0.png)

#### Figure 10.2: Comparison Tree for Binary Search

| 键元素等于 | A[0] | A[1] | A[2] | A[3] | A[4] | A[5] | A[6] | A[7] | A[8] | A[9] |
|---|---|---|---|---|---|---|---|---|---|---|
| 比较次数 | 3 | 2 | 3 | 4 | 1 | 3 | 4 | 2 | 3 | 4 |

平均情况 = 29/10 = 3（约数），最坏情况 = 4

最坏情况时间复杂度。在最坏情况下，比较的总次数可以递归计算：

```
T (n) = {
 c, when n=1
 T (n/2) + c, Otherwise
}
```

其中 c 是常数

现在，

```
T (n) = T (n/2) + c
 = [T (n/4) + c] + c
 = T (n/4) + 2c
 :
 = T (n/2^r) + rc
 = T (n/n) + c log n [when 2^r = n then r = log n]
 = T (1) + c log n [hence T (1)=c]
 = c + c log n
 = c[1 + log n]
 = O (log n)
```

在 log n + 1 最坏情况下的比较次数是二叉树的深度或高度。平均情况下的比较次数大约等于最坏情况下的比较次数。最佳情况发生在键在第一次比较时找到。

| 二分搜索算法 | 最佳情况 | 平均情况 | 最坏情况 |
|---|---|---|---|
| | O(1) | O(log n) | O(log n) |

#### Table 10.1: Differences between Linear Searching and Binary Searching

| 线性搜索 | 二分搜索 |
|---|---|
| 线性搜索在已排序和未排序的项目列表上执行。 | 二分搜索仅在已排序列表上执行。 |
| 线性搜索与数组和链表一起执行。 | 二分搜索仅与数组一起执行，不与链表一起执行。 |
| 在平均情况下，需要更多的比较。 | 平均情况下的比较较少。 |
| 平均情况和最坏情况的复杂度为 O(n) | 平均情况和最坏情况的复杂度为 O(log n) |

#### Limitation of the Binary Searching algorithm

该算法需要两个条件：

- 1. 列表必须已排序
- 2. 必须能够直接访问中间元素

