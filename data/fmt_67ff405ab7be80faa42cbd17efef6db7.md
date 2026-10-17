
栈还类似于食堂里的弹簧压力栈。如果你向栈中添加盘子，弹簧会压缩，使得顶部的盘子与桌面齐平。如果你移除一个盘子，弹簧会展开，使得现在顶部的盘子仍然与桌面齐平。图 5-1 显示了这种栈。

![](img/fefa42765c0b410af6705110aea7c0cb_135_0.png)

由于这种栈会将盘子向下推入桌面，这种数据结构有时也被称为压栈（pushdown stack）。向栈中添加对象被称为“推入”（push），从栈中移除对象被称为“弹出”（pop）。栈类通常提供 `Push` 和 `Pop` 方法来向栈中添加项目和移除项目。

接下来的章节描述了实现栈的几种较为常用的方法。

## 链表栈

使用链表实现栈是非常简单的。`Push` 方法简单地在列表顶部添加一个新单元格，而 `Pop` 方法则从列表中移除顶部的单元格。

以下伪代码显示了向链表栈推入项的算法：

```
Push(Cell: sentinel, Data: new_value)
  // 创建一个单元来存储新值。
  Cell: new_cell = New Cell
  new_cell.Value = new_value

  // 将新单元格加入链表。
  new_cell.Next = sentinel.Next
  sentinel.Next = new_cell
End Push
```

以下伪代码显示了从链表栈中弹出项的算法：

```
Data: Pop(Cell: sentinel)
  // 确保有项可以弹出。
  If (sentinel.Next == null) Then <throw an exception>

  // 获取顶部单元格的值。
  Data: result = sentinel.Next.Value

  // 从链表中移除顶部的单元格。
  sentinel.Next = sentinel.Next.Next

  // 返回结果。
  Return result
End Pop
```

图 5-2 显示了该过程。顶部的图像显示程序向栈推入字母 A、P、L、E 后的栈状态。中间的图像显示新字母 S 推入栈之后的状态。底部的图像显示在 S 弹出后栈的状态。

![](img/fefa42765c0b410af6705110aea7c0cb_136_0.png)

图 5-2: 使用链表构建栈非常简单。

> 注意：请参阅第 3 章获取更多关于使用链表的详细信息。

使用链表，推入和弹出项的运行时间均为 O(1)，因此这两个操作都非常快。该列表除了单元格之间的链接外，不需要额外存储，因此链表也是空间高效率的。

## 数组栈

在数组中实现栈几乎与使用链表实现一样简单。为数组分配空间，使其足够大以容纳你预期放入栈中的项目数量。使用一个变量来跟踪栈中下一个空位置。

以下伪代码显示了向基于数组的栈推入项的算法：

```
Push(Data: stack_values [], Integer: next_index, Data: new_value)
  // 确保有空间添加项。
  If (next_index == <length of stack_values>) Then <throw an exception>

  // 添加新项。
  stack_values[next_index] = new_value

  // 递增 next_index。
  next_index = next_index + 1
End Push
```

以下伪代码显示了从基于数组的栈中弹出项的算法：

```
Pop(Data: stack_values[], Integer: next_index)
  // 确保有项可以弹出。
  If (next_index == 0) Then <throw an exception>

  // 递减 next_index。
  next_index = next_index - 1

  // 返回结果。
  Return stack_values[next_index]
End Pop
```

图 5-3 显示了程序向栈推入字母 A、P、L、E 后的栈状态。中间的图像显示字母 S 推入栈之后的状态。底部的图像显示在 S 弹出后栈的状态。

![](img/fefa42765c0b410af6705110aea7c0cb_138_0.png)

图 5-3: 使用数组构建栈非常简单。

## 双栈

假设某个算法需要两个总大小受限的栈。在这种情况下，你可以将两个栈存储在同一个数组中，分别从两端开始向中间生长，如图 5-4 所示。

![](img/fefa42765c0b410af6705110aea7c0cb_138_1.png)

图 5-4: 两个栈共享一个数组。

以下伪代码显示了在单个数组中两个栈的推入和弹出算法。为了使算法更简单，数组以及 `NextIndex1` 和 `NextIndex2` 变量被存储在 Push 方法之外：

