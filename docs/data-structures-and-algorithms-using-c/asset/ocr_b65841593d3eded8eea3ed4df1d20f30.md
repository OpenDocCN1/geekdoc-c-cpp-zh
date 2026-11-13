# AVL Rotations

To balance itself, an AVL tree may perform the following four kinds of rotations –

+   - Left rotation
+   - Right rotation
+   - Left-Right rotation
+   - Right-Left rotation

The first two rotations are single rotations and the next two rotations are double rotations. To have an unbalanced tree, we at least need a tree of height 2. With this simple tree, let's understand them one by one.

# Left Rotation

If a tree becomes unbalanced, when a node is inserted into the right subtree of the right subtree, then we perform a single left rotation –

![](bbox=[0.05, 0.37, 0.95, 0.5])

In our example, node A has become unbalanced as a node is inserted in the right subtree of A's right subtree. We perform the left rotation by making A the left-subtree of B.

# Right Rotation

AVL tree may become unbalanced, if a node is inserted in the left subtree of the left subtree. The tree then needs a right rotation.

![](bbox=[0.05, 0.67, 0.95, 0.8])

As depicted, the unbalanced node becomes the right child of its left child by performing a right rotation.

# Left-Right Rotation

Double rotations are slightly complex version of already explained versions of rotations. To understand them better, we should take note of each action performed while rotation.