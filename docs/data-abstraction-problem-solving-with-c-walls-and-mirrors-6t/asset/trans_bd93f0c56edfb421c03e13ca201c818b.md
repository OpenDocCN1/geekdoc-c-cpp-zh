

递归方法 removeLeftmostNode，在 N 有两个子节点时由 removeNode 调用，也使用此策略来删除包含要移除项的节点的中序后继。

本章末尾的练习 12 描述了一种更简单的删除算法。然而，该算法倾向于增加树的高度，而且，如你稍后将看到的，高度增加会降低搜索树的效率。

### 图 16-14 递归删除节点 N

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_506_0.png)

### 问题 8 鉴于第 15 章图 15-18 中的二叉搜索树，跟踪从树中移除以下每个值时的删除算法。每次都从原始树开始。

- a. 70
- b. 20
- c. 60

### 检索条目。

通过改进搜索算法，你可以实现操作 getEntry。回顾第 15 章第 15.3.2 节，搜索算法如下

```
// Searches a binary search tree for a given target value.
search(binTree: BinarySearchTree, target: ItemType)
    if (binTree is empty)
        The desired item is not found
    else if (target == data item in the root of binTree)
        The desired item is found
    else if (target < data item in the root of binTree)
        search(Left subtree of binTree, target)
    else
        search(Right subtree of binTree, target)
```

我们可以如下改进此算法：

```
// Locates the node in the binary search tree to which subTreePtr points that contains
// the value target. Returns either a pointer to the located node or nullPtr if such a
// node is not found.
findNode(subTreePtr: BinaryNodePointer, target: ItemType): BinaryNodePointer
    if (subTreePtr == nullPtr) // Not found
        return nullPtr
    else if (subTreePtr->getItem() == target) // Found
        return subTreePtr
    else if (subTreePtr->getItem() > target)
        // Search left subtree
        return findNode(subTreePtr->getLeftChildPtr(), target)
    else
        // Search right subtree
        return findNode(subTreePtr->getRightChildPtr(), target)
```

如果存在所需值的项，操作 getEntry 必须返回该项；否则必须抛出异常 NotFoundException。因此，该方法调用 findNode 并检查其返回值。如果找到所需目标，getEntry 返回它。如果 findNode 返回 nullPtr，getEntry 抛出异常。

> **注意：遍历**
> 
> 二叉搜索树的遍历与二叉树的遍历相同。回顾第 15 章，二叉搜索树的中序遍历将按照条目的排序顺序访问树的节点。

### 16.3.2 类 BinarySearchTree

类 BinarySearchTree 的 C++ 链式定义在清单 16-4 中给出。请注意实现递归算法的 protected 方法。这些方法不是 public 的，因为客户端无法访问节点指针。这些方法可以是 private 的，但将其设为 protected 使派生类能够直接使用它们。

如第 15 章第 15.3.1 节所述，ADT 二叉树和 ADT 二叉搜索树有许多共同的方法。这一观察不应让你感到惊讶，因为二叉搜索树是一种二叉树。出于此原因，我们从 BinaryNodeTree 派生了 BinarySearchTree。

