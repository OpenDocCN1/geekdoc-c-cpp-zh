
## 12. 基于栈二二查找

模仿 18.7 节的技术，使用栈消除二分查找算法中的递归。

## 13. 基于栈的斐波那契函数

使用栈消除 14.4 节讨论的斐波那契函数的递归。

# 第19章 二叉树

# 目录

| 19.1 二叉树的定义与应用 | 19.3 二叉搜索树的模板考虑因素 |
| 19.2 二叉搜索树的操作 | 19.4 综合运用：谱系树 |

## 19.1 二叉树的定义与应用

**概念：** 二叉树与链表的区别在于，链表中的节点最多可以有一个后继节点，而二叉树中的节点可以多有两个后继节点。

*二叉树*是节点集合，其中每个节点都关联到最多两个后继节点，分别称为*左孩子*和*右孩子*。二叉树中的并非每个节点都有两个孩子：可以省略其中一个或两个两个节点。二叉树中没有子节点的节点被称为*叶子节点*。

拥有子节点的节点被称为其子节点的*父节点*。对于一个非空节点集合要成为二叉树，每个节点必须至少有一个父节点，且恰恰有一个节点没有父节点。没有父节点的节点被称为二叉树的*根*。空节点集合被视为构成一个空二叉树。

链表与二叉树之间存在某些相似之处。树的根对应于表的头，二叉树节点的孩子对应于链中的后继节点，二叉树节点的父节点对应于链中节点的前驱节点。当然，空表的等价物是空二叉树。

## 二叉树的实现

二叉树用于在节点中存储值。因此，二叉树中的节点将是一个结构体或类对象，它包含一个用于存储值的成员，以及两个指向该节点左孩子和右孩子的节点的成员：

二叉树本身由指向树根节点的指针来表示。图19-1展示了一个二叉树的示例（未显示节点中存储的值）。如果某个节点不具备相应的子节点，则该节点中的左指针或右指针被设置为 `nullptr`。

# 图 19-1

![](img/1c095ef63c71a34f9802f104f947be57_1160_0.png)

二叉树之所以被称为树，是因为它们像一棵倒过来的树。任何非空树都可以划分为它的根节点、左子树和右子树。直观上，子树是树的一整条分支，从一个特定的节点向下。图19-2显示了图19-1所示二叉树的左子树。

## 二叉树的应用

当结构包含大量信息时，对线性数据结构（如数组或标准链表）进行搜索是缓慢的。这是由于线性数据结构的顺序性质决定的。二叉树及其泛化是搜索大量信息的极佳数据结构。它们通常用于数据库应用程序，以组织索引数据库记录的键值。当用于辅助

## 19.1 二叉树的定义与应用

图 19-2

![](img/1c095ef63c71a34f9802f104f947be57_1161_0.png)

搜索时，二叉树被称为二叉搜索树。二叉搜索树是本章的重点。

信息在二叉搜索树中的存储方式使得在树中搜索信息变得简单。例如，看图19-3。

图 19-3

![](img/1c095ef63c71a34f9802f104f947be57_1161_1.png)

## 第19章 二叉树

该图描绘了一个二叉搜索树。信息在二叉搜索树中的存储方式使得在树中搜索信息变得简单。例如，看图19-3。

二叉搜索树是本章的重点。该图描绘了一个二叉搜索树。信息在二叉搜索树中的存储方式使得在树中搜索信息变得简单。例如，看图19-3。

二叉搜索树是本章的重点。该图描绘了一个二叉搜索树。信息在二叉搜索树中的存储方式使得在树中搜索信息变得简单。例如，看图19-4展示展示了二叉搜索树的搜索模式。

图19-4

![](img/1c095ef63c71a34f9802f104f947be57_1162_0.png)

这种搜索二叉树的方式让人联想到在排序数组上的搜索。假设二叉树是平衡的（即每个节点的左右子树节点数大致相同），搜索每一步都会将待搜索树的大小减半。这使得可以用较少的步骤搜索包含大量信息的二叉树。

检查点

- 19.1 描述二叉树与链表的区别。
- 19.2 什么是根节点？
- 19.3 什么是孩子节点？
- 19.4 什么是节点？
- 19.5 什么是子树？
- 19.6 为什么二叉树适用于需要搜索大量信息的算法？

## 19.2 二叉搜索树的操作

**概念：** 二叉搜索树上可以执行许多操作，创建二叉搜索树、插入、查找和删除节点。

在本节中，你将学习二叉搜索树的一些操作。我们将学习一个存储整数值的简单二叉树类。

## 创建二叉搜索树

我们将使用 `IntBinaryTree` 类演示基本的二叉树操作。我们二叉树节点的类声明如下：

```cpp
struct TreeNode {
    int value;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int value, TreeNode *left = nullptr, TreeNode *right = nullptr) {
        value = value;
        left = left;
        right = right;
    }
};
```

