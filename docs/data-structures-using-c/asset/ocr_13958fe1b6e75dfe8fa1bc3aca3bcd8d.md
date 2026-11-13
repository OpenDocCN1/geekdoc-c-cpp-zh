EXAMPLE 7.6 Build a BST from the following set of elements—100, 50, 200, 300, 20, 150, 70, 180, 120, 30—and traverse the tree built in inorder, postorder, and preorder.

Solution The BST is constructed through the following steps:

Step 1: Initially, Root = NULL. Now let us insert 100.

![](bbox=[0.508, 0.243, 0.597, 0.313])

Step 2: Insert 50. As it is less than the root, that is, 100, and its left child is NULL, we insert it as a left child of the root.

![](bbox=[0.508, 0.403, 0.613, 0.483])

Step 3: Insert 200. As it is greater than the root, that is, 100, and its right child is NULL, we insert it as a right child of the root.

![](bbox=[0.476, 0.573, 0.635, 0.653])

Step 4: Insert 300. As it is greater than the root, that is, 100, we move right to 200. It is greater than 200, and its right child is NULL, so we insert it as a right child of 200.

![](bbox=[0.443, 0.763, 0.663, 0.903])