

作为执行伪代码的示例，假设我们正在将 18 松散地插入到这个 B 树中（MAXIMUM 设置为 2）：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_586_0.png)

伪代码的第 1 步在根中查找第一个不小于新条目 18 的项。如你所见，根中的所有条目都小于 18，那么第 1 步反而会做什么呢？从伪代码中可以看出，索引 i 将被设置为 2（根节点中的条目数量）。

在第 2 步中，我们注意到既没有在根中找到新条目，也没有到达叶子节点。因此我们继续执行第 2c 步，递归调用将 18 插入到子树 2 中，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_586_1.png)

递归调用找到一个只有根的小子树。按照第 2b 步，递归调用将数字 18 插入到子树的根中，然后返回 true。递归调用返回后，整个树如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_586_2.png)

递归调用返回后，我们执行第 2c 步的其余部分，检查子树的根是否现在有太多条目。的确，subset[2] 的根现在有三个条目，比允许的最大值多一个。我们必须修复这个问题子节点，但如何修复呢？修复子节点似乎需要相当多的工作，因此我们将提出另一个私有成员函数来完成这项工作。

## 修复子节点溢出的私有成员函数

我们心目中的私有成员函数的规范如下：

```
template <class Item>
void set<Item>::fix_excess(std::size_t i);
// Precondition: (i < child_count) and the entire B-tree is valid EXCEPT that
// subset[i] has MAXIMUM + 1 entries.
// Postcondition: The tree has been rearranged so that the entire B-tree is
// valid EXCEPT that the number of entries in the root of this set might be
// one more than the allowed maximum.
```

查看规范，你可以看到该函数从一个问题子节点开始。当函数结束时，子节点不再有问题，尽管根可能现在有问题。fix_excess 函数的方法可以简单地陈述为：

> 修复溢出条目的子节点
> 要修复具有 MAXIMUM + 1 个条目的子节点，将子节点拆分为两个节点，每个节点包含 MINIMUM 个条目。这会留下一个额外的条目，该条目将向上传递给父节点。

让我们来看看这种方法的示例。在示例中，假设 MINIMUM 是 2，因此节点中的最大条目数为 4（即 2*MINIMUM）。我们想要修复示例树中的子树 1（阴影子树）：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_587_0.png)

fix_excess 采用的方法是将问题节点（具有 2*MINIMUM + 1 个条目）拆分为两个较小的节点（每个节点包含 MINIMUM 个条目）。这会留下一个未处理的条目，该额外条目将向上传递给拆分节点的父节点。因此，拆分节点的父节点会增加一个额外的子节点（来自拆分满节点）以及一个额外的条目（向上传递的额外条目）。在上面所示的示例中，拆分结果如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_588_0.png)

总是拆分节点的 *中间* 条目向上移动。另外，请注意，拆分节点的子节点已在两个较小的节点之间均匀分配。

作为 fix_excess 的另一个示例，假设 MAXIMUM 是 2，并且我们有如下所示的问题子节点：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_588_1.png)

调用 fix_excess(2) 后，问题子节点将被拆分为两个节点，中间条目向上传递，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_588_2.png)

如本示例所示，修复问题子节点可能会创建一个具有多余条目的根——但这没关系，因为 fix_excess 的后置条件允许根有一个额外的条目。

## 回到插入成员函数

我们需要完成对原始插入函数的讨论。通过使用 loose_insert 函数，公共插入函数只有两个步骤：

```
// Pseudocode for the public insert member function
if (!loose_insert(entry))
    Return false since loose_insert did not add a new entry to the set.
if (data_count > MAXIMUM)
    Fix the root of the entire tree so that it no longer has too many entries.
Return true.
```

在这个伪代码中，我们如何“修复整个树的根，使其不再有太多条目？”该步骤可以分为两部分。第一部分将根中的所有条目和子节点指针复制到新分配的节点中，并清空根，使其只有一个子节点（即新分配的节点）且没有条目。例如，假设我们执行松散插入，然后 B 树如下所示（MAXIMUM 设置为 2）：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_589_0.png)

我们将从根复制所有内容到新节点并清空根。在生成的树中，根将没有条目，其他所有内容都向下移动了一层，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_589_1.png)

以这种方式移动内容后，问题现在出在根的子节点上。我们可以通过将根的 subset[0] 拆分为两个节点并向上传递中间条目来修复这个问题。事实上，如果你在编写 fix_excess 时小心谨慎，可以通过调用 fix_excess(0) 来完成此拆分。必须小心，因为这个根没有条目，因此 fix_excess 必须准备好处理这种情况。（如果你采用这种方法，应该在其前置条件中记录 fix_excess 的扩展能力。）

在本示例中，拆分 subset[0] 后，我们得到了如下所示的完全有效的 B 树：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_589_2.png)

### B 树仅在根处增加高度

顺便说一句，在插入成员函数中，根处的这种增长是 B 树增加高度的唯一位置。

## 图 11.6 插入成员函数的自顶向下设计

插入函数调用：

- loose_insert
- fix_excess

loose_insert 函数是递归的，还调用：

- fix_excess
- 各种数组函数

fix_excess 函数调用：

- 各种数组函数

## 采用自顶向下设计

在进行项目时，请牢记我们采用的自顶向下设计。如图 11.6 所示，原始插入成员函数调用私有成员函数 loose_insert。普通插入和松散插入函数都会调用 fix_excess。在 fix_excess 的设计中，有几个地方你应该提出并实现更小的函数，以执行数组中元素复制和移动的基本工作。你可能能够使用 <algorithm> 库中的一些函数来完成这项数组工作（参见附录 G）。

## 从 B 树中删除一个项目

set 的 erase 成员函数从 B 树中删除一个条目。大部分工作将通过私有成员函数 loose_erase 完成，它执行一种“松散删除”，类似于松散插入。loose_erase 中的松散性是因为它允许留下一个条目过少的根。换句话说，它可能会使整个树的根没有条目（除非也没有子节点，否则这是不允许的），或者可能会使内部子树的根少于 MINIMUM 个条目。loose_erase 的规范如下：

```
template <class Item>
bool set<Item>::loose_erase(const Item& target);
// Precondition: The entire B-tree is valid.
// Postcondition: If target was not in the set, then the set is unchanged and
// the return value is false. Otherwise, the target has been removed, the
// return value is true, and the entire B-tree is still valid
// EXCEPT that the number of entries in the root of this set might be one
// less than the allowed minimum.
```

我们完整的 erase 函数将首先调用 loose_erase。之后，如果需要，我们可以修复可能留下零个条目和一个子节点的根。因此，erase 伪代码有以下步骤：

删除的伪代码

```
// Pseudocode for the public erase member function
if (!loose_erase(target))
    Return false since loose_erase did not remove an entry from the set.
if ((data_count == 0) && (child_count == 1))
    Fix the root of the entire set so that it no longer has zero entries.
Return true since an entry was removed from the set.
```

