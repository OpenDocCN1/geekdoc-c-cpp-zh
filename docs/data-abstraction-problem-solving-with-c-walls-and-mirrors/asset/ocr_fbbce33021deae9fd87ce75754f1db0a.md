# A Link-Based Implementation of the ADT Binary Search Tree 475

FIGURE 16-9 (a) N with only a left child—N can be either the left child or right child of P; (b) after removing node N

![](bbox=[0.068, 0.153, 0.737, 0.503])

What kind of node M is easier to remove than the node N? Because you know how to delete a node that has either no children or one child, M could be such a node. You have to be careful, though. Can you choose any node and copy its data into node N? No, because you must preserve the tree's status as a binary search tree. For example, if in the tree of Figure 16-11a, you copied the data from M to N, the result in Figure 16-lb would no longer be a binary search tree.

What data item, when copied into the node N will preserve the tree's status as a binary search tree? All of the entries in the left subtree of N are less than the entry in N, and all of the entries in the right subtree of N are greater than the entry in N. You must retain this property when you replace the

FIGURE 16-10 N with two children

![](bbox=[0.068, 0.743, 0.753, 0.893])