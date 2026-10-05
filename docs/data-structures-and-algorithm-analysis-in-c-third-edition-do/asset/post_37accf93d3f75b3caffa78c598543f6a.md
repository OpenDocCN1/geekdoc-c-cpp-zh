
for the BST containing n nodes to be a chain of nodes with height n. This would happen if, for example, all elements were inserted in sorted order. In general, it is preferable for a BST to be as shallow as possible. This keeps the average cost of a BST operation low.

Removing a node from a BST is a bit trickier than inserting a node, but it is not complicated if all of the possible cases are considered individually. Before tackling the general remove process, let us first describe how to remove from a given subtree with the smallest key value. This routine will be used later by the general remove process. To remove the node with the minimum key value from a subtree, find that by continuously moving down the left link until there is no further left to follow. Call this node S. To remove S, simply have the parent of S change its pointer to point to the right of S. We know that S has no left child (if S did have a left child, S would not be the node with minimum key value). Thus, changing the pointer for this method, named deletemin, is as follows:

```cpp
template <typename Key, typename E>
BSTNode<Key, E>* BST<Key, E>::
deletermin(BSTNode<Key, E>* rt) {
    if (rt->left() == NULL) // Found min
        return rt->right();
    else {
        // Continue left
        rt->setLeft(deletermin(rt->left()));
        return rt;
    }
}
```

**Example 5.6** 5.16 illustrates the deletemin process. Beginning at the root node with value 10, deletemin follows the left link until there is no further left link, in this case reaching the node with value 5. The node with value 10 is changed to point to the right child of the node containing the minimum value. This is indicated in Figure 5.16 by a dashed line.

A pointer to the node containing the minimum-valued element is stored in parameter S. The return value of the deletemin method is the subtree of the current node with the minimum-valued node in the removed subtree. As with inserthelp, each node on the path to the root has its left child pointer reassigned to the subtree resulting from its call to the deletemin method.

A useful companion method is getmin returns a pointer to the node containing the minimum value in the subtree.

## Sec 5.4 Binary Search Trees

![](img/0ae21f56d72533acf0527c86ba21e1e6_193_0.png)

**Figure 5.16** An example of deleting the node with minimum value. In this tree, the node with minimum value, 5, is the left child of the root. Thus, the root's left pointer is changed to point to 5's right child.

```cpp
template <typename Key, typename E>
BSTNode<Key, E>* BST<Key, E>::
getmin(BSTNode<Key, E>* rt) {
    if (rt->left() == NULL)
        return rt;
    else return getmin(rt->left());
}
```

Removing a node with given key value R from the BST requires we first find R and then remove it from the tree. The first part of the remove operation is a search to find R. Once R is found, there are several possibilities. If R has no children, then R's parent has its pointer set to NULL. If R has one child, then R's parent has its pointer set to R's child (similar to deletemin). The problem comes if R has two children. One simple approach, though expensive, is to set R's parent to one of R's subtrees, then remove the remaining subtree's nodes one at a time. A better alternative is to find a value in one of the subtrees that replace the value in R.

Thus, the question becomes: Which value can substitute for the one being removed? It cannot be any arbitrary value, because we must preserve the BST property while making changes to the structure of the tree. Which value is most like the one being removed? The answer is the least key value greater than (or equal to) the one being removed, or the greatest key value less than the one removed. If either of these values replaces the one being removed, then the BST property is maintained.

**Example 5.7** Assume that we wish to remove the value 37 from the BST of Figure 5.13(a). Instead of removing the root node, we remove the node with the least value in the right subtree (using the deletemin operation). This value can then replace the value in the root. In this example we remove the node with value 40, because it is the least value in the right subtree.

![](img/0ae21f56d72533acf0527c86ba21e1e6_194_0.png)

**Figure 5.17** An example of removing the value 37 from the BST. The node containing this value has two children. We replace value 37 with the least value from the node's right subtree, in this case 40.

We then substitute 40 as the new value for the root node. Figure 5.17 illustrates this process.

When duplicate node values do not appear in the tree, it makes no difference whether the replacement is the greatest value from the left subtree or the least value from the right subtree. If duplicates are stored, then we must select the replacement from the right subtree. To see why, the greatest value in the left subtree $G$. If multiple nodes in the left subtree have value $G$, selecting $G$ as the replacement for the root of the right subtree will result in a tree with equal values to the left of the node now containing $G$. Precisely this situation occurs if we replace value 120 with the greatest value in the left subtree of Figure 5.13(b). Selecting the value from the right subtree does not have a similar problem, because it does not violate the Binary Search Tree Property if equal values appear in the tree.

From the above, we see that if we want to remove the record stored in a node with two children, then we simply call `delete` on the node's right subtree and substitute the record for the record being removed. Figure 5.18 shows an implementation for `removehelp`.

The cost for **find** and **insert** is the depth of the node found or inserted. The cost for **removehelp** is the depth of the node being removed, or in the case when the node has two children, the depth of the node with smallest value in its right subtree. Thus, in the case, the cost for any one of these operations is the depth of the node. This is why it is desirable to keep BSTs **balanced**, that is, with least possible height. If a binary tree is completely unbalanced, for example in the shape of a linked list, then the height for a tree with $n$ nodes can be as great as $n$. Thus, a balanced BST in the average case have operations costing $\Theta(\log n)$, while a wildly unbalanced BST can have operations in the worst case $\Theta(n)$. Consider the situation where we construct a BST of $n$ nodes by inserting records one at a time. If we are fortunate to have them arrive in an order that results in a balanced tree (a “random” order is likely to be good enough for purpose,

```cpp
// Remove a node with key value k
// Return: The tree with the node removed
template <typename Key, typename E>
BSTNode<Key, E>* ::
removehelp(BSTNode<Key, E>* rt, const Key& k) {
    if (rt == NULL) return NULL;      // k is not in
    else if (k < rt->key())
        rt->setLeft(removehelp(rt->left(), k));
    else if (k > rt->key())
        rt->setRight(removehelp(rt->right(), k));
    else {
        BSTNode<Key, E>* temp = rt;    // remove it
        if (rt->right() == NULL) {
            rt = rt->left();              // point to right
            delete temp;
        }
        else if (rt->left() == NULL) { // Only a left
            rt = rt->right();             // point to left
            delete temp;
        }
        else {
            BSTNode<Key, E>* temp = getmin(rt->right()); // Both children are non-empty
            rt->setElement(temp->element);
            rt->setKey(temp->key());
            rt->setRight(deletermin(rt->right()));
            delete temp;
        }
    }
    return rt;
}
```

Figure 5.18 Implementation for the BST removehelp method.

If the records are inserted in order of increasing value, the resulting tree will be a chain of height $n$. The cost of insertion in this case is $\sum_{i=1}^n i = \Theta(n^2)$.

Traversing a BST costs $\Theta(n)$ regardless of the shape of the tree. Each node is visited exactly once, and each child pointer is followed exactly once.

Below are two traversals. The first is member clearhelp, which returns the nodes of the BST to the freelist. Because the children of a node must be freed before the node itself, this is a postorder traversal.

```cpp
template <typename Key, typename E>
void clearhelp(BSTNode<Key, E>* root) {
    if (root == NULL) return;
    clearhelp(root->left());
    clearhelp(root->right());
    delete root;
}
```