```
Data: StackValues(<max items>)
Integer: NextIndex1, NextIndex2

// 初始化数组。
Initialize()
NextIndex1 = 0
NextIndex2 = <length of StackValues> - 1
End Initialize

// 向顶部栈推入项。
Push(Data: new_value)
  // 确保有空间添加项。
  If (NextIndex1 > NextIndex2) Then <throw an exception>

  // 添加新项。
  StackValues[NextIndex1] = new_value

  // 递增 NextIndex1。
  NextIndex1 = NextIndex1 + 1
End Push

// 向底部栈推入项。
Push2(Data: new_value)
  // 确保有空间添加项。
  If (NextIndex1 > NextIndex2) Then <throw an exception>

  // 添加新项。
  StackValues[NextIndex2] = new_value

  // 递减 NextIndex2。
  NextIndex2 = NextIndex2 - 1
End Push2

// 从顶部栈弹出项。
Pop()
  // 确保有项可以弹出。
  If (NextIndex1 == 0) Then <throw an exception>

  // 递减 NextIndex1。
  NextIndex1 = NextIndex1 - 1

  // 返回顶部值。
  Return StackValues[NextIndex1]
End Pop

// 从底部栈弹出项。
Pop2()
  // 确保有项可以弹出。
  If (NextIndex2 == <length of StackValues> - 1) Then <throw an exception>

  // 递增 NextIndex2。
  NextIndex2 = NextIndex2 + 1

  // 返回底部值。
  Return StackValues[NextIndex2]
End Pop2
```

# 第5章 - 栈与队列

## 栈算法

许多算法都使用栈。例如，第13章中描述的某些最短路径算法可以使用栈。接下来的章节描述了你可以使用栈实现的其他一些算法。

### 反转数组

使用栈反转数组非常简单。只需将每个元素推入栈中，然后将其依次弹出。由于栈的后进先出（LIFO）特性，元素返回的顺序将反相反。

以下伪代码展示了该算法：

```
ReverseArray(Data: values[])
  // 将数组中的值推入栈。
  Stack: stack = New Stack
  For i = 0 To <length of values> - 1
    stack.Push(values[i])
Next i
```

```
// 将元素从栈弹出并放入数组。
  For i = 0 To <length of values> - 1
    values[i] = stack.Pop()
Next i
EndReverseArray
```

如果数组包含N个元素，该算法需要2 × N步操作，因此其运行复杂度为 O(N)。

### 火车排序

假设有一列火车包含开往不同目的地的车厢，它进入了一个调度场。在火车离开调度场之前，你需要使用轨道对车厢进行排序，以便去往同一目的地的车厢分组。

图5-5显示了一列从左输入轨道进入城市3、2、1、3和2的火车。火车可以移动到临时轨道，并将其最右侧的车厢移动到该临时轨道上任意车辆的左侧。稍后，火车可以返回临时轨道，将临时轨道左端的车厢移回火车的右端。目标是对比车厢进行排序。

![](img/fefa42765c0b410af6705110aea7c0cb_141_0.png)

**图5-5**：你可以使用栈来模拟真实的调度场火车排序。

你可以直接使用栈来模拟这种情况。一个栈代表进入的火车。它的 `Pop` 方法移除火车右侧的一节车厢，它的 `Push` 方法将一节车厢移回火车右端。

其他栈代表临时轨道和输出轨道。它们的 `Push` 方法代表将车厢移到轨道的左端，`Pop` 方法代表将车厢从轨道的左端移走。

以下伪代码展示了程序如何使用栈来对图5-5所示的火车排序。这里*train*在输入轨道上，*track1*和*track2*是上方和方的临时轨道，而*output*是输出轨道：

```
holding1.Push(train.Pop()) // 第1步：车厢2移到临时轨道1。
holding2.Push(train.Pop()) // 第2步：车厢3移到临时轨道2。
output.Push(train.Pop()) // 第3步：车厢1移到输出。
holding1.Push(train.Pop()) // 第4步：车厢2移到临时轨道1。
train.Push(holding2.Pop()) // 第5步：车厢3移回火车。
train.Push(holding1.Pop()) // 第6步：车厢2移回火车。
train.Push(holding1.Pop()) // 第7步：车厢2移回火车。
train.Push(output.Pop()) // 第8步：车厢1移回火车。
```

图5-6展示了这一过程。每一步中移动的车厢都有边框。箭头显示了每节车厢的移动方向。

当然，在真实的调度场中，每次移动都需要调整火车车厢，可能需要几分钟时间。因此，找到移动次数最少的解决方案是非常重要的。

![](img/fefa42765c0b410af6705110aea7c0cb_142_0.png)

**图5-6**：通过使用两个临时轨道和一个输出轨道，你可以八步内完成这列火车的排序。

### 汉诺塔

汉诺塔游戏如图5-7所示，有三个柱。一根柱上放着一叠大小不同的盘，按从小到大的顺序。你每次移动一个盘从一个柱移动到另一个柱，目标是按大小将所有盘重新堆叠在另一个柱上。你不能将盘放在半径较小的另一个盘之上。

![](img/fefa42765c0b410af6705110aea7c0cb_142_1.png)

**图5-7**：汉诺塔游戏的目标是将盘从一根柱重新堆叠到另一根柱，而不将盘放在小盘之上。

你可以用非常明显的方式使用三个栈来模拟这个游戏。每个栈代表一根柱。你可以使用代表盘半径的数字作为栈中的对象。

以下伪代码展示了程序如何使用栈来模拟将盘从左柱移动到中间柱：

