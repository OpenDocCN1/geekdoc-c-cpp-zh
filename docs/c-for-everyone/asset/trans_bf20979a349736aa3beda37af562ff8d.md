

![](img/5e58fb4c840712efd6ed6fa82bb97f57_605_0.png)

**图6** 经过五次插入后的二叉搜索树

我们想向其中插入一个新元素 Romeo。

`tree.add("Romeo");`

从根节点 Juliet 开始。Romeo 在 Juliet 之后，因此你移动到右子树。你遇到节点 Tom。Romeo 在 Tom 之前，因此你移动到左子树。但不存在左子树。因此，你将一个新的 Romeo 节点插入为 Tom 的左孩子（见图6）。

你应该确信得到的树仍然是一棵二叉搜索树。当插入 Romeo 时，它最终必然是 Juliet 的右后代——这就是二叉搜索树条件对于根节点 Juliet 的意义。根节点并不关心新节点在右子树中的最终位置。继续移动到 Juliet 的右孩子 Tom，它所关心的只是新节点 Romeo 最终位于其左侧的某个位置。它的左侧没有任何东西，所以 Romeo 成为新的左孩子，得到的树又是一棵二叉搜索树。

以下是 `BinarySearchTree` 类的 insert 成员函数的代码：

```cpp
void BinarySearchTree::insert(string data)
{
    TreeNode* new_node = new TreeNode;
    new_node->data = data;
    new_node->left = NULL;
    new_node->right = NULL;
    if (root == NULL)
    {
        root = new_node;
    }
    else
    {
        root->insert_node(new_node);
    }
}
```

要在一个二叉搜索树中插入一个值，就递归地将其插入左子树或右子树。

如果树为空，只需将其根节点设置为新节点。否则，你知道新节点必须插入到某个节点内部，你可以让根节点执行插入操作。该节点对象调用 `TreeNode` 类的 `insert_node` 成员函数。该成员函数检查新对象是否小于节点中存储的对象。如果是，则将该元素插入左子树。如果它大于节点中存储的对象，则插入右子树：

```cpp
void TreeNode::insert_node(TreeNode* new_node)
{
    if (new_node->data < data)
    {
        if (left == NULL)
        {
            left = new_node;
        }
        else
        {
            left->insert_node(new_node);
        }
    }
    else if (data < new_node->data)
    {
        if (right == NULL)
        {
            right = new_node;
        }
        else
        {
            right->insert_node(new_node);
        }
    }
}
```

让我们跟踪在将 Romeo 插入图5中的树时对 `insert_node` 的调用。对 `insert_node` 的第一次调用是

```
root->insert_node(newNode)
```

因为 root 指向 Juliet，你将 Juliet 与 Romeo 比较，发现必须调用

```
root->right->insert_node(newNode)
```

节点 `root->right` 包含 Tom。再次比较数据值（Tom 与 Romeo），发现现在必须向左移动。由于 `root->right->left` 为 NULL，将 `root->right->left` 设置为 `new_node`，插入就完成了（见图6）。

# 14.2.3 从二叉搜索树中删除元素

考虑从树中删除一个节点的任务。当然，我们必须首先找到要删除的节点。由于二叉搜索树的特征性质，这是一件简单的事情。将要删除的数据值与根节点中存储的数据值进行比较。如果较小，则继续在左子树中查找。否则，继续在右子树中查找。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_607_0.png)

> 当从二叉搜索树中删除只有一个孩子的节点时，该孩子替换要删除的节点。

现在让我们假设我们已经找到了需要删除的节点。首先，让我们考虑一个简单的情况：该节点只有一个孩子（见图7）。要删除该节点，只需修改指向该节点的父链接，使其改为指向孩子。

如果要删除的节点根本没有孩子，那么父链接直接设置为 NULL。

如果要删除的节点有两个孩子，这种情况更具挑战性。与其删除该节点，不如用树中下一个更大的值替换其数据值。这种替换保持了二叉搜索树的性质。（或者，你可以使用左子树中的最大元素——见练习 P14.11）。

图7  删除只有一个孩子的节点

![](img/5e58fb4c840712efd6ed6fa82bb97f57_607_1.png)

图8
删除有两个孩子的节点

如果二叉搜索树是平衡的，那么插入一个元素需要 O(log(n)) 时间。

