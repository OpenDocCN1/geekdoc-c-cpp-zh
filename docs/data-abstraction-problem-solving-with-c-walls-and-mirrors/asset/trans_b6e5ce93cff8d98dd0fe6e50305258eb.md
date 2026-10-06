
递归方法 `removeLeftNode` 在 N 有两个子节点时被 `removeNode` 调用，它也使用这种策略来删除包含要删除项目的中序继节点。

本章末尾的练习 12 描述了一种更简单的删除算法。然而，算法倾向于增加树的高度，而且正如你以后看到的，高度的增加会降低搜索树的效率。

# 图 16-14 节点 N 的递归删除

![](img/d0cb86b2f18b2db569968ad7c743510e_506_0.png)
![](img/d0cb86b2f18b2db569968ad7c743510e_506_1.png)
![](img/d0cb86b2f18b2db569968ad7c743510e_506_2.png)

# 基于链的二叉搜索树 ADT 实现 481

**问题 8** 给定第 15 章图 15–18 中的二叉搜索树，追踪从树中删除以下任一值时的删除算法。每次都从原始树开始。

- a. 70
- b. 20
- c. 60

检索条目。通过优化搜索算法，你可以实现 `getEntry` 操作。回想第 15 章 15.3.2 节，搜索算法为：

```cpp
// 在二叉树中搜索给定的目标值。
search(binTree: BinarySearchTree, target: ItemType)

if (binTree is empty)
    // 未找到所需的项目
else if (target == data item in the root of binTree)
    // 找到了所需的项目
else if (target < data item in the root of binTree)
    search(Left subtree of binTree, target)
else
    search(Right subtree of binTree, target)
```

我们可以按照如下方式优化该算法：

```cpp
// 在二叉树中定位到 subTree 指向的具有
// target 值的节点。返回指向找到找到的指针，如果未找到
// 节点则返回 nullptr。
findNode(subTree: BinaryNodePointer, target: ItemType): BinaryNodePointer
if (subTree == nullptr) // 未找到
    return nullptr;
else if (subTree->getItem() == target) // 找到
    return subTree;
else if (subTree->getItem() < target)
    // 搜索左子树
    return findNode(subTree->getChildPtr(), target)
else
    // 搜索右子树
    return findNode(subTree->getRightChildPtr(), target);
```

如果存在所需值的项目，操作 `getEntry` 必须返回它；否则必须抛出异常 `NotFoundException`。因此，该方法调用 `findNode` 并检查其返回值。如果找到了所需的目标，`getEntry` 返回它。如果 `findNode` 返回 `nullptr`，`getEntry` 抛出异常。

> 注意：二叉树的遍历与二叉树的遍历是相同的。回想第 15 章，二叉搜索树的中序遍历将根据条目的排序顺序访问树的节点。

## 16.3.2 BinarySearchTree 类

列表 16-4 给出了 `BinarySearchTree` 的 C++ 基于链的定义。注意实现递归算法的保护方法（protected）。这些方法不是公共的，因为客户端无法访问节点指针。这些方法本可以是私有的，将它们设为保护的允许派生类直接使用它们。

正如第 15 章 15.3.1 节所述，ADT 二叉树和二叉搜索树有许多共同方法。这一观察不会让你感到意外，因为二叉搜索树是一种二叉树。由于这个原因，我们从 `BinaryTreeNode` 继承。

列表 16-4 二叉搜索树的基于链的头文件

```cpp
/* 二叉搜索树的基于链实现 */
#ifndef BINARY_SEARCH_TREE
#define BINARY_SEARCH_TREE

#include "TreeInterface.h"
#include "BinaryNode.h"
#include "TreeNode.h"
#include "NotFoundException.h"
#include "PrecondViolated.h"

template<class ItemType>
class BinarySearchTree : public BinaryNode<ItemType>{
private:
    BinaryNode<ItemType>* rootPtr;
protected:
    // 保护工具方法：
    // 用于公共方法的递归方法。

    // 递归查找节点应该插入的位置
    // 并将其插入正确位置。
    BinaryNode<ItemType>* insertInorder(BinaryNode<ItemType>* subtreePtr, newNode);

    // 从树中删除给定的目标值
    // 并维护二叉搜索树。
    BinaryNode<ItemType>* removeValue(BinaryNode<ItemType>* subtreePtr, const ItemType target, bool& success);

    // 从树中删除节点
    // 并维护二叉搜索树。
    BinaryNode<ItemType>* removeNode(BinaryNode<ItemType>* nodePtr);

    // 删除 nodePtr 指向子树中最左侧的节点。
    // 将节点的值设置为 inorderSuccess。
    // 返回修改后的子树。
    BinaryNode<ItemType>* removeLeftmostNode(BinaryNode<ItemType>* subtreePtr, ItemType& inorderSuccess);

public:
    // 构造函数和析构函数部分。
    BinarySearchTree();
    BinarySearchTree(const ItemType& rootItem);
    BinarySearchTree(const BinarySearchTree<ItemType>& tree);
    virtual ~BinarySearchTree();

    // 公共方法部分。
    bool isEmpty() const;
    int getHeight() const;
    int getNumberOfNodes() const;
    ItemType getRootData() const throw(PrecondViolated);
    void setRootData(const ItemType& newData) const throw(PrecondViolated);
    bool add(const ItemType& newEntry);
    bool remove(const ItemType& anEntry);
    void clear();
    ItemType getEntry(const ItemType& anEntry) const throw(NotFoundException);
    bool contains(const ItemType& anEntry) const;

    // 公共遍历部分。
    void preorderTraverse(void visit(ItemType&)) const;
    void inorderTraverse(void visit(ItemType&)) const;
    void postorderTraverse(void visit(ItemType&)) const;

    // 重载运算符部分。
    BinarySearchTree<ItemType>&
    operator=(const BinarySearchTree<ItemType>& rightHandSide);
);// end BinarySearchTree
#include "BinarySearchTree.cpp"
#endif
```

## 16.4 将二叉搜索树保存到文件

想象一个维护朋友和亲属姓名、地址和电话的程序。在程序运行时，你可以输入姓名并获取该人的地址和电话。如果你终止程序执行，程序必须将其人物数据库保存为一种可以在以后恢复的形式。

# 第 16 章 树的实现

图 16-15 插入 60, 20, 10, 40, 30, 50, 70 后的初始空二叉树

![](img/d0cb86b2f18b2db569968ad7c743510e_510_0.png)
