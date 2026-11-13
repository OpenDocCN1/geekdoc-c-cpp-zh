![](bbox=[0.14, 0.09, 0.51, 0.25])

![](bbox=[0.66, 0.09, 0.86, 0.25])

# Figure 9.6 Continued

A binary tree that has only left or right children is known as a skewed binary tree in general and specifically left-skewed binary tree or right-skewed binary tree, respectively. Figure 9.7 illustrates the skewed binary trees.

![](bbox=[0.16, 0.38, 0.48, 0.55])

![](bbox=[0.52, 0.38, 0.84, 0.55])

# Figure 9.7 Skewed binary tree

# 9.5 REPRESENTATION OF BINARY TREES

Binary trees can be represented using both sequential (arrays) and linked data structure.

# 9.5.1 ARRAY REPRESENTATION OF A BINARY TREE

Numbering of nodes and the properties that are discussed in the earlier section are used in representing the binary trees as arrays. The elements in the nodes that are numbered are placed into the corresponding positions of the array. The array positions of missing nodes in the binary tree are left empty in the array. Hence, it leads to wastage of a space. Figure 9.8 illustrates the array representation of a binary tree.

For any element in array position i, the left child will be in position 2i, the right child will be in position (2i+1), and the parent is in position ⌊i/2⌋. The array representation of a binary tree depicted in Figure 9.8(a) is shown in Figure 9.8(b). Here, the root element P is placed in the first position of the array, i.e. i=1 position. Its left child Q is placed in 2i=2*1=2nd position of the array. Its right child R is placed in 2i+1=2*1+1=3rd position of the array. Now consider the element Q, as it is in the 2nd position of array, i=2, since it does not have a left child, the 4th position of the array is left empty. Its right child S is placed in 2i+1=2*2+1=5th position