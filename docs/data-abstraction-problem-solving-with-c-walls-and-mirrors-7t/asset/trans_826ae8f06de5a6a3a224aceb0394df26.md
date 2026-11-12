

![](img/288a0c22d14d2450c1e772f228f867b0_101_0.png)

- 2. 如果 \(S_1\) 包含 \(k-1\) 个值，则第 \(k^{th}\) 小的值必须是主元 \(p\)。这是基本情况；当 \(k = \text{pivotIndex} - \text{first} + 1\) 时发生。
- 3. 如果 \(S_1\) 包含少于 \(k-1\) 个值，则 anArray[first..last] 中第 \(k^{th}\) 小的值必须在 \(S_2\) 中。因为 \(S_1\) 包含 \(\text{pivotIndex} - \text{first}\) 个值，所以 anArray[first..last] 中第 \(k^{th}\) 小的值是 \(S_2\) 中第 \((k - (\text{pivotIndex} - \text{first} + 1))^{th}\) 小的值。当 \(k > \text{pivotIndex} - \text{first} + 1\) 时发生此情况。

递归定义可以总结此讨论。令

kSmall(k, anArray, first, last) = anArray[first..last] 中第 \(k^{th}\) 小的值

在选择主元值 \(p\) 并将 anArray[first..last] 划分为 \(S_1\) 和 \(S_2\) 后，有 kSmall(k, anArray, first, last) 等于

- * 当 k < pivotIndex - first + 1 时，kSmall(k, anArray, first, pivotIndex - 1)
- * 当 k = pivotIndex - first + 1 时，p
- * 当 k > pivotIndex - first + 1 时，kSmall(k - (pivotIndex - first + 1), anArray, pivotIndex + 1, last)

总存在一个主元，并且因为它既不属于 \(S_1\) 也不属于 \(S_2\)，所以每一步被搜索的数组段大小至少减少 1。因此，你最终将达到基本情况：所需的值是一个主元。高层伪代码解决方案如下。

anArray[first..last] 中第 \(k^{th}\) 小的值

```
// Returns the kth smallest value in anArray[first..last].
kSmall(k: integer, anArray: ArrayType,
       first: integer, last: integer): ValueType
    Choose a pivot value p from anArray[first..last]
    Partition the values of anArray[first..last] about p
    if (k < pivotIndex - first + 1)
        return kSmall(k, anArray, first, pivotIndex - 1)
    else if (k == pivotIndex - first + 1)
        return p
    else
        return kSmall(k - (pivotIndex - first + 1), anArray,
                      pivotIndex + 1, last)
```

此伪代码与 C++ 函数相差不大。剩下的唯一问题是如何选择主元值 \(p\) 以及如何围绕所选的 \(p\) 划分数组。对 \(p\) 的选择是任意的。数组中的任何 \(p\) 都可用，尽管选择的顺序会影响你多快达到基本情况。第 11 章给出了围绕 \(p\) 划分值的算法。在那里，你将看到如何将函数 kSmall 转换为排序算法。

## 2.5 组织数据

给定以某种方式组织的数据，你可能需要以另一种方式组织它。因此，你实际上会改变数据的某些方面，而不是例如简单地搜索它。本节的问题称为汉诺塔。虽然这个经典问题可能没有直接的实际应用，但我们考虑它是因为其解决方案很好地说明了递归的使用。

### 2.5.1 汉诺塔

很久很久以前，在遥远的东方——越南河内市——皇帝的智者去世了，去见他的祖先了。皇帝需要一位替代的智者。皇帝自己也是个相当聪明的人，他设计了一个谜题，宣布解开谜题的人可以担任智者一职。

![](img/288a0c22d14d2450c1e772f228f867b0_102_0.png)

皇帝的谜题由 n 个盘子（他没有说具体有多少个）和三根杆子组成：A（源杆）、B（目标杆）和 C（备用杆）。盘子大小不同，中间有孔，以便可以套在杆子上。由于重量很大，盘子只能放在比自己大的盘子之上。最初，所有盘子都在杆 A 上，如图 2-16a 所示。谜题是将盘子一个接一个地从杆 A 移到杆 B。在转移过程中，也可以使用杆 C，但同样，盘子只能放在比自己大的盘子之上。

由于智者一职众所周知是个差事，所以有很多申请人。学者和农民都把他们的解决方案呈给了皇帝。许多解决方案长达数千步，许多包含深层嵌套的循环和控制结构。“我看不懂这些步骤，”皇帝吼道。“一定有解决这个谜题的简单方法。”

果然如此。一位伟大的佛教僧人从山里出来见皇帝。“我的孩子，”他说，“这个谜题太简单了，几乎能自行解决！”皇帝的安保主管想把这个奇怪的人赶出去，但皇帝让他继续说下去。

“如果你只有一个盘子（即 n = 1），将其从杆 A 移到杆 B。”到目前为止还好，但即使是村里的傻瓜也能做对这一部分。“如果你有多个盘子（即 n > 1），只需”

