# Object-Oriented Programming with C++

the user of the program may find that the size of the array is not enough to hold the number of elements that he/she needs to create.

Conversely, if the programmer specifies a very large value for the size of the array, the user may not use all of the elements of the array during run time. But, when it gets created during run time, occupies the space for all its elements even if they are not use. This will lead to wastage of space especially if each element is a large object. Also, we cannot easily insert a new at the beginning or in the middle of the array.

Linked lists (a type of data structure) are a good substitute for arrays. They do not have the above limitations of arrays. But, in order to use them and other data structures, you need to write special programs to create and then use them or use libraries that can create them for you.

Arrays have one more limitation. They have a linear structure. One element of the array is followed by only one element. But our programming may require us to link one element to two or more. Trees (another type of data structure) enable us to fulfill this programming need. Again, just like linked lists, you need to write special programs to create and use trees or use libraries that can create them for you.

Data structures can be used to solve a number of programming problems like creating database software, engineering problems, etc. They can be created using various programming languages, C++. We can create various data structures by utilizing classes, functions, pointers, and the delete operators,

# 9.2 Linked Lists

Linked lists are data structures. They consist of nodes that are linked to each other in a linear fashion. Each node in a linked list is an object that is made up of two parts. The first part is data carried by the node. The second part of node is a pointer that carries the address of the node in the list. This is how a node is linked to the node.

Each node in a linked list is linked to exactly one node (Note that we are talking about linked lists. We also have double linked lists where one node is connected to two nodes–the next node in the list and the previous node in the list). 9.2 illustrates a sample structure of a single linked list.

This figure shows that each of the four nodes represents a node and the address of each node has been mentioned above the box it represents. The address of the first node is 6327, that of the second node is 9243, that of the third node is 743, and that of the last node is 8138. Let us ignore the node labelled head for the time being.

In this specific case, each node carries data as the data. But, we can embed any type of data. The data carried by the first node is 4527, that by the second node is 55, that by the third node is 3281, and by the last node is 21629.

As we know, the second part of each node is a pointer that carries the address of the next node in the list. the address stored inside the first node is 9243 (which is the address of the second node), the address stored inside the second node is 743 (which is the address of the third node), and the address stored inside the third node is 8138 (which is the address of the fourth node). The address stored inside the fourth node is NULL (which indicates that it is not connected to any other node and is therefore the last node).

We also need to store the address of the first node. This is where the head pointer comes into play. It stores the address of the first node (6327 in this case).