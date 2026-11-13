you move to the right child. Eventually, you will reach a leaf, and the name at the leaf tells you which animal you have been examining—or at least it does if the animal is one of the animals that the tree knows about.

# General Trees

Each node in a binary tree has at most two children. In fact, that's why the word "binary" is used. But in general, a node in a tree may have any number of children. Figure 10.4 shows an example where some nodes have one child, some have two, and some have three. A node in a general tree might even have more than three children (although three is the most in Figure 10.4). In Figure 10.4 we have not written any data at the nodes—but we could have written integers or strings or whatever data type we were interested in storing.

# Trees

A tree is a finite set of nodes. The set might be empty (no nodes, which is called the empty tree). But if the set is not empty, then it must follow these rules:

+   1. There is one special node, called the root.
+   2. Each node may be associated with one or more different nodes, called its children. If a node c is the child of another node p, then we say that p is c's parent.
+   3. Each node except the root has exactly one parent; the root has no parent.
+   4. If you start at any node and move to the node's parent (provided there is one), then move again to that node's parent (provided there is one), and keep moving upward to each node's parent, you will eventually reach the root.

FIGURE 10.4 A General Tree

![](bbox=[0.37, 0.7, 0.62, 0.85])