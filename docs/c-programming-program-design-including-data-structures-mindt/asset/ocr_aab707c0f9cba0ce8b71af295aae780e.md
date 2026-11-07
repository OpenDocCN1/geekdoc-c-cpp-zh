![](bbox=[0.183, 0.076, 0.909, 0.201])

FIGURE 16-23  List with more than one node

Suppose that the node to be deleted is 28. After deleting this node, the second node becomes the first node. Therefore, after deleting this node, the value of the pointer `first` changes; that is, after deletion, `first` contains the address of the node with info 17, and `count` is decremented by 1. Figure 16-24 shows the list after deleting 28.

![](bbox=[0.183, 0.377, 0.909, 0.502])

FIGURE 16-24  List after deleting node with info 28

# Case 3: The node to be deleted is not the first node but is somewhere in the list.

This case has two subcases: (a) the node to be deleted is not the last node, and (b) the node to be deleted is the last node. Let us illustrate both cases.

# Case 3a: The node to be deleted is not the last node. Consider the list shown in Figure 16-25.

![](bbox=[0.183, 0.716, 0.909, 0.846])

FIGURE 16-25  List before deleting 37

Suppose that the node to be deleted is 37. After deleting this node, the resulting list is shown in Figure 16-26. (Notice that the deleting of 37 does not require us to