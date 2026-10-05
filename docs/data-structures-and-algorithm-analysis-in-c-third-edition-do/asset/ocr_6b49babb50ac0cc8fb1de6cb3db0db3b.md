206

Chap. 6 Non-Binary Trees

![](bbox=[0.396, 0.185, 0.603, 0.298])

Figure 6.3 An example of a general tree.

traversal does not have a natural definition for the general tree, because there is no particular number of children for an internal node. An arbitrary definition — such as visit the leftmost subtree of inorder, then the root, then visit the remaining subtrees in inorder. However, inorder traversals are generally not useful with general trees.

Example 6.1 A preorder traversal of the tree in Figure 6.3 visits the nodes in order RACDEBF.

A posteriori traversal of this tree visits the nodes in CDEAFBR.

To perform a preorder traversal, it is necessary to visit each of the children for a given node (say R) from left to right. This is accomplished by starting at R's leftmost child (call it T). From T, we can move to T's right sibling, and then to that node's right sibling, and so on.

Using the logic of Figure 6.2, here is a C++ implementation to print the nodes of a general tree in preorder. The for loop at the end, processes the list of children by visiting the leftmost child, repeatedly moving to the next child until calling next NULL

```
// Print using a preorder traversal
void print(GTNode<E>* root) {
  if (root->isLeaf()) cout << "Leaf:";
  else cout << "Internal:";
  cout << root->value() << "\n";
  // Now process the children of "root"
  for (GTNode<E>* temp = root->leftmostChild();
       temp != NULL; temp = temp->rightSibling())
    printleft(temp);
  }
}
```