```
LISTING 16-4 A header file for the link-based implementation of the class BinarySearchTree
/** Link-based implementation of the ADT binary search tree.
@file BinarySearchTree.h */
#ifndef _BINARY_SEARCH_TREE
#define _BINARY_SEARCH_TREE

#include "BinaryTreeInterface.h"
#include "BinaryNode.h"
#include "BinaryNodeTree.h"
#include "NotFoundException.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class BinarySearchTree : public BinaryNodeTree<ItemType>
{
private:
   BinaryNode<ItemType>* rootPtr;
protected:
////////////////////////////////////////////////////////
//      Protected Utility Methods Section:
//      Recursive helper methods for the public methods.
////////////////////////////////////////////////////////
// Recursively finds where the given node should be placed and
// inserts it in a leaf at that point.
BinaryNode<ItemType>* insertInorder(BinaryNode<ItemType>* subTreePtr,
                                    BinaryNode<ItemType>* newNode);
// Removes the given target value from the tree while maintaining a
// binary search tree.
BinaryNode<ItemType>* removeValue(BinaryNode<ItemType>* subTreePtr,
                                  const ItemType target,
                                  bool& success);
// Removes a given node from a tree while maintaining a
// binary search tree.
BinaryNode<ItemType>* removeNode(BinaryNode<ItemType>* subTreePtr);
// Removes the leftmost node in the left subtree of the node
// pointed to by nodePtr.
// Sets inorderSuccessor to the value in this node.
// Returns a pointer to the revised subtree.
BinaryNode<ItemType>* removeLeftmostNode(BinaryNode<ItemType>* subTreePtr,
                                         ItemType& inorderSuccessor);
// Returns a pointer to the node containing the given value,
// or nullptr if not found.
BinaryNode<ItemType>* findNode(BinaryNode<ItemType>* treePtr,
                               const ItemType& target) const;

public:
// --------------------------------------------------
// Constructor and Destructor Section.
// --------------------------------------------------
BinarySearchTree();
BinarySearchTree(const ItemType& rootItem);
BinarySearchTree(const BinarySearchTree<ItemType>& tree);
virtual ~BinarySearchTree();
// --------------------------------------------------
// Public Methods Section.
// --------------------------------------------------
bool isEmpty() const;
int getHeight() const;
int getNumberOfNodes() const;
ItemType getRootData() const throw(PrecondViolatedExcep);
void setRootData(const ItemType& newData) const
      throw(PrecondViolatedExcep)
bool add(const ItemType& newEntry);
bool remove(const ItemType& anEntry);
void clear();
ItemType getEntry(const ItemType& anEntry) const
      throw(NotFoundException);
bool contains(const ItemType& anEntry) const;
// --------------------------------------------------
// Public Traversals Section.
// --------------------------------------------------
void preorderTraverse(void visit(ItemType&)) const;
void inorderTraverse(void visit(ItemType&)) const;
void postorderTraverse(void visit(ItemType&)) const;
// --------------------------------------------------
// Overloaded Operator Section.
// --------------------------------------------------
BinarySearchTree<ItemType>&
operator=(const BinarySearchTree<ItemType>& rightHandSide);
}; // end BinarySearchTree
#include "BinarySearchTree.cpp"
#endif
```

## 16.4 将二叉搜索树保存到文件中

想象一个维护你朋友和亲戚姓名、地址和电话号码的程序。在程序运行期间，你可以输入一个姓名并获取该人的地址和电话号码。如果你终止程序执行，程序必须以一种稍后可以恢复的形式保存其人员数据库。

### 图 16-15 插入 60、20、10、40、30、50 和 70 后最初为空的二叉搜索树

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_510_0.png)

如果程序使用二叉搜索树来表示数据库，则必须将树的数据保存在文件中，以便稍后恢复树。这里将考虑两种保存和恢复二叉搜索树的不同算法。第一种算法将二叉搜索树恢复到其原始形状。第二种算法将二叉搜索树恢复到平衡形状。

### 使用先序遍历将二叉搜索树保存到文件中，并通过 add 恢复其原始形状

**保存二叉搜索树并将其恢复到原始形状。** 第一种算法将二叉搜索树恢复到保存前完全相同的形状。例如，考虑图 16-15 中的树。如果你以先序保存树，则得到序列 60, 20, 10, 40, 30, 50, 70。然后，如果你使用 add 方法将这些值插入最初为空的二叉搜索树，你将得到原始树。

平衡二叉搜索树提高了 ADT 操作的效率

### 保存二叉搜索树并将其恢复到平衡形状。将二叉搜索树保存到文件后，你是否一定希望恢复的树具有其原始形状？回想一下，你可以使用给定的一组数据项来创建形状不同的多个二叉搜索树。虽然二叉搜索树的形状对 ADT 操作的正确性完全没有影响，但它会影响这些操作的效率。如果二叉搜索树是平衡的，则可确保操作高效。

将二叉搜索树恢复到平衡形状的算法出奇地简单。事实上，你甚至可以保证恢复的树具有最小高度——这是比平衡更强的条件。为了深入了解解决方案，请考虑一棵满树，因为它是平衡的。如果你使用中序遍历将满树保存到文件中，则文件将按排序顺序排列，如图 16-16 所示。

对于某个高度 h，恰好有 n = 2^h - 1 个节点的满树，其根中包含数据项的精确中间值。根的左子树和右子树各是具有 2^(h-1) - 1 个节点的满树（即 n - 1 的一半，因为 n 是奇数，或等价地，n / 2）。因此，你可以使用以下递归算法创建具有 n 个节点的满二叉搜索树，前提是你事先知道或可以确定 n。

### 构建满二叉搜索树

```
// Builds a full binary search tree from n sorted values in a file.
// Returns a pointer to the tree's root.
readFullTree(n: integer): BinaryNodePointer
{
   if (n > 0)
   {
      // Get the root
      treePtr = pointer to new node with nullPtr as its child pointers
      rootItem = next item from file
      treePtr->setItem(rootItem)
```

