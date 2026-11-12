

二叉树的遍历操作——你刚才看到的那些——不加改动地适用于二叉搜索树，因为二叉搜索树本身就是一棵二叉树。

定义抽象数据类型二叉搜索树的操作如下：

- **注意：抽象数据类型二叉搜索树操作**
- 测试二叉搜索树是否为空。
- 获取二叉搜索树的高度。
- 获取二叉搜索树中的节点数量。
- 获取二叉搜索树根节点中的数据。
- 将新项插入二叉搜索树。
- 从二叉搜索树中移除给定项。
- 从二叉搜索树中移除所有条目。
- 从二叉搜索树中检索给定项。
- 测试二叉搜索树是否包含特定条目。
- 以先序、中序或后序遍历二叉搜索树中的项。

为简单起见，我们将坚持二叉搜索树包含唯一数据。以下契约更详细地指定了插入和移除操作。二叉搜索树类的UML图将与二叉树类的UML图几乎相同，因此我们不在此处编写。

## 抽象数据类型：二叉搜索树

### 数据
- 按层级顺序排列的有限数量的对象。

### 操作
| 伪代码 | 描述 |
| :--- | :--- |
| add(newEntry) | 任务：将newEntry插入此二叉搜索树，使二叉搜索树的属性得以维持。输入：newEntry是要插入的数据项。假设树中的条目互不相同且与newEntry不同。输出：如果插入成功则为True，否则为false。 |
| remove(anEntry) | 任务：从此二叉搜索树中移除给定条目，使二叉搜索树的属性得以维持。输入：anEntry是要移除的条目。输出：如果移除成功则为True，否则为false。 |

方法isEmpty、getHeight、getNumberOfNodes、getRootData、clear、getEntry、contains、preorderTraverse、inorderTraverse和postorderTraverse的规范与二叉树相同。

**示例。** 如果nameTree是图15-13和15-14中的任意一棵二叉搜索树，且其节点包含字符串，则语句

`string name = nameTree.getEntry(nancy);`

其中nancy是包含"Nancy"的字符串变量，该语句定位包含"Nancy"的节点并将其数据赋给name。无论getEntry搜索哪棵树，结果都相同。然而，getEntry查找nancy所需的时间取决于树的形状，如你将看到的。如果字符串变量hal包含"Hal"，并且你通过调用nameTree.add(hal)将其插入nameTree，那么你以后将能够检索hal，并且仍然能够检索nancy。如果你使用nameTree.remove(Jane)移除jane，你仍然能够检索对象nancy和hal。最后，如果displayName是显示其字符串参数的客户端函数，nameTree.inorderTraverse(displayName)将按字母顺序显示nameTree所代表的人员的姓名。同样，无论你遍历哪棵树都无关紧要。

- 问题9 证明图15-13和15-14中的每棵树都是二叉搜索树。
- 问题10 证明图15-13和15-14中每棵二叉搜索树的中序遍历结果相同。
- 问题11 图15-13和15-14中每棵二叉搜索树的先序遍历和后序遍历分别是什么？先序遍历结果相同吗？后序遍历结果相同吗？

## 15.3.2 搜索二叉搜索树

再次考虑图15-13中的二叉搜索树。树中的每个节点都包含一个人名。假设你想在二叉搜索树中定位Elisa。树的根节点包含Jane，因此如果Elisa存在于树中，它必定在Jane的左子树中，因为字符串"Elisa"在字母表中排在字符串"Jane"之前。由于二叉搜索树天生具有递归性，为树上的操作制定递归算法是很自然的。因此，你知道Jane的左子树也是一棵二叉搜索树，所以你使用完全相同的策略来搜索这棵子树中的Elisa。这棵二叉搜索树的根节点包含Bob，并且由于字符串"Elisa"大于字符串"Bob"，Elisa必定在Bob的右子树中。那个右子树也是一棵二叉搜索树，而且Elisa恰好位于这棵树的根节点中。因此，搜索已定位到Elisa。

二叉搜索树的搜索算法

```
// Searches the binary search tree for a given target value.
search(bstTree: BinarySearchTree, target: ItemType)

if (bstTree is empty)
    The desired item is not found
else if (target == data item in the root of bstTree)
    The desired item is found
else if (target < data item in the root of bstTree)
    search(Left subtree of bstTree, target)
else
    search(Right subtree of bstTree, target)
```

如你将看到的，这个搜索算法是二叉搜索树上其他操作的基础。树的形状绝不影响搜索算法的有效性。该算法只要求树是一棵二叉搜索树。然而，搜索算法在某些树上的效率高于其他树。例如，对于图15-14b中的树，search在定位Wendy之前会检查每个节点。事实上，这棵二叉搜索树实际上与排序列表的链式表示具有相同的结构，在效率上没有优势。相比之下，对于图15-13中的满树，搜索算法仅检查包含Jane、Tom和Wendy姓名的节点。这些姓名正是二叉搜索图15-15中排序数组时会检查的姓名。

### 图15-15 按排序顺序排列的姓名数组

| Alan | Bob | Elisa | Jane | Nancy | Tom | Wendy |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 |

二叉搜索树的形状影响其操作的效率。二叉搜索树越平衡，它就越远离线性结构，搜索算法的行为就越接近对数组的二叉搜索（也就越远离线性搜索的行为）。在本章后面，你将了解更多关于二叉搜索树的形状如何影响搜索效率，以及插入和移除操作如何影响这种形状。

> **问题12** 使用图15-14c中的树，跟踪搜索二叉搜索树的算法，以查找
> 
> a. Elisa
> 
> b. Kyle
> 
> 在每种情况下，按搜索访问节点的顺序列出节点。

## 15.3.3 创建二叉搜索树

假设你想将Frank插入图15-13的二叉搜索树中。第一步，想象你实际上想搜索字符串“Frank”。搜索算法首先搜索以Jane为根的树，然后搜索以Bob为根的树，接着搜索以Elisa为根的树。然后它搜索以Elisa的右子节点为根的树。由于这棵树为空，如图15-16所示，搜索算法已达到基准情况，并将终止并报告Frank不存在。搜索在Elisa的右子树中查找Frank是什么意思？首先，这意味着如果Frank是Elisa的右子节点，search本会在那里找到Frank。

使用搜索确定插入点

这一观察表明，将Frank作为Elisa的右子节点插入是一个很好的位置。因为Elisa没有右子节点，插入很简单，只需添加一个新的叶节点。更重要的是，Frank应该位于这个位置——search会在这里查找Frank。具体来说，将Frank作为Elisa的右子节点插入将保留树的二叉搜索树属性。因为，在搜索Frank时，你会遵循一条通往Elisa右子节点的路径，你可以确信Frank与树中其上方的名称具有正确的关系。

> **注意：** 使用搜索来确定在树中插入新名称的位置总是会导致简单的插入。无论你向树中插入什么新项，search总是会在空子树处终止。因此，search总是告诉你将项作为新叶节点插入。