注意树的每个节点都有一个值成员，以及两个用于跟踪左和右孩子的指针。该类将用于构建树。

```cpp
class IntBinaryTree {
private:
    TreeNode *root;
    void destroySubtree(TreeNode *node);

public:
    IntBinaryTree() {
        root = nullptr;
    }
    ~IntBinaryTree() {
        destroySubtree(root);
    }
    void insert(int num);
    bool search(int num) const;
    void remove(int num);
    void inOrder() const;
    void preOrder() const;
    void postOrder() const;
};
```

# 图 19-S

![](img/1c095ef63c71a34f9802f104f947be57_1166_0.png)

# 二叉搜索树操作实现

许多二叉树操作都有天然的递归实现。这是因为二叉树本质上是一种递归的数据结构：每个非空二叉树都由一个根节点以及左右两个子树组成，而这两个子树本身也是二叉树。许多二叉树操作可以通过对根节点进行某些处理，然后递归地对左右子树执行该操作来实现。例如，如果根节点由一个指针表示

```cpp
TreeNode*;
```

那么根的值将是 `tree->value`，而左右子树分别由 `tree->left` 和 `tree->right` 提供。递归操作必须首先处理 `tree->value`，然后递归对 `tree->left` 和 `tree->right` 进行操作。

# 插入元素

向二叉搜索树中插入数字的工作是由私有成员函数完成的

```cpp
insert(TreeNode *tree, int num)
```

该函数接收一个二叉搜索树根节点的指针和一个要插入树的数字 `num`。它使用递归策略：如果二叉树为空（这是递归中发生的情况），它会创建一个新的 `TreeNode` 对象，其 `value` 成员为给定的数字，并将其设置为树的根节点：

![](img/1c095ef63c71a34f9802f104f947be57_1166_1.png)

```cpp
if (!tree)
{
  tree = new TreeNode(num);
  return;
}
```

然而，如果二叉搜索树不为空，`insert` 函数会将 `num` 与根节点中的值 `tree->value` 进行比较。根据此比较的结果，将新值递归地插入到左子树或右子树中：

```cpp
if (num < tree->value)
  insert(tree->left, num);
else
  insert(tree->right, num);
```

这里是完整的函数：

```cpp
void IntBinaryTree::insert(TreeNode *tree, int num)
{
  // 如果树为空，创建一个新节点并将其设为
  // 树的根
  if (!tree)
  {
    tree = new TreeNode(num);
    return;
  }
  // 如果 num 已经在树中：返回
  if (tree->value == num)
    return;
  
  // 树不为空：将新节点插入到
  // 左或右子树
  if (num < tree->value)
    insert(tree->left, num);
  else
    insert(tree->right, num);
}
```

注意函数传递的是指针的引用，因为该指针可能需要被函数修改。这也是为什么 `remove` 和 `delete` 函数通过引用传递参数的原因。

> 注意：图 19-5 所示树的形状取决于值插入的顺序。根节点持有值 5，是因为它是第一个被插入的值。通过单步执行函数，你可以看到其他节点是如何出现在它们所示的位置的。

![](img/1c095ef63c71a34f9802f104f947be57_1167_0.png)

# 遍历树

遍历非空二叉树并处理每个节点值的常用方法有：中序遍历、前序遍历和后序遍历。这些方法最好都实现为递归函数。算法描述如下。

# 中序遍历

- 1. 遍历节点的左子树。
- 2. 处理节点的数据。
- 3. 遍历节点的右子树。
- 前序遍历
- 1. 处理节点的数据。
- 2. 遍历节点的左子树。
- 3. 遍历节点的右子树。
- 后序遍历
- 1. 遍历节点的左子树。
- 2. 遍历节点的右子树。
- 3. 处理节点的数据。

`IntBinaryTree` 类可以使用所有算法显示树中的所有值。这些算法通过以下内联公有成员函数启动：

```cpp
void showInOrder(void)
  { displayInOrder(root); }
void showPreOrder()
  { displayPreOrder(root); }
void showPostOrder()
  { displayPostOrder(root); }
```

每个公共成员函数都调用一个递归的私有成员函数，并将根指针作为参数传递。递归函数非常简单且直接：

```cpp
void IntBinaryTree::displayInOrder(TreeNode *tree) const
  {
    if (tree)
    {
      displayInOrder(tree->left);
      cout << tree->value << " ";
      displayInOrder(tree->right);
    }
}
```

```cpp
void IntBinaryTree::displayPreOrder(TreeNode *tree) const
  {
    if (tree)
    {
      cout << tree->value << " ";
      displayPreOrder(tree->left);
      displayPreOrder(tree->right);
    }
}
```

