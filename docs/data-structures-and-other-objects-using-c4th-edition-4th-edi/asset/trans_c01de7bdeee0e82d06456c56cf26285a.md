

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_572_0.png)

21 已与其较大的子节点交换。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_572_1.png)

再次，21 已与其较大的子节点交换。

### 向下重堆化

此时，下沉的节点已到达叶子，因此可以停止，结构已成为堆。当下沉的节点不再小于其任何一个子节点时，该过程也会停止。这一过程称为向下重堆化，如图 11.2 所示。堆还有其他几种应用，包括在第 13 章中讨论的一种排序算法。

### 图 11.2 从优先队列中移除一个条目

### 移除条目的伪代码

优先队列已实现为堆。

- 1. 将堆根处的条目复制到用于返回值的变量中。
- 2. 将最深层级的最后一个条目复制到根，然后将该最后节点从树中移除。此条目称为“位置不当”条目。
- 3. while (位置不当的条目小于其任何一个子节点) 将位置不当的条目与其较大的子节点交换。
- 4. 返回在第 1 步中保存的答案。

请注意，第 3 步中的过程将在位置不当的条目到达叶子，或当位置不当的条目不再小于其任何一个子节点时停止。

## 11.2 STL 优先队列和堆算法

STL 包含一个优先队列类，如图 11.3 所示。条目本身使用小于运算符直接相互比较。这就是我们在上一节中构建的那种优先队列。

此外，STL 的 #include <algorithm> 设施包含四个函数，用于从数组或其他带有迭代器的结构中创建和操作堆。例如，假设 data 是长度为 N 的整数数组。函数 make_heap 使用高效的 O(N) 算法将数组转换为堆，该算法我们在第 11.1 节中未展示。函数调用如下：

```
make_heap(data, data+N);
```

第一个参数是数组及其长度，与第 3 章（第 116 页）中的 copy 函数相同。另外两个函数允许你向现有堆中添加和移除项。调用 push_heap(data, data+N) 假设 data[0] 到 data[N-2] 已经是一个堆，且要添加的新元素位于 data[N-1]。调用 pop_heap(data, data+N) 假设 data[0] 到 data[N-1] 是一个堆；在 pop_heap 调用之后，最大的元素（来自 data[0]）已与 data[N-1] 交换，其余部分已重堆化。

### 图 11.3 标准库优先队列类

### 来自 <queue> 的 priority_queue<Item> 类成员部分列表

```
// TYPEDEFS
// value_type: The data type of the items in the priority queue from the Item parameter
// For this version of the priority queue, the item must have a 'less than'
// operator < defined, forming a strict weak ordering (see
// Figure 3.12 on page 139). Appendix H shows other alternatives.
// size_type: The data type to keep track of how many items are in a priority queue
// CONSTRUCTOR
// Default constructor: Creates an empty priority queue
// VOID FUNCTIONS TO INSERT AND REMOVE ITEMS:
// pop( ): Removes the highest priority item of the priority queue
// push(const Item& entry): Adds an item to the priority queue
// FUNCTIONS TO EXAMINE THE QUEUE AND ITS ITEMS:
// empty( ): Returns true if the queue is empty; otherwise returns false
// size( ): Returns the number of items in the queue
// top( ): Returns the highest priority item of the queue (without removing it)
// If there are several equally high priorities, the implementation may
// decide which one to return.
// VALUE SEMANTICS:
// Assignments and the copy constructor may be used with priority_queue<Item> objects.
```

## 第 11.1 节和 11.2 节自测练习

- 1. 堆与二叉搜索树有何不同？
- 2. 编写一个 C++ 类定义，适用于作为最多 50 个条目的堆实现的值优先队列。编写第二个定义，该定义不对堆中的条目数量设置任何预定义限制。为第二个类使用动态数组。
- 3. 堆中的新条目最初放置在哪里？为什么？
- 4. 从堆中移除一个项后，哪个项被放置在根中？
- 5. 从一个空的整数堆开始，输入 1 到 10 的 10 个数字。绘制结果堆。
- 6. 从你在上一练习中创建的堆中移除三个条目。绘制结果堆。
- 7. 在向下重堆化的描述中，我们规定位置不当的条目必须与其两个子节点中较大的一个交换。如果与较小的子节点交换会出什么问题？

## 11.3 B 树

二叉搜索树在第 10.5 节中用于实现一个包类。但是，二叉搜索树的效率可能会消失。本节解释了潜在问题并展示了一种修复方法。大部分内容不绑定到任何特定编程语言。

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_574_0.png)

### 不平衡树的问题

让我们创建一个棘手的整数二叉搜索树。第一个数字是 1，然后按顺序添加 2、3、4 和 5。结果如图 11.4(a) 所示。也许你已经发现了问题。假设接下来按顺序添加 6、7、8、9 和 10，最终得到图 11.4(b)。问题是树的层级仅稀疏填充，导致长而深的路径，从而违背了使用深度二叉树的初衷。例如，如果我们在图 11.4(b) 中搜索数字 12，最终将查看树中的每个节点。实际上，我们并不比链表实现更好。添加和删除条目时也会出现类似问题。

该问题有几种可能的解决方案，所有这些方案都涉及叶子深度保持较小的树。例如，一种解决方案是定期平衡搜索树，如第 10 章（第 538 页）编程项目 9 中所述。另一种解决方案使用一种称为 B 树的特殊树，其中叶子不能变得太深（相对于节点数量）。这些树由 R. Bayer 和 E. M. McCreight 于 1972 年提出（参见 *Acta Informatica* 第 1 卷第 1 期 [1972] 第 173–189 页中的“大型有序索引的组织与维护”）。本节其余部分提供了一个 B 树实现。

### B 树规则

B 树不是二叉树

B 树是一种特殊的树，类似于二叉搜索树，其中每个节点保存某种类型的条目。与二叉搜索树一样，实现需要能够通过小于运算符比较两个条目。但是 B 树不是二叉搜索树——事实上，B 树甚至不是二叉树，因为 B 树节点有远多于两个子节点。B 树的另一个重要属性是每个节点包含的不仅仅是一个条目。B 树的规则使搜索指定条目变得容易，并且这些规则还确保叶子不会变得太深。

B 树规则可以针对包或集合制定

精确的 B 树规则可以制定为使 B 树存储一个条目包，类似于我们之前见过的包实现。或者，B 树可以制定为存储一个条目集合。集合与包的区别在于，两个或多个相等条目可以在包中多次出现，但在集合中不能。例如，C++ 标准库有一个 set 模板类，其中禁止相等条目（详情见附录 H）。我们将研究 B 树规则的“集合制定”，但请记住，“包制定”也是可能的。

### B 树节点中的条目

每个 B 树都依赖于一个名为 MINIMUM 的正常数整数。该常数的目的是确定单个节点中保存多少个条目，如前两条 B 树规则所示：

- **B 树规则 1：** 根最少可以有一个条目（如果它也没有子节点，甚至可以没有条目）；其他每个节点至少有 MINIMUM 个条目。

- **B 树规则 2：** 节点中条目的最大数量是 MINIMUM 值的两倍。

虽然 MINIMUM 可以小至 1，但在实践中使用的值要大得多——可能是几百，甚至几千。

B 树节点的许多条目存储在数组中，因此我们可以谈论“索引 0 处的条目”或“索引 1 处的条目”，等等。在数组中，条目必须从小到大排序。这提供了我们的第三条 B 树规则：

- **B 树规则 3：** 每个 B 树节点的条目存储在一个部分填充的数组中，从最小条目（索引 0 处）到最大条目（数组的最后一个已用位置）排序。

