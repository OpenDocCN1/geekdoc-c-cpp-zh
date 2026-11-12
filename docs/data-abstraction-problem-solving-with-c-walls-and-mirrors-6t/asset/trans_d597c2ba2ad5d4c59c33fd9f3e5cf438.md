

其中 $r$ 是包含一个数据项的节点，$T_L$ 和 $T_R$ 均为高度为 $h - 1$ 的 2-3 树。在此情况下，$r$ 中的项必须大于左子树 $T_L$ 中的每一项，且小于右子树 $T_R$ 中的每一项。

- T 的形式为

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_596_0.png)

其中 $r$ 是包含两个数据项的节点，$T_L$、$T_M$ 和 $T_R$ 均为高度为 $h - 1$ 的 2-3 树。在此情况下，$r$ 中的较小项必须大于左子树 $T_L$ 中的每一项，且小于中间子树 $T_M$ 中的每一项。$r$ 中的较大项必须大于中间子树 $T_M$ 中的每一项，且小于右子树 $T_R$ 中的每一项。

### 注：向 2-3 树节点中放置数据项的规则

2-3 树的前面定义隐含了以下关于如何在其节点中放置数据项的规则：

- 2-节点（拥有两个子节点）必须包含一个数据项，该项大于左子节点的项且小于右子节点的项，如图 19-3a 所示。

- 3-节点（拥有三个子节点）必须包含两个数据项 $S$ 和 $L$，它们满足以下关系，如图 19-3b 所示：$S$ 大于左子节点的项且小于中间子节点的项；$L$ 大于中间子节点的项且小于右子节点的项。

- 叶节点可以包含一个或两个数据项。

### 图 19-3 2-3 树中的节点：(a) 2-节点；(b) 3-节点

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_596_1.png)

### 图 19-4 一棵 2-3 树

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_597_0.png)

清单 19-1 声明了用于 2-3 树的节点类。当节点仅包含一个数据项时，你可以将其放在 smallItem 中，并使用 leftChildPtr 和 midChildPtr 指向节点的子节点。为保险起见，你可以将 nullPtr 放在 rightChildPtr 中。

```
LISTING 19-1 A header file for a class of nodes for a 2-3 tree
/** A class of nodes for a link-based 2-3 tree.
 @file Tri_Node.h */
#ifndef _TRI_NODE
#define _TRI_NODE

template<class ItemType>
class TriNode
{
private:
   ItemType smallItem, largeItem;   // Data portion
   TriNode<ItemType>* leftChildPtr; // Left-child pointer
   TriNode<ItemType>* midChildPtr;  // Middle-child pointer
   TriNode<ItemType>* rightChildPtr; // Right-child pointer

public:
   TriNode();
   TriNode(const ItemType& anItem);
   TriNode(const ItemType& anItem, TriNode<ItemType>* leftPtr,
           TriNode<ItemType>* midPtr, TriNode<ItemType>* rightPtr);

   bool isLeaf() const;
   bool isTwoNode() const;
   bool isThreeNode() const;

   ItemType getSmallItem() const;
   ItemType getLargeItem() const;

   void setSmallItem(const ItemType& anItem);
   void setLargeItem(const ItemType& anItem);

   TriNode<ItemType>* getLeftChildPtr() const;
   TriNode<ItemType>* getMidChildPtr() const;
   TriNode<ItemType>* getRightChildPtr() const;

   void setLeftChildPtr(TriNode<ItemType>* leftPtr);
   void setMidChildPtr(TriNode<ItemType>* midPtr);
   void setRightChildPtr(TriNode<ItemType>* rightPtr);
}; // end TriNode
#include "TriNode.h"
#endif
```

## 19.2.1 遍历 2-3 树

2-3 树上遍历、检索、插入和删除操作的算法均为递归算法。你可以通过将这些递归算法的基本情况定义为叶节点而非空子树，来避免分散注意力的实现细节。因此，这些算法必须假设它们不会接收空树作为参数。

你可以通过对二叉树执行中序遍历的类似操作，以有序方式遍历 2-3 树：

