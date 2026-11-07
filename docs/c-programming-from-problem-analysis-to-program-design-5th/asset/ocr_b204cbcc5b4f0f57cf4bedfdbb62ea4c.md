![](bbox=[0.182, 0.107, 0.912, 0.236])

**FIGURE 18-42**  Doubly linked list before deleting 17

Suppose that the item to be deleted is 17. First, we search the list with two pointers and find the node with info 17 and then adjust the link field of the affected nodes (see Figure 18-43).

![](bbox=[0.182, 0.377, 0.912, 0.579])

**FIGURE 18-43**  List after adjusting the links of the nodes before and after the node with info 17

Next, we delete the node pointed to by current (see Figure 18-44).

![](bbox=[0.182, 0.673, 0.912, 0.803])

**FIGURE 18-44**  List after deleting the node with info 17