有一些更复杂的树结构，其函数始终保持树的平衡。在这些树结构中，可以保证查找、添加和删除元素需要 O(log(n)) 时间。标准 C++ 库使用 *红黑树*（平衡二叉树的一种特殊形式）来实现集合和映射。

表1 总结了数组或向量、链表和平衡二叉树上基本操作的性能。

**表1 — 容器操作的执行时间**

| 操作 | 数组/向量 | 链表 | 平衡二叉树 |
|---|---:|---:|---:|
| 在末尾添加/删除元素 | O(1) | O(1) | 不适用 |
| 在中间添加/删除元素 | O(n) | O(1) | O(log(n)) |
| 获取第 k 个元素 | O(1) | O(k) | 不适用 |
| 查找值 | O(n) | O(n) | O(log(n)) |

# 14.2.4 树的遍历

一旦数据被插入二叉搜索树，按排序顺序打印所有元素就变得异常简单。你知道任何节点的左子树中的所有数据都必须在该节点之前，并且在该节点右子树中的所有数据之前。也就是说，以下算法将按排序顺序打印元素：

- 1. 打印左子树。
- 2. 打印节点的数据。
- 3. 打印右子树。

让我们用图10中的树来试试。算法告诉我们

- 1. 打印 Juliet 的左子树；也就是 Diana 及其后代。
- 2. 打印 Juliet。
- 3. 打印 Juliet 的右子树；也就是 Tom 及其后代。

如何打印从 Diana 开始的子树呢？

- 1. 打印 Diana 的左子树。没有可打印的内容。
- 2. 打印 Diana。
- 3. 打印 Diana 的右子树，即 Harry。

也就是说，Juliet 的左子树打印为

```
Diana
Harry
```

Juliet 的右子树是从 Tom 开始的子树。它如何打印？同样使用相同的算法：

- 1. 打印 Tom 的左子树，即 Romeo。
- 2. 打印 Tom。
- 3. 打印 Tom 的右子树。没有可打印的内容。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_610_0.png)

因此，Juliet 的右子树打印为

Romeo Tom

现在把所有内容组合起来：左子树、Juliet 和右子树：

Diana Harry Juliet Romeo Tom

树按排序顺序打印出来了。

让我们实现 print 成员函数。你需要一个 `TreeNode` 类的辅助函数 `print_nodes`：

```cpp
void TreeNode::print_nodes() const
{
    if (left != NULL)
    {
        left->print_nodes();
    }
    cout << data << endl;
    if (right != NULL)
    {
        right->print_nodes();
    }
}
```

要打印整棵树，从根节点开始这个递归打印过程，使用 `BinarySearchTree` 类的以下成员函数：

```cpp
void BinarySearchTree::print() const
{
    if (root != NULL)
    {
        root->print_nodes();
    }
}
```

这种访问方案称为 *中序遍历*。还有另外两种遍历方案，称为 *前序遍历* 和 *后序遍历*。

三种遍历方案包括前序遍历、中序遍历和后序遍历。

- 在前序遍历中，
  - 访问根节点。
  - 访问左子树。
  - 访问右子树。

- 在后序遍历中，
  - 访问左子树。
  - 访问右子树。
  - 访问根节点。

这两种遍历不会按排序顺序打印树。然而，它们在二叉树的其他应用中很重要。

树遍历在重要方面与迭代器不同。迭代器允许你一次访问一个节点，并且可以随时停止迭代。而遍历会访问所有元素。

事实证明，实现一个访问二叉树元素的迭代器有点复杂。与列表迭代器一样，树迭代器包含一个指向节点的指针。迭代从没有孩子的最左边元素（称为叶子）开始。然后移动到父节点，再到右孩子，再到下一个未访问的父节点的最左孩子，依此类推，直到到达没有孩子的最右边元素。练习 P14.12 和练习 P14.13 讨论了实现这种树迭代器的两种方法。

# ch14/bintree.cpp

```cpp
#include <iostream>
#include <string>

using namespace std;

class TreeNode
{
public:
    void insert_node(TreeNode* new_node);
    void print_nodes() const;
    bool find(string value) const;
private:
    string data;
    TreeNode* left;
    TreeNode* right;
    friend class BinarySearchTree;
};

class BinarySearchTree
{
public:
    BinarySearchTree();
    void insert(string data);
    void erase(string data);
    int count(string data) const;
    void print() const;
private:
    TreeNode* root;
};
```

