

![](img/be6359df08208122bec6fad1103de211_378_0.png)

图 12.11 优先队列可视化

从队首出队（或移除）。然而，与普通队列不同，在优先队列中，元素的逻辑顺序由其优先级决定。虽然高优先级元素被添加到队列的前部，但低优先级元素被添加到队列的后部。

从概念上讲，我们可以将优先队列视为图 12.11 所示的一袋优先级。在这个袋子里，你可以插入任意优先级，但只能取出值最高的一个。

虽然我们可以使用线性数组轻松实现优先队列，但首先应考虑将元素插入数组然后对其排序所需的时间。我们需要 O(n) 时间来插入一个元素，并且至少需要 O(n log n) 时间来对数组进行排序。因此，实现优先队列的更好方法是使用二叉堆，它允许以 O(log n) 时间对元素进行入队和出队操作。

## 12.2 二项堆

二项堆 h 是满足二项堆属性的二项树集合。首先，让我们讨论一下什么是二项树。

二项树是一种有序树，可以递归定义如下：

- 阶为 0 的二项树只有一个节点。
- 阶为 i 的二项树有一个根节点，其子节点分别是阶为 i-1、i-2、...、2、1 和 0 的二项树的根节点。
- 二项树 B_i 有 2^i 个节点。
- 二项树 B_i 的高度为 i。

请看图 12.12，它展示了几个不同阶数的二项树。我们可以从两个阶为 B_{i-1} 的二项树构造出二项树 B_i，方法是将它们链接在一起，使得其中一棵树的根节点成为另一棵树根节点的最左子节点。

![](img/be6359df08208122bec6fad1103de211_378_1.png)

图 12.12 二项树

二项堆 h 是满足以下属性的二项树集合：

- h 中的每个二项树都满足最小堆属性（即，一个节点的键要么大于等于其父节点的键）。
- 对于包括零阶在内的每个阶，可以有一个或零个二项树。

根据第一个属性，堆有序树的根节点包含树中最小的键。另一方面，第二个属性意味着，拥有 n 个节点的二项堆 H 最多包含 log (n + 1) 棵二项树。

### 12.2.1 二项堆的链式表示

二项堆 H 中的每个节点都有一个存储其值的 val 字段。此外，每个节点 n 都有以下指针：

- P[n] 指向 n 的父节点
- Child[n] 指向最左子节点
- Sibling[n] 指向 n 紧邻其右侧的兄弟节点

![](img/be6359df08208122bec6fad1103de211_379_0.png)

图 12.13 二项堆

如果 n 是根节点，则 P[n] = NULL。如果 n 没有子节点，则 Child[n] = NULL，如果 n 是其父节点的最右子节点，则 Sibling[n] = NULL。

除此之外，每个节点 n 都有一个存储 n 的子节点数量的 degree 字段。请看图 12.13 所示的二项堆。图 12.14 展示了其对应的链式表示。

![](img/be6359df08208122bec6fad1103de211_379_1.png)

图 12.14 图 12.13 所示二项树的链式表示

### 12.2.2 二项堆上的操作

在本节中，我们将讨论可以对二项堆执行的不同操作。

#### 创建新的二项堆

过程 Create_Binomial_Heap() 分配并返回一个对象 H，其中 Head[H] 设置为 NULL。该过程的运行时间为 O(1)。

#### 查找具有最小键的节点

过程 Min_Binomial_Heap() 返回指向二项堆 H 中具有最小值的节点的指针。Min_Binomial_Heap() 的算法如图 12.15 所示。

```
Min_Binomial_Heap(H)
Step 1: [INITIALIZATION] SET Y = NULL, X = Head[H] and Min = ∞
Step 2: REPEAT Steps 3 and 4 While X ≠ NULL
Step 3: If Val[X] < Min
        SET Min = Val[X]
        SET Y = X
[END OF IF]
Step 4: SET X = Sibling[X]
[END OF LOOP]
Step 5: RETURN Y
```

图 12.15 查找具有最小值节点的算法

我们已经讨论过二项堆是堆有序的；因此，特定二项树中具有最小值的节点将作为二项堆中的根节点出现。因此，Min_Binomial-Heap() 过程检查所有根节点。由于最多需要检查 log (n + 1) 个根节点，该过程的运行时间为 O(log n)。

**示例 12.4** 考虑下面给出的二项堆，看看该过程在这种情况下是如何工作的。

![](img/be6359df08208122bec6fad1103de211_380_0.png)

图 12.16 二项堆

#### 合并两个二项堆

合并两个二项堆的过程被其他操作用作子程序。Union_Binomial_Heap() 过程将根节点具有相同度数的二项树链接在一起。将根节点为 y 的 B_{k-1} 树链接到根节点为 z 的 B_{k-1} 树，使 z 成为 y 的父节点的算法如图 12.17 所示。

