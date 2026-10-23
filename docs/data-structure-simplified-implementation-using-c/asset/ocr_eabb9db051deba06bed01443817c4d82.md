During the creation of a doubly link list, we create it by creating one node at a time. Upon defining the node structure, needed space will be allocated from the memory. Allocation of memory to a newnode, connecting the previous and next pointer along with the node data has been depicted as follows:

```
dnode *newnode;
newnode=new dnode;
newnode->prev=NULL;
newnode->next=NULL;
newnode->data=5;
```

Complete operation for creating a node of a doubly link list, its data and allocation assignment has been illustrated in figure 4.2.

![](bbox=[0.19, 0.34, 0.88, 0.54])

# 4.4 DISPLAYING ITEMS OF A DOUBLY LINK LIST

In doubly link list, traversal is possible in both the direction. We can start from the first node and using the next pointer can reach upto the last node. Similarly, from the last node, we can reach to the first node by using the previous pointer. We have employed both the method to traverse the doubly link list. Each of them has been enumerated in the following programs.

```
Program: To display the item of a doubly link list
Solution:
//traversing from first to the last node using next pointer
void doubly_display()
{
dnode *current;
current=first;
while(current!=NULL)
{
```