```
// Traverses a nonempty 2-3 tree in sorted order
inorder(23Tree: TwoThreeTree): void
if (23Tree's root node r is a leaf)
    Visit the data item(s)
else if (r has two data items)
    inorder(left subtree of 23Tree's root)
    Visit the first data item
    inorder(middle subtree of 23Tree's root)
    Visit the second data item
    inorder(right subtree of 23Tree's root)
}
else // r has one data item
{
    inorder(left subtree of 23Tree's root)
    Visit the data item
    inorder(right subtree of 23Tree's root)
}
```

## 19.2.2 搜索 2-3 树

2-3 树中项的排序方式与二叉搜索树类似，这使你能够高效地在 2-3 树中搜索特定项。事实上，2-3 树的检索操作与二叉搜索树的检索操作非常相似，如以下伪代码所示：

```
// Locates the value target in a nonempty 2-3 tree. Returns either the located
// entry or throws an exception if such a node is not found.
findItem(23Tree: TwoThreeTree, target: ItemType): ItemType
if (target is in 23Tree's root node r)
{ // The item has been found
    treeItem = the data portion of r
    return treeItem // Success
}
else if (r is a leaf)
    throw NotFoundException // Failure
// Else search the appropriate subtree
else if (r has two data items)
{
    if (target < smaller item in r)
        return findItem(r's left subtree, target)
    else if (target < larger item in r)
        return findItem(r's middle subtree, target)
    else
        return findItem(r's right subtree, target)
}
else // r has one data item
{
    if (target < r's data item)
        return findItem(r's left subtree, target)
    else
        return findItem(r's right subtree, target)
}
```

你可以以大约相同的效率搜索 2-3 树和最短的二叉搜索树，因为

- 含 n 个节点的二叉搜索树的高度不低于 ⌈log2(n + 1)⌉
- 含 n 个节点的 2-3 树的高度不高于 ⌈log2(n + 1)⌉
- 2-3 树中的节点最多包含两个项

然而，搜索 2-3 树并不比搜索二叉搜索树更高效。这一观察可能会让你感到惊讶，毕竟 2-3 树的节点可以有三个子节点，因此 2-3 树确实可能比最短的可能二叉搜索树更矮。虽然这是事实，但高度方面的优势被将给定值与两个值（而非仅一个值）进行比较所需的额外时间所抵消。换句话说，虽然你在搜索 2-3 树时可能访问更少的节点，但可能需要在每个节点上进行更多比较。因此，搜索 2-3 树中特定项所需的比较次数，大约等于搜索尽可能平衡的二叉搜索树所需的比较次数。这个数大约为 log2 n。

如果你可以以大约相同的效率搜索 2-3 树和平衡的二叉搜索树，那么为什么还要使用 2-3 树呢？因为尽管在插入和删除操作面前维护二叉搜索树的平衡很困难，但维护 2-3 树的形状相对简单。例如，考虑图 19-5 中的两棵树。第一棵树是一棵二叉

搜索 2-3 树的时间复杂度为 O(log n)

### 图 19-5 (a) 一棵平衡的二叉搜索树；(b) 含相同条目的一棵 2-3 树

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_599_0.png)

### 图 19-6 (a) 图 19-5a 的二叉搜索树在插入值序列 32 到 39 后的样子；(b) 图 19-5b 的 2-3 树在相同插入后的样子

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_600_0.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_600_1.png)

> 维护 2-3 树的形状相对容易

搜索树，第二棵是 2-3 树。两棵树包含相同的数据项。二叉搜索树已尽可能平衡，因此你可以以大约相同的效率在这两棵树中搜索某一项。然而，如果你对二叉搜索树执行一系列插入操作——使用第 16 章的插入算法——该树可能会迅速失去平衡，如图 19-6a 所示。在此示例中，我们按数值顺序插入了 32 到 39 的值。如你很快将看到，你可以对 2-3 树执行相同的插入序列而不会导致树的形状退化——它将保留其结构，如图 19-6b 所示。

插入到图 19-5a 的二叉搜索树中的新值（32 到 39）在图 19-6a 中沿着一条路径出现。这些插入将二叉搜索树的高度从 4 增加到 12——增加了 8。另一方面，新值已分布在图 19-6b 的 2-3 树中。因此，生成的树的高度仅比图 19-5b 中原始 2-3 树的高度大 1。接下来，我们将演示将这些值插入原始 2-3 树的过程。