```
Link_Binomial-Tree(Y, Z)
Step 1: SET Parent[Y] = Z
Step 2: SET Sibling[Y] = Child[Z]
Step 3: SET Child[Z] = Y
Step 4: SET Degree[Z] = Degree[Z] + 1
Step 5: END
```

图 12.17 链接两个二项树的算法

Link_Binomial-Tree() 过程在 O(1) 时间内使 y 成为节点 z 子节点链表的新头节点。合并两个二项堆 H1 和 H2 的算法如图 12.18 所示。

```
Union_Binomial-Heap(H1, H2)
Step 1: SET H = Create_Binomial-Heap()
Step 2: SET Head[H] = Merge_Binomial-heap(H1, H2)
Step 3: Free the memory occupied by H1 and H2
Step 4: IF Head[H] = NULL, then RETURN H
Step 5: Make PTR = NULL, PRE = Head[H] and NEXT = Sibling[PTR]
Step 6: Repeat Step 7 while NEXT != NULL
Step 7: IF Degree[PTR] != Degree[NEXT] OR (Sibling[NEXT] != NULL AND Degree[Sibling[NEXT]] = Degree[PTR]), then SET Prev = PTR, PTR = NEXT ELSE IF Val[PTR] <= Val[NEXT], then SET Sibling[PTR] = Sibling[NEXT] Link_Binomial-Tree(NEXT, PTR) ELSE IF Prev = NULL, then Head[H] = NEXT ELSE Sibling[Prev] = NEXT Link_Binomial-Tree(PTR, NEXT) SET PTR = NEXT SET NEXT = Sibling[PTR]
Step 8: RETURN H
```

图 12.18 合并两个二项堆的算法

该算法会破坏堆 H1 和 H2 的原始表示。除了 Link_Binomial-Tree() 之外，它还使用另一个过程 Merge_Binomial-Heap()，该过程用于将 H1 和 H2 的根列表合并为一个按度数单调递增排序的单链表。

在该算法中，步骤 1 到 3 将二项堆 H1 和 H2 的根列表合并为一个根列表 H，使得 H1 和 H2 按递增度数严格排序。Merge_Binomial-Heap() 返回一个按单调递增度数排序的根列表 H。如果 H1 和 H2 的根列表中共有 m 个根节点，则 Merge_Binomial-Heap() 在 O(m) 时间内运行。该过程反复检查两个根列表头部的根节点，并将度数较低的根节点追加到输出根列表中，同时从其输入根列表中将其移除。

算法的步骤 4 检查堆 H 中是否至少有一个根节点。只有当 H 至少有一个根节点时，算法才会继续。在步骤 5 中，我们初始化三个指针：PTR 指向当前正在检查的根节点，PREV 指向根列表中 PTR 前面的根节点，next 指向根列表中 PTR 后面的根节点。

在步骤 6 中，我们有一个 while 循环，在每次迭代中，我们根据它们的度数以及可能 Sibling[NEXT] 的度数，决定是将 PTR 链接到 NEXT 还是将 next 链接到 PTR。

在步骤 7 中，我们检查两个条件。首先，如果 degree[PTR] != degree[NEXT]，即当 PTR 是某个二项树的根节点而 NEXT 是某个二项树的根节点（对于某个 j > 1），那么 PTR 和 NEXT 不会相互链接，但我们将指针在列表中向下移动一个位置。其次，我们检查 PTR 是否是三个度数相等的根节点中的第一个，即 degree[PTR] = degree[NEXT] = degree[Sibling[NEXT]]。在这种情况下，我们也只是通过写入 PREV = PTR, PTR = NEXT 将指针在列表中向下移动一个位置。

但是，如果上述 IF 条件不满足，那么出现的情况是 PTR 是两个度数相等的根节点中的第一个，即 degree[PTR] = degree[NEXT] != degree[Sibling[NEXT]]。在这种情况下，我们根据哪个键更小，将 PTR 与 NEXT 链接或将 NEXT 与 PTR 链接。当然，键较小的节点将在两个节点链接后成为根节点。

Union-Binomial-Heap() 的运行时间为 O(log n)，其中 n 是二项堆 H1 和 H2 中节点的总数。如果 H1 包含 n1 个节点，H2 包含 n2 个节点，那么 H1 最多包含 log(n1 + 1) 个根节点，H2 最多包含 log(n2 + 1) 个根节点，因此在调用 Merge_Binomial-Heap() 时，H 最多包含 (log n1 + log n2 + 2) <= 2(log n + 2) = O(log n) 个根节点。由于 n = n1 + n2，Merge_Binomial-Heap() 的执行时间为 O(log n)。while 循环的每次迭代耗时 O(1)，由于最多有 (log n1 + log n2 + 2) 次迭代，总时间因此为 O(log n)。