```
peg2.Push(peg1.Pop())
peg3.Push(peg1.Pop())
peg2.Push(peg3.Pop())
peg1.Push(peg2.Pop())
peg3.Push(peg2.Pop())
peg2.Push(peg3.Pop())
peg1.Push(peg2.Pop())
```

![](img/fefa42765c0b410af6705110aea7c0cb_143_0.png)

**图5-7**：汉诺塔游戏的目标是将盘从一根柱重新堆叠到另一根柱，而不将盘放在小盘之上。

*(注：后续文本为大量重复内容，已根据要求去重并保留核心逻辑结构)*

## 栈选择

追踪最大值。将最大项存储在变量 `largest_item` 中。

此时，有 `(num_items - i - 1)` 个未排序的项。

```
<将 largest_item 添加到原始栈中
在之前已排序项的末尾.>
```

<将未排序的项从 temp_stack 移回

原始栈，当遇到 largest_item 时跳过它>

继续处理下一个 i

结束栈选择 (End StackSelections)

对于每个项目，该算法将未排序的项移动到临时栈中，将最大项添加到原始栈的排序部分，然后将剩余未排序的项目从临时栈移动到原始栈。对于数组中的每个位置，我们必须移动两次未排序的项目。在不同的步骤中，有 N, N-1, N-2, ... 个未排序的项需要移动，因此移动的项目总数为 N × (N-1) + (N-2) + ... + 1 = N × (N+1)/2，算法的运行时间为 O(N²)。

## 队列

队列是一种数据结构，项按照先进先出的顺序进行添加和移除。由于这种先进先出（FIFO，通常读作“ife-oh”）的行为，栈有时被称为 FIFO 列表或 FIFOs。

队列类似于商店的收银台。你加入队尾并等待轮到你。当你走到队首时，收银员会给你一张收据。

通常，向队列添加项的方法称为 Enqueue（入队），从队列中移除项的方法称为 Dequeue（出队）。

接下来的章节描述了实现队列的几种常用方法。

### 链表队列

使用链表实现队列是非常简单的。为了方便从队列中移除最后一个项，队列应该使用双向链表。

Enqueue 方法简单地在列表顶部添加一个新单元，而 Dequeue 方法从列表中移除底部的单元。

以下伪代码显示了在链表中入队项的算法：

```
Enqueue(Cell: top_sentinel, Data: new_value)
  // 创建一个单元来存储新值。
  Cell: new_cell = New Cell
```

```
new_cell.Value = new_value
```

```
// 将新单元添加到链表中。
new_cell.Next = top_sentinel.Next
top_sentinel.Next = new_cell
new_cell.Prev = top_sentinel
```

```
End Enqueue
```

以下伪代码显示了从链栈中出队项的算法：

```
Data: Dequeue(Cell: bottom_sentinel)
// 确保有项可以出队。
If (bottom_sentinel.Prev == top_sentinel) Then <抛出异常>

// 获取底部单元的值。
Data: result = bottom_sentinel.Prev.Value

// 从链表中移除底部单元。
bottom_sentinel.Prev = bottom_sentinel.Prev.Prev
bottom_sentinel.Prev.Next = bottom_sentinel

// 返回结果。
Return result
```

```
End Dequeue
```

> 注意：参见第 3 章以了解关于使用链表的更多详情。

使用链表，入队和出队的操作运行时间均为 O(1)，这两个操作都非常快。列表除了单元之间的连接外，不需要额外空间，因此链表是空间高效的。

### 数组队列

在数组中实现队列比使用链表实现要复杂一点。为了跟踪已使用的数组位置，你可以使用两个变量：Next，用于标记下一个空位置；Last，用于标记存储最久的位置。然而，如果你简单地在数组的一端存储项并从另一端移除，被占的空间就会在数组中移动。

例如，假设队列在一个具有八个条目的数组中实现。考虑以下系列入队和出队操作：

```
Enqueue(M)
Enqueue(O)
Enqueue(V)
Dequeue() // 移除 M.
Dequeue() // 移除 O.
Enqueue(I)
Enqueue(N)
Enqueue(Q)
Dequeue() // 移除 V.
Dequeue() // 移除 I.
```

图 5-9 显示了这一操作序列。最初 Next 和 Last 指向同一个条目。这表示队列为空。在执行一系列操作后，只剩下两个空空间可以添加新项。之后，将无法向队列添加新项。

解决此问题的方法之一是在 Next 越数组边界时扩大数组。遗憾的是，这将导致数组随时间变大，并且 Last 之前的所有空间将被浪费。

另一种方法是每当 Last 越界时，将数组项移动到数组开头。这种方法可行，但速度相对较慢。

![](img/fefa42765c0b410af6705110aea7c0cb_148_0.png)

**图 5-9：** 在基于数组的队列中入队和出队时，被占的空间会在数组中移动。

更有效的方法是构建一个循环数组，其中你将最后一个项视为紧接在第一个项之前的项。当 Next 越界时，它会绕回。

## 特殊队列
