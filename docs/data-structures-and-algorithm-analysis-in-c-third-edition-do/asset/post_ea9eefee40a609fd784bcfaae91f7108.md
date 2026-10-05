
binary search tree of Section 5.4 makes use of this traversal to print all nodes in ascending order of value.

# **Example 5.3** the inorder enumeration for the tree of Figure 5.1 is

A traversal routine is naturally written as a recursive function. Its input parameter is a pointer to a node which we will call root because each node can be viewed as the root of some subtree. The initial call to the traversal function visits root in a pointer to the root of the tree. The traversal function visits root and its children (if any) in the desired order. For example, a preorder traversal specifies that root be visited before its children. This can easily be implemented as follows.

```cpp
template <typename E>
void preorder(BinNode<E> root) {
 if (root == NULL) return; // Empty subtree, do nothing
 visit(root);
 preorder(root->left()); // Perform desired action
preorder(root->right());
}
```

**Function preorder** first checks that the tree is not empty (if it is, the traversal is done and preorder simply returns). Otherwise, preorder makes a call to visit, which processes the root node (i.e., prints or performs whatever computation is required by the application). **Function preorder** is then called recursively on the left subtree, which will visit all nodes in that subtree. Finally, preorder is called on the right subtree, visiting all nodes in the right subtree. Postorder and inorder traversals are similar. They simply change the order in which the node and its children are visited, as appropriate.

An important decision in the implementation of recursive function on trees is to check before to see if the value for root is NULL. If not, it will recursively call itself on the left and right children of root. In other words, preorder makes no attempt to avoid calling on an empty tree. Some programmers use an alternate design in which the left and right pointers of the current node are checked so that the recursive call is only made on non-empty children. Such a design typically looks as follows:

```cpp
template <typename E>
void preorder(BinNode<E>* root) {
 visit(root); // Perform whatever action is desired
 if (root->left() != NULL) preorder2(root->left());
 if (root->right() != NULL) preorder2(root->right());
}
```

At first it might appear that preorder2 is more efficient than preorder, because it makes only half as many recursive calls. (Why?) On the other hand, preorder2 must access the left and right child pointers twice as often. The net result is little or no performance improvement.

In reality, the design of preorder2 is inferior to that of preorder for two reasons. First, while it is not apparent in this simple example, for more complex traversals it can become awkward to place the check for the NULL pointer in the calling code. Even here we had to write two tests for NULL, rather than one needed by preorder. The more important concern with preorder2 is that no recursive calls are made on empty subtrees, it will fail if the initial call passes a NULL pointer. This would occur if the tree is empty. To avoid the bug, preorder2 needs an additional test for a NULL pointer at the beginning (making the subsequent tests redundant after all), or the caller of preorder2 has been obliged to pass in a non-empty tree, which is unreliable design. The net result is that many programmers forget to test for the possibility that the tree is traversed. By using the first design, which explicitly supports processing of empty subtrees, the problem is solved.

Another issue to consider when designing a traversal is how to define the visitor function that is to be executed on every node. One approach is simply to write a new version of the traversal for each visitor function as needed. The disadvantage is that whatever function the traversal must have access to the BinNode class. It is probably better design to permit only the tree class to have access to the BinNode class.

Another approach is for the tree class to supply a generic traversal function which takes the visitor either as a template parameter or as a function parameter. This is known as the signature design pattern. A major constraint on this approach is that the signature for visitor functions is fixed, thus the designer of the generic traversal function must be able to adequately judge what parameters and return type will likely be needed by potential visitor functions.

Handling information flow between parts of a program can be a significant design challenge, especially when dealing with recursive functions as tree traversals. In general, we can run into trouble with passing the correct information needed by the function to do its work, or with returning information to the recursive function's caller. We will see many examples throughout the book that illustrate methods for passing in and out of recursive functions as they traverse a tree structure. Here are a few simple examples.

First we consider the simple case where a computation requires that we communicate information back up the tree to the end user.

## Sec. 5.2 Binary Tree Traversals

![](img/0ae21f56d72533acf0527c86ba21e1e6_177_0.png)

**Figure 5.6** To be a binary search tree, the left child of the node with value 40 must have a value between 20 and 40.

**Example 5.4** We wish to count the number of nodes in a binary tree. The key insight is that the total count for any (non-empty) subtree is one for the root plus the counts for the left and right subtrees. Where do left and right subtree counts come from? Calls to function `count` on the subtrees will compute for this. Thus, we can implement `count` as follows.

```cpp
template <typename E>
int count(BinNode<E>* root) {
    if (root == NULL) return 0;
    return 1 + count(root->left()) + count(root->right());
}
```

Another problem arises when we need to determine if all keys in a binary tree are within a certain range. This is a common requirement for binary search trees. We can implement a check as follows:

```cpp
template <typename Key, typename E>
bool checkBST(BSTNode<Key, E>* root, Key low, Key high) {
    if (root == NULL) return true;
    Key rootkey = root->key();
    if (rootkey < low || rootkey > high)
        return false;
    return checkBST(root->left(), low, rootkey) && checkBST(root->right(), rootkey, high);
}
```
