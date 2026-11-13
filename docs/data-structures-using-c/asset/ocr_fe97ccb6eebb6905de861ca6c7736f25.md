Now, through `Head` we have access to the last node, and it also (`Head->next`) gives us the address of the first node.

# 6.8.2 Circular Linked List with Header Node

Consider a circular list with a single node in the list (Fig. 6.37).

![](bbox=[0.35, 0.23, 0.75, 0.29])

Fig. 6.37 Singly circular linked list with two nodes

Circular list with a single node has a problem of checking end of traversal as

```
(while(x->link != Head));
```

This would enter an infinite loop.

So, we can use a circular linked list with header node as shown in Fig. 6.38.

![](bbox=[0.35, 0.455, 0.75, 0.555])

Fig. 6.38 Singly circular linked list with header node

The circular list with header node drawn in Fig. 6.38 can be redrawn as in Fig. 6.39.

![](bbox=[0.3, 0.645, 0.8, 0.705])

Fig. 6.39 Singly circular linked list with header node–representation 2

Suppose we want to insert a new node at the front of this list. We have to change the link field of the last node. In addition, we have to traverse the whole list to reach till the last node as the link field of the last node is also to be updated. Hence, it is convenient if the head pointer points to the last node rather than the header node, which is the first node of the list.

If the singly headed circular linked list has a head pointer as shown in Fig. 6.40, then a node can easily be inserted at the front and also at the rear of the list.