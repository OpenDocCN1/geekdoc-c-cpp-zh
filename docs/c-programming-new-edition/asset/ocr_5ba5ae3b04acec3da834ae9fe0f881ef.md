![](bbox=[0.27, 0.09, 0.68, 0.27])

Obviously the latter option is advisable because if you have a large list and you use the former method you will end up forfeiting a lot of time and resources. A heap is a tree most often referred as a binary tree. The difference between the heap and any other tree in a heap every child node has a value which is less than its parent value. Thus, the root node is the node with the largest value.

The above approach is called top-heavy where although the nodes along every branch has a particular order the nodes at a level are not necessarily ordered. If the above approach is not particularly appealing then the heaps offer another method called bottom-heavy in which the root node is the smallest in the list and the parent node is essentially less than the child nodes. As the nodes are added they grow from left to right.

The most approved method is to store nodes successively in an array in the pattern one would encounter them in a level traversal. Consider a zero-indexed array, that is the parent of each node at a position I in the array is located at position(I-1)/2. The left and right children of a node are situated at the positions 2I+1 and 2I+2. Using this kind of arrangement it is easy to locate a heap’s last node because the right most node at the deepest level is the last node.

24 21 19 11 10 18 16 17 8 6 14 0 1 2 3 4 5 6 7 8 9 1 0 24 19 8 6 14 11 9 18 16 21

Quick sort – the quick sort mechanism can also be termed as partition exchange sort.

The main reason behind giving it the name partition exchange sort lies in the very essence that this program is based on placing a specific element at the right position in each partition. The flow of the process begins by taking a pivot element.

A pivot element is always the first element of the list. Now, the pivot element must be placed at one of the positions in the list in such a manner that all the elements towards the left of pivot element are less than it and all the elements towards the right are greater than it.