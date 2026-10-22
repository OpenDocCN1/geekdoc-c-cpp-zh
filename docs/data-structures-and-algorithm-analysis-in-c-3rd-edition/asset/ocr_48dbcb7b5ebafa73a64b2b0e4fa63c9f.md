![](bbox=[0.35, 0.07, 0.65, 0.22])

# Figure 4.7 Initial state of a linked list when using a header node.

Implementations for most member functions of the list class are straightforward. However, insert and remove should be studied carefully.

Inserting a new element is a three-step process. First, the new list node is created and the new element is stored into it. Second, the next field of the new list node is assigned to point to the current node (the one after the node that curr points to). Third, the next field of node pointed to by curr is assigned to point to the newly inserted node. The following line in the insert method of Figure 4.8 does all three of these steps.

```
curr->next = new Link<E>(it, curr->next);
```

Operator new creates the new link node and calls the Link class constructor, which takes two parameters. The first is the element. The second is the value to be placed in the list node’s next field, in this case “curr->next.” Figure 4.9 illustrates this three-step process. Once the new node is added, tail is pushed forward if the new element was added to the end of the list. Insertion requires Θ(1) time.

Removing a node from the linked list requires only that the appropriate pointer be redirected around the node to be deleted. The following lines from the remove method of Figure 4.8 do precisely this.

```
Link<E>* ltemp = curr->next;   // Remember link node
curr->next = curr->next->next; // Remove from list
```

We must be careful not to “lose” the memory for the deleted link node. So, temporary pointer ltemp is first assigned to point to the node being removed. A call to delete is later used to return the old node to free storage. Figure 4.10 illustrates the remove method. Assuming that the free-store delete operator requires constant time, removing an element requires Θ(1) time.

Method next simply moves curr one position toward the tail of the list, which takes Θ(1) time. Method prev moves curr one position toward the head of the list, but its implementation is more difficult. In a singly linked list, there is no pointer to the previous node. Thus, the only alternative is to march down the list from the beginning until we reach the current node (being sure always to remember the node before it, because that is what we really want). This takes Θ(n) time in the average and worst cases. Implementation of method moveToPos is similar in that finding the ith position requires marching down i positions from the head of the list, taking Θ(i) time.

Implementations for the remaining operations each require Θ(1) time.