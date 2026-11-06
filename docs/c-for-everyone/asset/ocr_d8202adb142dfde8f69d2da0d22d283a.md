Three traversal schemes include preorder traversal, inorder traversal, and postorder traversal.

+   In preorder traversal,
+   - Visit the root.
+   - Visit the left subtree.
+   - Visit the right subtree.

+   In postorder traversal,
+   - Visit the left subtree.
+   - Visit the right subtree.
+   - Visit the root.

These two traversals will not print the tree in sorted order. However, they are important in other applications of binary trees.

Tree traversals differ from an iterator in an important way. An iterator lets you visit a node at a time, and you can stop the iteration whenever you like. The traversals, on the other hand, visit all elements.

It turns out to be a bit complex to implement an iterator that visits the elements of a binary tree. Like a list iterator, a tree iterator contains a pointer to a node. The iteration starts at the leftmost element with no children (called a leaf). It then moves to the parent node, then to the right child, then to the next unvisited parent's leftmost child, and so on, until it reaches the rightmost element with no children. Exercise P14.12 and Exercise P14.13 discuss two methods for implementing such a tree iterator.

# ch14/bintree.cpp

```
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
```