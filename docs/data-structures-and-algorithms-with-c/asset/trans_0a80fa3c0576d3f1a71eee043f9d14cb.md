

命名为归并排序。归并排序算法可以概括为包含以下三个步骤：

假设 A 是一个包含 N 个元素的数组，从 A[0] 到 A[N-1]。

- 1. 分解步骤：如果给定的数组 A 包含零个或一个元素，则返回，因为它已经是有序的。否则，将 A 分为两个子数组，A1 = A[0], A[1], ..., A[N/2-1] 和 A2 = A[N/2], A[N/2+1], ..., A[N-1]，每个子数组包含 A 中大约一半的元素。
- 2. 递归步骤：递归地对两个子数组 A1 和 A2 进行排序；
- 3. 合并步骤：通过将两个已排序的数组 A1 和 A2 合并为一个有序序列，将元素重新组合回 A 中。

示例：

输入数据：8, 6, 3, 5, 2, 7, 4 和 1。

![](img/723fa3ef35f5102eb67dc45b74bb823d_290_0.png)

![](img/723fa3ef35f5102eb67dc45b74bb823d_290_1.png)

图 10.116：(a) 分解阶段和 (b) 合并阶段

## 归并排序算法

```
Algorithm: MERGE_SORT(A, F, L)
[A is an array of N elements, F is the first position and L is the last position of the sub-array]
1. If F < L then
    a) Set MID = (F + L)/2
    b) Call MERGE_SORT(A, F, MID)
    c) Call MERGE_SORT(A, MID+1, L)
    d) Call MERGE(A, F, L, MID)
2. Return

Function: MERGE(A, F, L, MID)
[A is an array, F is the first position, L is the last position and MID is the middle position of the sub-array]
1. Set I = F, J = MID + 1, K = F
2. Repeat while I <= MID and J <= L
    If A[I] < A[J] then
    a) Set C[K] = A[I]
    b) Set I = I + 1
    c) Set K = K + 1
    ELSE
    a) Set C[K] = A[J]
    b) Set J = J + 1
    c) Set K = K + 1
    [End of IF]
    [End of Loop]
3. Repeat while I <= MID
    a) Set C[K] = A[I]
    b) Set I = I + 1
    c) Set K = K + 1
    [End of Loop]
4. Repeat while J <= L
    a) Set C[K] = A[J]
    b) Set J = J + 1
    c) Set K = K + 1
    [End of Loop]
5. Repeat for I = F to K
    Set A[I] = C[I]
6. Return
```

## MergeSort 的时间复杂度

最佳情况 / 最坏情况 / 平均情况时间复杂度：在归并排序中，分区始终是均衡的，大小相等，每个分区有 n/2 个元素。每个大小为 n/2 的子问题递归地对两个大小为 n/4 的子数组进行排序。有四个大小为 n/4 的子问题，每个子问题的合并时间为 cn/4，总合并时间为 4cn/4 = cn。子问题大小树及所有子问题的总合并时间如下图所示。

![](img/723fa3ef35f5102eb67dc45b74bb823d_292_0.png)

图 10.12：归并排序中的子程序大小

对于所有情况，比较次数总数可以递归计算

```
T (n) = \begin{cases} c, & \text{when n=1} \\ 2T (n/2) + cn, & \text{otherwise} \end{cases}
```

其中 c 是一个常数

现在，

```
T (n) = 2T (n/2) + cn
= 2 [2 T(n/4) + cn/2] + cn
= 2^2T (n/4) + cn+cn
= 2^2T (n/2^2) + 2cn
:
= 2^i T(n/2^i) + icn
```

现在，令 2^i = n，因此 i = log n

```
T (n) = nT (n/n) + cnlog n
= nT (1) + cnlog n
= c + cnlog n [hence T (1)=c]
= O (nlogn)
```

| 归并排序算法 | 最佳情况 | 平均情况 | 最坏情况 |
|---|---|---|---|
| | O(nlogn) | O(nlogn) | O(nlogn) |

## 归并排序的空间复杂度

归并排序的空间复杂度为 O(n + logn)，其中 n 用于辅助数组，logn 用于栈空间。

## 堆排序

堆排序是选择排序更高效、改进的版本。它同样通过确定列表中的最大元素，将其放置在列表末尾，然后继续处理其余列表来工作。堆排序是一种原地排序算法，但不是稳定排序。堆排序由 J. W. J. Williams 于 1964 年发明。

堆排序基于一种称为堆的数据结构，这是一种特殊的二叉树。回顾一下，在堆中，A[K] 的左子节点存储在 A[2*K]，右子节点存储在 A[2*K+1]。由于这种排序技术使用堆数据结构，因此命名为堆排序。

一旦数据列表被构建成最大堆，根节点保证是最大元素。当它被移除并放置在列表末尾时，堆会被重新排列，使剩余的最大元素移动到根节点。

