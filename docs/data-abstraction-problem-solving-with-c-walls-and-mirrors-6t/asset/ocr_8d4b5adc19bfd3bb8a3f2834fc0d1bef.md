# FIGURE 16-9 (a) N with only a left child—N can be either the left child or right child of P; (b) after removing node N

![](bbox=[0.1, 0.145, 0.75, 0.49])

What kind of node M is easier to remove than the node N? Because you know how to delete a node that has either no children or one child, M could be such a node. You have to be careful, though. Can you choose any node and copy its data into N? No, because you must preserve the tree's status as a binary search tree. For example, if in the tree of Figure 16-11a, you copied the data from M to N, the result in Figure 16-11b would no longer be a binary search tree. What data item, when copied into the node N, will preserve the tree's status as a binary search tree? All of the entries in the left subtree of N are less than the entry in N, and all of the entries in the right subtree of N are greater than the entry in N. You must retain this property when you replace the

# FIGURE 16-10 N with two children

![](bbox=[0.3, 0.73, 0.5, 0.9])