```cpp
void IntBinaryTree::displayPostOrder(TreeNode *tree) const
  {
    if (tree)
    {
      displayInOrder(tree->left); // 等等，原文这里有两个 displayPostOrder(tree->left)？ 
                                  // 根据标准逻辑进行修正：
      displayPostOrder(tree->left);
      displayPostOrder(tree->right);
      cout << tree->value << " ";
    }
}
```

# 19.2 二叉搜索树

# 搜索树

`IntBinarySearchTree` 类有一个公有成员函数 `search`，如果在树中找到该值则返回 `true`，否则返回 `false`。该函数从根节点开始。函数将 `num`（要查找的值）与当前正在搜索的根节点的值进行比较。如果值不匹配，函数继续搜索左子树或右子树。

```cpp
bool IntBinaryTree::search(int num) const
{
    TreeNode *tree = root;
    while (tree)
    {
        if (tree->value == num)
            return true;
        else if (num < tree->value)
            tree = tree->left;
        else
            tree = tree->right;
    }
    return false;
}
```

# 程序 19-3

```cpp
// 该程序构建包含 5 个节点的二叉树。
// 搜索函数判断 3 是否在树中。
#include <iostream>
#include "IntBinaryTree.h"
using namespace std;

int main()
{
    IntBinaryTree tree;
    cout << "插入数字 5 8 3 12 9。\n";
    tree.insert(5);
    tree.insert(8);
    tree.insert(3);
    tree.insert(12);
    tree.insert(9);

    cout << "\n中序遍历: ";
    tree.showInOrder();
    cout << "\n前序遍历: ";
    tree.showPreOrder();
    cout << "\n后序遍历: ";
    tree.showPostOrder();

    if (tree.search(3))
        cout << "\n树中找到了 3。\n";
    else
        cout << "\n树中未找到 3。\n";

    return 0;
}
```

输出

插入数字 5 8 3 12 9.

中序遍历: 3 5 8 9 12 

前序遍历: 5 3 8 9 12 

后序遍历: 3 12 9 8 5 

树中找到了 3.

# 删除元素

要删除元素，我们首先找到包含元素的节点并删除该节点。删除节点的方法取决于其子节点的数量。如果 X 没有子节点，我们首先找到它的父节点，将父节点的子指针链接设置为 `nullptr`，然后释放为 X 分配的内存。如果 X 是树的根，我们刚刚描述的方法将不再适用。在这种情况下，我们只需删除 X 并将树根的指针设置为 `nullptr`。

删除非叶子节点的程序必须确保该节点连接的子树仍然作为树的一部分。该程序根据被删除节点拥有一个还是两个子节点而异。图 19-6 显示了一个正准备删除带有一个子树节点的树。

![](img/1c095ef63c71a34f9802f104f947be57_1170_0.png)

图 19-7 显示了我们将如何将节点的子树与其父节点重新连接。

![](img/1c095ef63c71a34f9802f104f947be57_1171_1.png)

然而，当我们要删除的节点有两个子树时，问题就不那么容易解决了。例如，请看 19-8。

# 图 19-8

![](img/1c095ef63c71a34f9802f104f947be57_1172_0.png)

显然，我们不能将该节点的两个子树都连接到它的父节点，必须有其他解决方案。解决这个问题的一种方法是将节点的右子树连接到父节点，然后在右子树中找到一个位置来挂载左子树。结果如图 19-9 所示。注意，在将左子树接到右子树时，我们必须注意保持二叉树的搜索属性。

# 图 19-9

![](img/1c095ef63c71a34f9802f104f947be57_1172_1.png)

## 19.2 二叉搜索树操作

从 `IntBinaryTree` 对象中删除一个值是通过调用公共成员函数 `remove` 完成的，该函数反过来又调用同名的私有成员函数。后者函数接收一个二叉搜索树（其根节点）和一个要从树中删除的值：

该函数使用了递归策略。如果树为空，它会立即返回。否则，如果 `num` 小于根节点中存储的值，函数将递归地从左子树中删除 `num`；但如果 `num` 大于，函数将递归地从右子树中删除 `num`。在根节点中找到 `num` 的将交给一个函数

```
remove(TreeNode *tree, int num)
```

以下是 `remove` 的代码：

```
void IntBinaryTree::remove(TreeNode *tree, int num)
{
    if (tree == nullptr) return;
    if (num < tree->value)
        remove(tree->left, num);
    else if (num > tree->value)
        remove(tree->right, num);
    else
        // 我们找到了要删除的节点。
        makeDeletion(tree);
}
```

`makeDeletion` 函数的设计用于删除作为参数传递的二叉搜索树的根节点，留下一个由剩余节点组成的二叉搜索树。我们来看下 `makeDeletion` 背后的逻辑。有几种情况：

- 1. 传递给 `makeDeletion` 的树根节点没有孩子。在这种情况下，我们删除根节点并将树替换为 `nullptr`。
- 2. 树的根节点只有一个孩子。在这种情况下，我们删除根节点并将树替换为被删除根节点的子节点：
