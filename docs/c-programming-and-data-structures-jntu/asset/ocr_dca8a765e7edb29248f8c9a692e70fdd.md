![](bbox=[0.18, 0.13, 0.88, 0.22])

Fig. 15.21

In a doubly linked circular list, the backward link of the last node points to the first node and the forward link of the first node points to the last node. Unlike circular linked lists, we can easily insert a node in the middle of a doubly linked circular list, because it is not necessary to search the entire list to find the address of the preceding node. Fig. 15.22 shows how the new node Y is inserted before the node, X in the doubly linked circular list:

![](bbox=[0.2, 0.44, 0.85, 0.62])

Fig. 15.22

To insert a new node Y, the forward link of the node A now points to the node Y and the backward link of the node, Y points to node A. Similarly the forward link of new node Y points to the node X and the backward link of the node, X points to the node, Y.

Fig. 15.23 illustrates the deletion of a node X from the doubly linked circular list:

![](bbox=[0.18, 0.84, 0.88, 0.92])

Fig. 15.23

In the above figure, the forward link points to the node Z and the backward link of Z points to node A so that the node X is automatically deleted from the list.

# 15.13 STACKS AND QUEUES USING LINKED LIST

In the previous chapter, we have seen the implementation of stacks and queues using arrays. In this section, we will discuss how stacks and queues are implemented using linked lists. Unlike arrays, when using linked lists, the memory is allocated dynamically when new data is inserted into the stacks and queues.