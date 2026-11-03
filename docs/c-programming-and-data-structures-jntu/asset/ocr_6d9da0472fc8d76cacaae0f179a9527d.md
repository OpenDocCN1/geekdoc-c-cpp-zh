Case c: Since the node to be deleted has one child, the solution is again rather simple. We have to adjust the pointer of the parent of the node to be deleted, such that after deletion it points to child node being deleted.

![](bbox=[0.05, 0.25, 0.45, 0.52])

![](bbox=[0.55, 0.25, 0.95, 0.52])

Case d: Since the node to be deleted has two children, the solution is more complex. The whole logic of deleting a node with two children is to locate the in-order successor, copy its data and reduce the problem to a simple deletion of a node with one or zero child.

![](bbox=[0.05, 0.75, 0.45, 0.92])

![](bbox=[0.55, 0.75, 0.95, 0.92])

Algorithm to perform deletion operation in a binary search tree.

+   Step 1: Start
+   Step 2: Define a structure btree
+   Step 3: Type define struct btree as node
+   Step 4: While(tree), begin
+   Step 5: Print MENU
+   Step 6: Write your choice