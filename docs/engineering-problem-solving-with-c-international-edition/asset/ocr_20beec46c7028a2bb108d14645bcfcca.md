To delete a value from a linked list, we need to find the node to be deleted. We again use the pointer to the head of the list to access the first data value in the list. We then move from one node to another using the pointer in the current node. If we reach a data value greater than the one to be deleted, we print a message that the value to be deleted is not in the list. The node to be deleted can be the first node, a node between two other nodes, or the last node. We must handle each of these cases carefully, so we can make sure that the pointers are updated properly. Figures 7.6 through 7.8 outline each of these three cases. For each case, we start with the linked list given in Figure 7.2. Note that there are nodes (and data values) that cannot be accessed after these deletions. For example, in Figure 7.6, we can no longer access the value 10; in Figure 7.7, we can no longer access the value 21; and in Figure 7.8, we can no longer access the value 35. Also, note that deleting the first node may result in an empty list if the list only contains one node.

Empty list

We will now develop a set of four functions to create and maintain a linked list. The first function determines if a linked list is an empty list, the second function prints the contents of a linked list, the third function inserts a node in its correct ordered position, and the fourth function deletes a node. Each node in the linked list will be represented by the following structure:

```
struct node
{
 int data;
 struct node *link;
 };
```

![](bbox=[0.3, 0.5, 0.8, 0.62])

![](bbox=[0.3, 0.65, 0.8, 0.78])

![](bbox=[0.3, 0.8, 0.8, 0.92])