
visit(curPtr->getItem())
nodeStack.pop()
// Traverse the right subtree of the node just visited
curPtr = curPtr->getRightChildPtr()
}
else
done = true
}

消除递归可能比这里给出的示例更复杂。然而，一般情况超出了本书的范围。

## 16.3 二叉搜索树 ADT 的链式实现

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_497_0.png)

由于二叉搜索树是一种二叉树，其实现可以使用与二叉树实现相同的节点对象。由于我们计划采用链式实现，将使用前面在清单 16-2 中给出的类 BinaryNode。

我们在第 15 章第 15.3.2 节中介绍的递归搜索算法是二叉搜索树上插入、删除和检索操作的基础。接下来针对二叉搜索树操作的算法假设采用本章前面讨论过的二叉树链式实现。还要牢记，二叉搜索树中的数据项是唯一的这一假设。

### 16.3.1 二叉搜索树 ADT 操作的算法

添加新条目。如第 15 章第 15.3.3 节所示，将新条目插入二叉搜索树的位置与搜索算法查找它的位置相同。例如，如果要将科迪插入图 16-7a 所示的二叉搜索树，首先需要搜索该树

使用搜索确定插入点

图 16-7 (a) 二叉搜索树；(b) 搜索算法在查找科迪时终止的空子树；(c) 将科迪插入为新叶节点后的树

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_497_1.png)

以查找科迪。搜索算法将在南希的空左子树处终止，如图 16-7b 所示。然后将科迪插入为南希的左子节点，如图 16-7c 所示。

因为南希没有左子节点，插入操作很简单，只需让南希的左子指针指向科迪。因为在二叉搜索树中搜索不存在的条目总是以空子树结束，因此你始终将新项插入为新叶节点。因为添加叶节点只需更改父节点中的相应指针，插入所需的工作几乎与相应的搜索相同。

我们先定义公共方法 add，如下所示：

```
template<class ItemType>
bool BinarySearchTree<ItemType>::add(const ItemType& newData)
{
   BinaryNode<ItemType>* newNodePtr = new BinaryNode<ItemType>(newData);
   rootPtr = insertInorder(rootPtr, newNodePtr);
   return true;
} // end add
```

该方法创建一个新节点，并将树和新节点的指针传递给实际执行插入操作的递归方法。以下高级伪代码描述了此插入过程：

### 插入算法的初稿

```
// Inserts a new node into a binary search tree.
insertInorder(subTreePtr: BinaryNodePointer,
              newNodePtr: BinaryNodePointer): BinaryNodePointer

Search the tree pointed to by subTreePtr for the item in the node pointed
to by newNodePtr
if (the search terminates at parentNode's left subtree)
   Set leftChildPtr of parentNode to newNodePtr
else
   Set rightChildPtr of parentNode to newNodePtr
```

父节点 parentNode 的相应指针（leftChildPtr 或 rightChildPtr）必须设置为指向新节点。搜索算法的递归性质提供了一种优雅的设置指针的方法，前提是你返回可能更改后的指针。这种情况与你在第 9 章中看到的 ADT 列表的递归插入方法非常相似。如果插入前树为空，则指向树根的外部指针将为 nullptr，且方法不会进行递归调用。因此，你将返回指向新节点的指针。我们的伪代码细化如下：

### 插入算法的细化

```
// Inserts a new item into the binary search tree to which subTreePtr points.
insertInorder(subTreePtr: BinaryNodePointer,
              newNodePtr: BinaryNodePointer): BinaryNodePointer

if (subTreePtr is nullptr)
   return newNodePtr
else if (subTreePtr->getItem() > newNodePtr->getItem())
{
   tempPtr = insertInorder(subTreePtr->getLeftChildPtr(), newNodePtr)
   subTreePtr->setLeftChildPtr(tempPtr)
}
else
{

```

图 16-8 (a) 向空树插入；(b) 查找弗兰克在叶节点处终止；(c) 在叶节点处插入

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_499_0.png)

```
tempPtr = insertInorder(subTreePtr->getRightChildPtr(), newNodePtr)
subTreePtr->setRightChildPtr(tempPtr)
}
return subTreePtr;
```

当 subTreePtr 为 nullptr 时，insertInorder 返回指向新节点的指针。对于最初为空的树，add 将返回的指针赋给 rootPtr，如图 16-8a 所示。对于非空树，add 将返回的指针赋给空子树父节点中当前值为 nullptr 的 leftChildPtr 或 rightChildPtr 指针。因此，父节点中的相应指针被设置为指向新节点。图 16-8 的 b 和 c 部分说明了插入的一般情况。