- 1. 忽略底部的盘子，为 n − 1 个盘子解决问题，稍作修改：杆 C 是目标杆，杆 B 是备用杆。（参见图 2-16b。）

- 2. 做完这些后，n − 1 个盘子将在杆 C 上，最大的盘子将留在杆 A 上。因此，通过将大盘子从 A 移到 B 来解决 n = 1 的问题（回想一下，即使是村里的傻瓜也能做到）。（参见图 2-16c。）

- 3. 现在你要做的就是将 n − 1 个盘子从杆 C 移到杆 B：也就是说，以杆 C 为源杆、杆 B 为目标杆、杆 A 为备用杆来解决问题。
  （参见图 2-16d。）

沉默了片刻，最后皇帝不耐烦地说：“好吧，你到底要不要告诉我们你的解决方案？”僧人只是报以了了然的微笑，然后消失了。

皇帝显然不是递归思维者，但你应该意识到僧人的解决方案是完全正确的。解决方案的关键在于这样一个观察：通过解决三个更小的（就盘子数量而言）汉诺塔问题，可以解决 n 个盘子的汉诺塔问题。令 towers(count, source, destination, spare) 表示将 count 个盘子从源杆 source 移动到目标杆 destination，使用 spare 作为备用杆的问题。请注意，即使源杆上有超过 count 个盘子，这个定义也是有意义的；在这种情况下，你只关心最上面的 count 个盘子，忽略其他的。同样，在开始之前，目标杆和备用杆上可能已经有盘子；你也忽略这些盘子，只是只能将较小的盘子放在它们之上。

你可以这样重述皇帝的问题：从杆 A 上有 n 个盘子、杆 B 和 C 上没有盘子的初始状态开始，求解 towers(n, A, B, C)。你可以这样陈述僧人的解决方案：

### 步骤 1. 从初始状态开始——所有盘子都在杆 A 上——求解问题

```
towers(n - 1, A, C, B)
```

也就是说，忽略底部（最大的）盘子，将顶部的 n − 1 个盘子从杆 A 移到杆 C，使用杆 B 作为备用。完成后，最大的盘子将留在杆 A 上，所有其他盘子将在杆 C 上。

### 步骤 2. 现在，最大的盘子在杆 A 上，所有其他盘子在杆 C 上，求解问题

```
towers(1, A, B, C)
```

也就是说，将最大的盘子从杆 A 移到杆 B。由于这个盘子比备用杆 C 上已有的盘子大，你实际上无法使用备用杆。不过，幸运的是——而且显而易见的是——在这个基本情况下你不需要使用备用杆。完成后，最大的盘子将在杆 B 上，所有其他盘子将留在杆 C 上。

### 步骤 3. 最后，最大的盘子在杆 B 上，所有其他盘子在杆 C 上，求解问题

```
towers(n - 1, C, B, A)
```

也就是说，将 n − 1 个盘子从杆 C 移到杆 B，使用 A 作为备用。请注意，目标杆 B 上已经有最大的盘子，你忽略它。完成后，你就解决了原始问题：所有盘子都将在杆 B 上。

问题 towers(count, source, destination, spare) 有以下伪代码解决方案：

```
solveTowers(count, source, destination, spare)
if (count == 1)
    Move a disk directly from source to destination
else
    solveTowers(count - 1, source, spare, destination)
    solveTowers(1, source, destination, spare)
    solveTowers(count - 1, spare, destination, source)
}
```

这个递归解决方案遵循与你在本章前面看到的递归解决方案相同的基本模式：

- 1. 你通过解决其他汉诺塔问题来解决一个汉诺塔问题。
- 2. 这些其他汉诺塔问题比原始问题更小；它们需要移动的盘子更少。特别是，在每次递归调用中，盘子数量减少 1。
- 3. 当问题只有一个盘子时——即基本情况——解决方案可以直接轻松求解。
- 4. 问题变小的方式确保你将达到基本情况。

汉诺塔问题的解决方案满足递归解决方案的四个标准

求解汉诺塔问题需要你递归地求解许多更小的汉诺塔问题。

图 2-17 说明了求解三个盘子问题时产生的递归调用及其顺序。

三个盘子的解决方案

现在考虑此算法的 C++ 实现。请注意，由于大多数计算机没有手臂（在撰写本文时），该函数通过向人类提供指令来移动盘子。因此，表示杆子的参数类型为 char，相应的参数可以是 'A'、'B' 和 'C'。调用 solveTowers(3, 'A', 'B', 'C') 会产生以下输出：

```
Move top disk from pole A to pole B
Move top disk from pole A to pole C
Move top disk from pole B to pole C
Move top disk from pole A to pole B
Move top disk from pole C to pole A
Move top disk from pole C to pole B
Move top disk from pole A to pole B
```

### 图 2-17 solveTowers(3, A, B, C) 产生的递归调用顺序

![](img/288a0c22d14d2450c1e772f228f867b0_104_0.png)

