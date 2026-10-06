

## 442 第 15 章 树

```cpp
the tree is empty, inserts a new root node containing the
data into the tree.
@pre None.
@post The data in the root of the binary tree is as given.
virtual void setRootData(const ItemType& newData) = 0;
/** 向此二叉树添加一个包含给定数据的新节点。
@param newData 新节点的数据。
@post 二叉树包含一个新节点。
@return 如果添加成功则返回 True，否则返回 false。 //
virtual bool add(const ItemType& newData) = 0;
/** 从此二叉树中根据给定数据项移除节点。
@param data data 要从树中移除的数据值。 /
@return 如果移除成功则返回 True，否则返回 false。 //
virtual bool remove(const ItemType& data) = 0;
/** 从此二叉树中所有节点。 /
virtual void clear() = 0;
/** 在此二叉树中获取特定的条目。
@post 条目已返回，二叉树保持不变。如果未找到此类条目，则抛出异常。
@param anEntry 要在二叉树中定位的匹配该条目的条目。
@throw NotFoundException 如果条目不在树中。 //
virtual Item getEntry(const ItemType& anEntry) const
throw(NotFoundException) = 0;
/** 测试给定条目是否存在于此二叉树中。
@post 二叉树保持不变。
@return 如果条目出现在树中则返回 True，否则返回 false。 //
virtual bool contains(const ItemType& anEntry) const = 0;
/** 按照前序（中序、后序）遍历此树，并对每个节点调用一次函数。
@param visit 客户端定义的函数，对每个访问的节点或节点中的数据执行操作。 /
virtual void preorderTraverse(void visit(const ItemType&)) const = 0;
virtual void inorderTraverse(void visit(const ItemType&)) const = 0;
virtual void postorderTraverse(void visit(const ItemType&)) const = 0;
}; // endBinaryTreeInterface
endif
```

## 15.3 ADT 二叉搜索树

![](img/d0cb86b2f18b2db569968ad7c743510e_468_0.png)

ADT 二叉搜索树

查找某项是 ADT 树并不擅长的操作之一。二叉搜索树通过按值组织其数据纠正了这一缺陷。回想二叉树中的每个节点 $n$ 都满足以下三个属性：

- * *n 的值大于其左子树 $T_L$ 中的所有值*
- * n 的值小于其右子树 $T_R$ 中的所有值*
- * $T_L$ 和 $T_R$ 都是二叉搜索树*

二叉搜索树的递归定义

## ADT 二叉搜索树 443

这种数据组织方式允许你在给定值而非位置的情况下，在二叉搜索树中搜索特定的数据项。

**示例**。让我们考虑一个节点包含人名字的二叉搜索树。假设这些对象是 Alan, Bob, Elise, Jane, Nancy, Tom 和 Wendy。图 15-13 展示了我们用这些名字形成的一个二叉搜索树。

## **图 15-13** 名字的二叉搜索树

![](img/d0cb86b2f18b2db569968ad7c743510e_469_0.png)

然而，许多不同的二叉搜索树可以包含相同的数据。例如，除了15-13中的树外，15-14 中的每棵树都是 Alan, Bob, Elise, Jane, Nancy, Tom 和 Wendy 这些名字有效二叉搜索树。尽管这些树的形状不同，但每一个都满足二叉搜索树的要求。

## **图 15-14** 与图 15-13 相同数据的二叉搜索树

![](img/d0cb86b2f18b2db569968ad7c743510e_469_1.png)

### 15.3.1 二叉搜索树操作

作为一种 ADT，二叉搜索树的操作与你在之前章节学习的 ADT 操作相似，因为它们涉及插入、移除和检索数据。与面向位置的 ADT（栈、列表和队列）不同，类似于排序列表 ADT，插入、移除和检索操作是按值的，而不是按位置的。另一方面，其他操作——包括

## 444 第 15 章 树

你刚刚看到的用于二叉树的遍历操作可以不加修改地应用于二叉搜索树，因为二叉搜索树本身就是二叉树。
定义 ADT 二叉搜索树的操作如下：

> 注意：ADT 二叉搜索树操作
* 测试二叉搜索树是否为空。
* 获取二叉搜索树的高度。
* 获取二叉搜索树中的节点数量。
* 获取二叉搜索树根节点的数据。
* 向二叉搜索树中插入新项。
* 从二叉搜索树中移除给定项。
* 从二叉搜索树中移除所有条目。
* 从二叉搜索树中检索项。
* 测试二叉搜索树是否包含特定条目。
* 按照前序、中序或后序遍历二叉搜索树中的项。

为了简单起见，我们坚持二叉搜索树包含唯一的数据。以下契约详细说明了插入和移除操作。二叉树类的 UML 图将与二叉树类的图几乎相同，因此我们在这里不写了。

| 抽象数据类型：二叉搜索树 | |
| :--- | :--- |
| 数据 | 按层次顺序排列的有限对象 |
| 操作 | |
| 伪代码 | 描述 |
| add(newEntry) | 任务：将 newEntry 插入此二叉搜索树，以维护二叉搜索树的属性。输入：newEntry 是要插入的数据。假设树中的条目是唯一的且与 newEntry 不同。输出：如果插入成功返回 True，否则返回 false。 |
| remove(anEntry) | 任务：从此二叉搜索树中移除给定条目，以维护二叉搜索树的属性。输入：anEntry 是要移除的条目。输出：如果移除成功返回 True，否则返回 false。 |

方法 `isEmpty`、`getHeight`、`getNumberOfNodes`、`getRootData`、`clear`、`contains`、`preorderTraverse`、`inorderTraverse` 和 `postorderTraverse` 与二叉树的规范相同。471

然而，查找的时间取决于树的形状，你会看到。

img/d0cb86b2f18b2db569968ad7c743510e_471_0.png

- **问题 9** 证明 15-13 和 15-14 中的每棵树都是二叉树。
- **问题 10** 证明 15-13 和 15-14 二叉搜索树的中序遍历是相同的。
- **问题 11** 二叉搜索树的前序和后序遍历是什么？前序遍历相同吗？

## 15.3.2 搜索二叉搜索树

再次考虑 15-13 中的搜索树。树中的每个节点包含一个人的名字。假设你想在二叉搜索树中定位 Elise。树的根节点包含 Jane，因此如果 Elise 在树中，它必须在 Jane 的左子树中，因为按字母顺序 "Elisa" 小于 "Jane"。因为二叉搜索树是递归的，对树表制定递归操作是自然的。因此，你发现 Jane 的左子树也是二叉树，所以你对 Elise 使用相同的搜索策略。该树的根包含 Bob，且搜索 "Elisa" 大于搜索 "Bob"，Elise 必须在 Bob 的右子树中。该右子树也是二叉树，并且恰好位于该树的根节点中。搜索已定位 Elise。

// 为给定值搜索二叉搜索树。

```cpp
search(bst:BinarySearchTree, target: ItemType)

if (bst is empty)
    未找到所需的项
else if (target == data item in the root of bst)
    未找到所需的项
else if (target < data item in the root of bst)
    search(Left subtree of bst, target)
else
    search(Right subtree of bst, target)
```

二叉搜索树的搜索算法

正如你所看到的，这种搜索算法是二叉搜索树其他操作的基础。树的形状完全不影响搜索算法的质量。该算法要求 a 是二叉搜索树。然而，搜索算法在某些情况下运行更高效。

