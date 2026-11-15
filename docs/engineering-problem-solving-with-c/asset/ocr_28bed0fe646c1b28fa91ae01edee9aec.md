right child of this node. The condition root == null is the terminating condition, and each recursive call reduces the problem to the traversal of a smaller subtree. Applying an in order traversal of the tree in Figure 10.10, and picking each nodes as it was visited would result in the following output: 8 10 14 19 22 27.

The algorithm for inserting a new node in the correct position to maintain the ordering of a binary search tree begins at the root of the tree. If the tree is empty, the new node is inserted as the first node in the tree. If the root is not empty, the value of the new node is compared to the value of the first node. If the value of the new node is less than the root node, the algorithm calls itself on the left child, else the algorithm calls itself on the right child. The recursive algorithm is described below:

```
insert(Node* root, int value):
if(root == null)
root = new Node(value)
return
else
if(value < root->value)
insert(root->left child,value)
else
insert(root->right child,value)
```

If the value 17 was inserted into the binary search tree in Figure 10.10, the resulting tree would look like the tree in Figure 10.11.

![](bbox=[0.196, 0.623, 0.506, 0.908])

Figure 10.11 Binary search tree after insertion of a new node.