你可以使用公共方法 add 来创建二叉搜索树。例如，从空树开始，如果按简、鲍勃、阿兰、伊丽莎、汤姆、南希和温迪的顺序插入这些名字，你将得到第 15 章图 15-13 中的二叉搜索树。有趣的是，简、鲍勃、阿兰、伊丽莎、汤姆、南希和温迪这些名字构成了图 15-13 中树的前序遍历。因此，如果你取二叉搜索树的前序遍历输出，并将其与 insertInorder 一起用于创建二叉搜索树，你将得到一棵重复的树。这一结果不应让你感到惊讶，因为 ADT 二叉树的拷贝构造函数使用了前序遍历来复制树。

通过以不同顺序插入前面的名字，你将得到不同的二叉搜索树。

例如，按字母顺序插入前面的名字，你将得到第 15 章图 15-14b 中的二叉搜索树。

问题 7 从空二叉搜索树开始，应以什么顺序插入项才能得到第 15 章图 15-18 中的二叉搜索树？

### 删除算法的初稿

删除条目。从二叉搜索树中删除条目比添加条目稍微复杂一些。首先，你使用搜索算法定位指定的项，然后，如果找到它，必须将其从树中删除。该算法的初稿如下：

```
// Removes the given target from a binary search tree
// Returns true if the removal is successful or false otherwise.
removeValue(target: ItemType): boolean
   Locate the target by using the search algorithm
   if (target is found)
      Remove target from the tree
      return true
   else
      return false
```

### 包含要删除的项的节点 N 的三种情况

这里的基本任务是将目标从树中删除。假设 removeValue 在特定节点 N 中定位了目标，需要考虑三种情况：

- N 是叶节点
- N 只有一个子节点
- N 有两个子节点

### 情况 1：将叶节点父节点中的指针设置为 nullptr

情况 1。第一种情况最简单。要删除包含目标的叶节点，只需将其父节点中的指针设置为 nullptr。

### 情况 2：只有一个子节点的节点的两种可能性

情况 2。第二种情况稍微复杂一些。如果 N 只有一个子节点，你有两种可能性：

- N 只有左子节点
- N 只有右子节点

### 让 N 的父节点收养 N 的子节点

这两种可能性是对称的，因此仅需说明左子节点的解决方案。在图 16-9a 中，L 是 N 的左子节点，P 是 N 的父节点。N 可以是 P 的左子节点或右子节点。如果从树中删除 N，L 将没有父节点，P 也将少一个子节点。假设你让 L 取代 N 成为 P 的一个子节点，如图 16-9b 所示。这种收养是否保留了二叉搜索树属性？

例如，如果 N 是 P 的左子节点，则以 N 为根的子树中的所有数据项都小于 P 中的项。因此，以 L 为根的子树中的所有数据项都小于 P 中的项。因此，在删除 N 并让 P 收养 L 之后，P 左子树中的所有项仍然小于 P 中的项。因此，这种策略保留了二叉搜索树属性。如果 N 是 P 的右子节点，也有类似的论证，因此在两种情况下都保留了二叉搜索树属性。

### 情况 3：N 有两个子节点

情况 3。三种情况中最困难的一种是要删除的项位于有两个子节点的节点 N 中，如图 16-10 所示。正如你刚才看到的，当 N 只有一个子节点时，子节点替换 N。但是，当 N 有两个子节点时，这些子节点不能同时替换 N：N 的父节点只能容纳 N 的一个子节点作为 N 的替代品。需要一种不同的策略。

事实上，你根本不会删除 N。你可以找到另一个更容易删除的节点，并删除它而不是 N。这种策略听起来可能像作弊，但请记住，客户只期望从 ADT 中删除某个特定条目。由于程序与 ADT 实现之间存在隔离墙，它无权期望删除树中的某个特定节点。

### 删除其节点有两个子节点的项

那么，考虑一种替代策略。要从二叉搜索树中删除位于有两个子节点的节点 N 中的项，请执行以下步骤：

1. 找到另一个比节点 N 更容易从树中删除的节点 M。
2. 将 M 中的项复制到 N，从而有效地从树中删除原本在 N 中的项。
3. 从树中删除节点 M。
