To illustrate, a linked list storing the integers 9, 17, 22, 26, 34 might be pictured as follows:

![](bbox=[0.18, 0.115, 0.75, 0.21])

In this diagram, arrows represent links, and first points to the first node in the list. The data part of each node stores one of the elements of the list, and each arrow from a next part represents a pointer. The symbol in the last node (a version of the ground symbol used in electrical engineering) represents a null link and indicates that this list element has no successor.

# 15.3.1.1 Insert Operation

To see how linked lists make it possible to avoid the data-shifting problem of arrays and vector<T>, suppose we wish to insert 20 after 17 in the preceding linked list, and that predptr points to the node containing 17. We first obtain a new node (via the new operator) temporarily pointed to by newptr and store 20 in its data part:

![](bbox=[0.17, 0.495, 0.8, 0.61])

We insert it into the list by first setting its next part equal to the link in the node pointed to by predptr so that it points to its successor:

![](bbox=[0.17, 0.695, 0.8, 0.81])

Now reset the link in the predecessor node to point to this new node:

![](bbox=[0.17, 0.875, 0.8, 0.99])