

## 16.2.2 平衡树

在平衡树中，从根到叶子的所有路径长度大致相同。

当我们使用二叉树存储数据时（第 16.3 节将这样使用），我们希望树是平衡的。在平衡树中，从根到任一叶节点的所有路径长度大致相同。图 7 展示了平衡树和非平衡树的示例。

回顾一下，树的高度是指从根到叶的最长路径上的节点数。图 7 中的树高度为 5。正如你所见，对于给定的高度，平衡树能容纳比非平衡树更多的节点。

我们关心树的高度，是因为许多树操作沿着从根到叶的路径进行，其效率用树的高度来表示比用树中元素个数来表示更合适。

高度为 h 的二叉树最多可以有 n = 2^h − 1 个节点。例如，一棵完全填满的高度为 4 的二叉树有 1 + 2 + 4 + 8 = 15 = 2^4 − 1 个节点（见图 8）。

换言之，对于完全填满的二叉树，h = log₂(n + 1)。对于平衡树，我们仍然有 h ≈ log₂ n。例如，包含 1,000 个节点的平衡二叉树的高度约为 10（因为 1,000 ≈ 1024 = 2¹⁰）。包含 1,000,000 个节点的平衡二叉树的高度约为 20（因为 10⁶ ≈ 2²⁰）。正如你将在第 16.3 节中看到的，在这样的树中查找任何元素大约需要 20 步。这比遍历包含 1,000,000 个元素的链表要快得多。

![](img/d61019b035dd82beb581604273c0ee6b_823_0.png)

© Emrah Turudu/iStockphoto.

在平衡二叉树中，每个子树都有大致相同数量的节点。

![](img/d61019b035dd82beb581604273c0ee6b_823_1.png)

图 7 平衡树与非平衡树

让我们跟踪在图 11 的树中插入 Romeo 时对 add_node 的调用。第一次调用 add_node 为

```
add_node(root, new_node)
```

由于 root 指向 Juliet，你将 Juliet 与 Romeo 比较，发现必须调用

```
add_node(parent->right, new_node)
```

节点 parent->right 是 Tom。再次比较数据值（Tom 与 Romeo），发现现在必须向左移动。由于 parent->right->left 为 nullptr，将 parent->right->left 设为 new_node，插入完成（见图 12）。

与链表或数组不同，和哈希表一样，二叉搜索树没有插入位置。你不能选择将元素插入二叉搜索树的哪个位置。这种数据结构是自组织的；也就是说，每个元素都会找到自己的位置。

## 16.3.3 删除

现在讨论删除算法。我们的任务是从树中移除一个节点。当然，我们必须首先找到要删除的节点。由于二叉搜索树的特性，这是一件简单的事情。将要删除的数据值与存储在根节点中的数据值进行比较。如果更小，继续在左子树中查找。否则，继续在右子树中查找。

现在假设我们已经找到了需要删除的节点。首先考虑最简单的情况。如果要删除的节点根本没有子节点，那么直接将父链接设置为 nullptr（图 13）。

当要删除的节点只有一个子节点时，情况仍然很简单（见图 14）。

要删除该节点，只需修改指向该节点的父链接，使其转而指向子节点。

要删除的节点有两个子节点的情况更具挑战性。与其移除该节点，不如用树中下一个更大的值替换其数据值。这种替换保持了二叉搜索树的特性。（或者，你也可以使用左子树中的最大元素——参见练习 P16.4）。

> 从二叉搜索树中删除只有一个子节点的节点时，该子节点会替换被删除的节点。

![](img/d61019b035dd82beb581604273c0ee6b_829_0.png)

图 13 删除没有子节点的节点

![](img/d61019b035dd82beb581604273c0ee6b_829_1.png)

图 14 删除只有一个子节点的节点

从二叉搜索树中删除有两个子节点的节点时，用右子树中最小的节点替换它。

为了找到下一个更大的值，进入右子树并找到其中最小的数据值。持续沿着左子节点链接向下查找。一旦到达没有左子节点的节点，就找到了包含该子树最小数据值的节点。现在删除该节点——它很容易删除，因为它至多有一个右子节点。然后将其数据值存储到原本计划删除的节点中。图 15 展示了细节。

![](img/d61019b035dd82beb581604273c0ee6b_830_0.png)

图 15 删除有两个子节点的节点

在本节末尾，你将看到 BinarySearchTree 类的源代码。它包含我们刚才描述的 insert 和 erase 函数、一个测试值是否存在于二叉搜索树中的 count 函数，以及一个我们将在第 16.4 节分析的 print 函数。

## 16.3.4 操作的效率

在平衡树中，从根到叶的所有路径长度大致相同。

既然你已经了解了这种数据结构的实现，那么很可能会想知道它到底好不好。与链表中的节点一样，这里的节点也是逐个分配的。插入或删除新元素时，不需要移动已有元素；这是一个优点。然而，插入和删除的速度取决于树的形状。如果树是平衡的，这些操作就很快。由于查找、添加和删除元素的操作会处理从根到叶的路径上的节点，其执行时间与树的高度成正比，而不是与树中的节点总数成正比。对于平衡树，我们有 h ≈ O(log(n))。因此，插入、查找或删除一个元素是 O(log(n)) 操作。另一方面，如果树恰好不平衡，那么二叉树操作可能会很慢——在最坏的情况下，与链表插入一样慢。表 2 总结了这些观察。

```cpp
/*
void insert(string element);

/**
 * Tries to find an element in the tree.
 * @param element the element to find
 * @return 1 if the element is contained in the tree
 */
int count(string element) const;

/**
 * Tries to remove an element from the tree. Does nothing
 * if the element is not contained in the tree.
 * @param element the element to remove
 */
void erase(string element);

/**
 * Prints the contents of the tree in sorted order.
 */
void print() const;

private:
/**
 * Prints a node and all of its descendants in sorted order.
 * @param parent the root of the subtree to print
 */
void print(Node* parent) const;

/**
 * Inserts a new node as a descendant of a given node.
 * @param parent the root node
 * @param new_node the node to insert
 */
void add_node(Node* parent, Node* new_node) const;

Node* root;
};

#endif
```

# sec03/binary_search_tree.cpp

```cpp
#include <iostream>
#include "binary_search_tree.h"

using namespace std;

BinarySearchTree::BinarySearchTree()
{
    root = nullptr;
}

void BinarySearchTree::insert(string element)
{
    Node* new_node = new Node;
    new_node->data = element;
    new_node->left = nullptr;
    new_node->right = nullptr;
    if (root == nullptr) { root = new_node; }
```

```cpp
}
else
{
    new_child = to_be_removed->left;
}
if (parent == nullptr) // Found in root
{
    root = new_child;
}
else if (parent->left == to_be_removed)
{
    parent->left = new_child;
}
else
{
    parent->right = new_child;
}
return;
}
// Neither subtree is empty
// Find smallest element of the right subtree
Node* smallest_parent = to_be_removed;
Node* smallest = to_be_removed->right;
while (smallest->left != nullptr)
{
    smallest_parent = smallest;
    smallest = smallest->left;
}
// smallest contains smallest child in right subtree
// Move contents, unlink child
to_be_removed->data = smallest->data;
if (smallest_parent == to_be_removed)
{
    smallest_parent->right = smallest->right;
}
else
{
    smallest_parent->left = smallest->right;
}
void BinarySearchTree::print() const
{
    print(root);
    cout << endl;
}
void BinarySearchTree::print(Node* parent) const
{
    if (parent == nullptr) { return; }
    print(parent->left);
    cout << parent->data << " ";
    print(parent->right);
```