创建堆的操作也称为 heapify，用于从数据项列表构建堆。现在，heapify 操作有两种变体：shift-up 和 shift-down。

shift-up 过程从空堆开始，然后依次将元素插入树中，并通过 shift-up 操作构建堆。在这里，堆的构建采用自顶向下的方法。在 shift-up 操作中，如果新插入的元素大于（最大堆）或小于（最小堆）其父节点，则需要与父节点交换。

### 示例

使用 shift-up 过程构建堆：60, 50, 30, 10, 80, 70, 20 和 40

### 插入 60：

![](img/723fa3ef35f5102eb67dc45b74bb823d_293_0.png)

### 插入 50：

![](img/723fa3ef35f5102eb67dc45b74bb823d_293_1.png)

### 插入 30：

![](img/723fa3ef35f5102eb67dc45b74bb823d_293_2.png)

### 插入 10：

![](img/723fa3ef35f5102eb67dc45b74bb823d_293_3.png)

### 插入 80：

![](img/723fa3ef35f5102eb67dc45b74bb823d_294_0.png)

(e)

现在，由于 80 大于其父节点 50，因此与父节点交换。

![](img/723fa3ef35f5102eb67dc45b74bb823d_294_1.png)

(f)

现在，再次 80 大于其父节点 60，因此与父节点交换。

![](img/723fa3ef35f5102eb67dc45b74bb823d_294_2.png)

(g)

### 插入 70：

![](img/723fa3ef35f5102eb67dc45b74bb823d_294_3.png)

(h)

现在，由于 70 大于其父节点 30，因此与父节点交换。

![](img/723fa3ef35f5102eb67dc45b74bb823d_295_0.png)

### 插入 20：

![](img/723fa3ef35f5102eb67dc45b74bb823d_295_1.png)

### 插入 40：

![](img/723fa3ef35f5102eb67dc45b74bb823d_295_2.png)

现在，由于 40 大于其父节点 10，因此与父节点交换。

![](img/723fa3ef35f5102eb67dc45b74bb823d_295_3.png)

图 10.13 (a-j)：使用 shift-up 创建最大堆

shift-down 过程将整个输入数组视为完全二叉树，但不是堆，并从最后一个非平凡子堆（即最后一个父节点）开始维护。在这里，堆的构建采用自底向上的方法，节点依次向下移动以建立堆属性。元素 A[N/2+1], A[N/2+2], ..., A[N] 没有子节点，每个元素都是大小为 1 的子堆。现在，对每个 I（其中 I = N/2, N/2-1, ..., 1）执行 shift-down 操作。A[I] 的两个子节点都是子堆的根，因此调用 shift-down 使 A[I] 成为其自身子堆的根。在 shift-down 操作中，如果某个子节点大于（最大堆）或小于（最小堆）其子节点，则需要与该子节点交换。

![](img/723fa3ef35f5102eb67dc45b74bb823d_296_0.png)

图 10.14：(a) 自底向上（Shift-Down），(b) 自顶向下（Shift-Up）。圆圈中的数字表示构建堆时所需的最大交换次数。

此 shift-down 版本比 shift-up 更高效，后者中插入操作被调用 N 次。请注意，对于 N/2 个元素，我们对根为 A[I] 且高度为 1 的子堆中的 N/4 个元素调用 shift-down。对于 N/8 个元素，我们对高度为 2 的子堆调用 shift-down，以此类推。在图 10.14 中，圆圈中的数字表示构建堆时所需的最大交换次数。shift-down 版本所需的交换次数少于 shift-up 版本。因此，通常使用 shift-down 版本来构建堆。

现在，堆排序算法可以分为两部分。假设 A 是一个包含 N 个元素的数组，从 A[1] 到 A[N]。

- i) 在第一步中，从 N 个数据项构建最大堆。结果，根 A[1] 是最大元素。
- ii) 在第二步中，
  - A[1] 和 A[N] 之间的交换。显然，最大元素在第 1 趟结束时被放置在数组的第 N 位置。将堆大小减一，并将新的第一个值 A[1] 下移到其适当位置以重建堆。
  - A[1] 和 A[N-1] 之间的交换。第二大元素在第 2 趟结束时被放置在数组的第 N-1 位置。将堆大小减一，并将新的第一个值 A[1] 下移到其适当位置以重建堆。
  - A[1] 和 A[N-2] 之间的交换。第三大元素在第 3 趟结束时被放置在数组的第 N-2 位置。将堆大小减一，并将新的第一个值 A[1] 下移到其适当位置以重建堆。
  - 最后，A[1] 和 A[2] 之间的交换。将堆大小减一，显然，最小元素在 A[1] 中。

因此，从 A[1] 到 A[N] 的 N 个元素的数组在 N-1 趟后排序完成。

