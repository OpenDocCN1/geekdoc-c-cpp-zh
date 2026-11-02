
## 16.2.2 Balanced Trees

In a balanced tree, all paths from the root to the leaves have approximately the same length.

When we use binary trees to store data, as we will in Section 16.3, we would like to have trees that are balanced. In a balanced tree, all paths from the root to one of the leaf nodes have approximately the same length. Figure 7 shows examples of a balanced and an unbalanced tree.

Recall that the height of a tree is the number of nodes in the longest path from the root to a leaf. The trees in Figure 7 have height 5. As you can see, for a given height, a balanced tree can hold more nodes than an unbalanced tree.

We care about the height of a tree because many tree operations proceed along a path from the root to a leaf, and their efficiency is better expressed by the height of the tree than the number of elements in the tree.

A binary tree of height h can have up to n = 2^h − 1 nodes. For example, a completely filled binary tree of height 4 has 1 + 2 + 4 + 8 = 15 = 2^4 − 1 nodes (see Figure 8).

In other words, h = log₂(n + 1) for a completely filled binary tree. For a balanced tree, we still have h ≈ log₂ n. For example, the height of a balanced binary tree with 1,000 nodes is approximately 10 (because 1,000 ≈ 1024 = 2¹⁰). A balanced binary tree with 1,000,000 nodes has a height of approximately 20 (because 10⁶ ≈ 2²⁰). As you will see in Section 16.3, you can find any element in such a tree in about 20 steps. That is a lot faster than traversing the 1,000,000 elements of a linked list.

![](img/d61019b035dd82beb581604273c0ee6b_823_0.png)

© Emrah Turudu/iStockphoto.

In a balanced binary tree, each subtree has approximately the same number of nodes.

![](img/d61019b035dd82beb581604273c0ee6b_823_1.png)

Figure 7 Balanced and Unbalanced Trees

Let's trace the calls to add_node when inserting Romeo into the tree in Figure 11. The first call to add_node is

```
add_node(root, new_node)
```

Because root points to Juliet, you compare Juliet with Romeo and find that you must call

```
add_node(parent->right, new_node)
```

The node parent->right is Tom. Compare the data values again (Tom vs. Romeo) and find that you must now move to the left. Because parent->right->left is nullptr, set parent->right->left = new_node, and the insertion is complete (see Figure 12).

Unlike a linked list or an array, and like a hash table, a binary search tree has no insert positions. You cannot select the position where you would like to insert an element into a binary search tree. The data structure is self-organizing; that is, each element finds its own place.

## 16.3.3 Removal

We will now discuss the removal algorithm. Our task is to remove a node from the tree. Of course, we must first find the node to be removed. That is a simple matter, due to the characteristic property of a binary search tree. Compare the data value to be removed with the data value that is stored in the root node. If it is smaller, keep looking in the left subtree. Otherwise, keep looking in the right subtree.

Let us now assume that we have located the node that needs to be removed. First, let us consider the easiest case. If the node to be removed has no children at all, then the parent link is simply set to nullptr (Figure 13).

When the node to be removed has only one child, the situation is still simple (see Figure 14).

To remove the node, simply modify the parent link that points to the node so that it points to the child instead.

The case in which the node to be removed has two children is more challenging. Rather than removing the node, it is easier to replace its data value with the next larger value in the tree. That replacement preserves the binary search tree property. (Alternatively, you could use the largest element of the left subtree—see Exercise P16.4).

> When removing a node with only one child from a binary search tree, the child replaces the node to be removed.

![](img/d61019b035dd82beb581604273c0ee6b_829_0.png)

Figure 13 Removing a Node with No Children

![](img/d61019b035dd82beb581604273c0ee6b_829_1.png)

Figure 14 Removing a Node with One Child

When removing a node with two children from a binary search tree, replace it with the smallest node of the right subtree.

To locate the next larger value, go to the right subtree and find its smallest data value. Keep following the left child links. Once you reach a node that has no left child, you have found the node containing the smallest data value of the subtree. Now remove that node—it is easily removed because it has at most one child to the right. Then store its data value in the original node that was slated for removal. Figure 15 shows the details.

![](img/d61019b035dd82beb581604273c0ee6b_830_0.png)

Figure 15 Removing a Node with Two Children

At the end of this section, you will find the source code for the BinarySearchTree class. It contains the insert and erase functions that we just described, a count function that tests whether a value is present in a binary search tree, and a print function that we will analyze in Section 16.4.

## 16.3.4 Efficiency of the Operations

In a balanced tree, all paths from the root to the leaves have about the same length.

Now that you have seen the implementation of this data structure, you may well wonder whether it is any good. Like nodes in a linked list, the nodes are allocated one at a time. No existing elements need to be moved when a new element is inserted or removed; that is an advantage. How fast insertion and removal are, however, depends on the shape of the tree. These operations are fast if the tree is balanced. Because the operations of finding, adding, and removing an element process the nodes along a path from the root to a leaf, their execution time is proportional to the height of the tree, and not to the total number of nodes in the tree. For a balanced tree, we have h ≈ O(log(n)). Therefore, inserting, finding, or removing an element is an O(log(n)) operation. On the other hand, if the tree happens to be unbalanced, then binary tree operations can be slow—in the worst case, as slow as insertion into a linked list. Table 2 summarizes these observations.

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
