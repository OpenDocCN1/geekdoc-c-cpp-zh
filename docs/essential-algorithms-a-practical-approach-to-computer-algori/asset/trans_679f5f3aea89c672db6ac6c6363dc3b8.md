
仅通过分支就可以更快速地进行中序遍历或反序遍历。

![](img/fefa42765c0b410af6705110aea7c0cb_274_0.png)

> 注意：你可以在树中定义其他类型的线程，但这种类型是最常见的。因为它包含了穿过树的中序遍历的正向和反向线程，这种树有时被称为对称线程树（symmetrically threaded tree）。

> 注意：注意图 10-12 中的所有节点都有左分支或右分支。如果你能以某种方式区分它们，可以对两个分支和线程使用相同的引用。例如，如果你在节点类中使用两个布尔变量 `HasLeftBranch` 和 `HasRightBranch`，那么在将这些变量设置为 `True` 时，你可以将线程存储在子节点链接中。

你可以将这两个布尔值封装到一个字节中，并使用字节操作来查看它们是否存在。在实践中，如果你处理的是一棵巨大的树，保存在内存中可能还没有额外的复杂性和潜在的混乱。

要使用这种线程树，你需要知道两点：如何构建树以及如何遍历它。

## 构建线程树

线程树从一个节点开始，该节点没有分支，且线程设置为 `null`。创建节点非常简单。技巧在于向树中添加新节点。有两种情况，取决于你将新节点作为父节点的左子还是右子添加。

首先，假设你正将新节点作为左子添加。假设你在图 10-12 所示的树中，将节点 3 添加为节点 4 的左子。由于新节点放置的位置，它的值是父节点值下一个较小的值。（在本例中，3 是 4 之后的下一个较小值。）

这意味着遍历中新节点之前的节点是原先在父节点之前的节点。（在本例中，3 之前的节点是原本在 4 之前的节点——在这种情况下，是 2）。在创建新节点时，将新节点的左线程设置为父节点左线程的值。

现在，父节点的先驱节点变成了新节点。父节点的左分支指向新节点，因此父节点不再需要它的左线程，你应该将其设置为 `null`。

新节点的右线程应该指向树的遍历中的下一个节点。由于新节点放置的位置，那个节点是父节点，因此你应该将新节点的右线程设置为其父节点。（在本例中，节点 3 的右线程应该指向节点 4）。

图 10-13 显示了添加节点 3 后的更新树。

![](img/fefa42765c0b410af6705110aea7c0cb_275_0.png)

**图 10-13：** 当你插入一个左子节点时，它的左线程指向父节点左线程曾经指向的地方。

当你将一个节点作为现有节点的右子添加时，步骤是类似的，只是左右分支和线程的角色发生了反过了。新节点的右线程获取父节点右线程的值，而父节点的右线程被设置为 `null`。新节点的左线程指向父节点。

图 10-14 显示了在图 10-13 的基础上插入新节点 8 后的树。以下伪代码显示了向线程子树中插入节点的算法。

```
// 向此节点排序子树中添加节点。
AddNode(Data: new_value)
// 检查新值是否比我们的值小。
If (new_value < this.Value)
  // 新值较小。将其添加到左子树。
  If (this.LeftChild != null)
    Then this.LeftChild.AddNode(new_value)
  Else
    // 在此处添加新节点。
    Threaded child = ThreadedNode(new_value)
    child.LeftThread = this.LeftThread
    child.RightThread = this
    this.LeftChild = child
    this.LeftThread = null
End If
Else
// 新值并不较小。将其添加到右子树。
  If (this.RightChild != null)
    Then this.RightChild.AddNode(new_value)
  Else
    // 在此处添加新节点。
    Threaded child = ThreadedNode(new_value)
    child.LeftThread = this
    child.RightThread = this.RightThread
    this.LeftChild = child
    this.RightThread = null
End If
End AddNode
```

![](img/fefa42765c0b410af6705110aea7c0cb_276_0.png)

**图 10-14：** 当你插入一个右子节点时，它的右线程指向父节点右线程曾经指向的地方。
