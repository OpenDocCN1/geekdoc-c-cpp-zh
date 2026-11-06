![](bbox=[0.214, 0.124, 0.704, 0.347])

**Fig. 20.18** | A graphical representation of a binary tree.

# *Binary Search Trees*

A binary search tree (with no duplicate node values) has the characteristic that the values in any left subtree are less than the value in its parent node, and the values in any right subtree are greater than the value in its parent node. Figure 20.19 illustrates a binary search tree with 9 values. Note that the shape of the binary search tree that corresponds to a set of data can vary, depending on the order in which the values are inserted into the tree.

![](bbox=[0.371, 0.549, 0.6, 0.652])

**Fig. 20.19** | A binary search tree.

# *Implementing the Binary Search Tree Program*

The program of Figs. 20.20–20.22 creates a binary search tree and traverses it (i.e., walks through all its nodes) three ways—using recursive inorder, preorder and postorder traversals. We explain these traversal algorithms shortly.

We begin our discussion with the driver program (Fig. 20.22), then continue with the implementations of classes Node (Fig. 20.20) and Tree (Fig. 20.21). Function main (Fig. 20.22) begins by instantiating integer tree intTree of type Tree<int> (line 10). The program prompts for 10 integers, each of which is inserted in the binary search tree by calling insertNode (line 19). The program then performs preorder, inorder and postorder traversals (these are explained shortly) of intTree (lines 23, 26 and 29, respectively). The program then instantiates floating-point tree doubleTree of type Tree<double> (line 31). The program prompts for 10 double values, each of which is inserted in the binary