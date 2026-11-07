are greater than the value in its parent node. Figure 19.19 illustrates a binary search tree with 9 values. Note that the shape of the binary search tree that corresponds to a set of data can vary, depending on the order in which the values are inserted into the tree.

![](bbox=[0.359, 0.196, 0.629, 0.307])

# Implementing the Binary Search Tree Program

The program of Figs. 19.20–19.22 creates a binary search tree and traverses it (i.e., walks through all its nodes) three ways—using recursive inorder, preorder and postorder traversals. We explain these traversal algorithms shortly.

# Testing the Tree Class Template

We begin our discussion with the driver program (Fig. 19.20), then continue with the implementations of classes TreeNode (Fig. 19.21) and Tree (Fig. 19.22). Function main (Fig. 19.20) begins by instantiating integer tree intTree of type Tree< int > (line 10). The program prompts for 10 integers, each of which is entered in the binary tree by calling insertNode (line 19). The program then performs preorder, inorder and postorder traversals (these are explained shortly) of intTree (lines 23, 26 and 29, respectively). The program then instantiates floating-point tree doubleTree of type Tree< double > (line 31). The program prompts for 10 double values, each of which is inserted in the binary tree by calling insertNode (line 41). The program then performs preorder, inorder and postorder traversals of doubleTree (lines 45, 48 and 51, respectively).

```
```cpp
// Fig. 19.20: fig19_20.cpp
// Creating and traversing a binary tree.
#include <iostream>
#include <iomanip>
#include "Tree.h" // Tree class definition
using namespace std;

int main()
{
    Tree< int > intTree; // create Tree of int values

    cout << "Enter 10 integer values:\n";
```
```

Fig. 19.20 | Creating and traversing a binary tree. (Part 1 of 3.)