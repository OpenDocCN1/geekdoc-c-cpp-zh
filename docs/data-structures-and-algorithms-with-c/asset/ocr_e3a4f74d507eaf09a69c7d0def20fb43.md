# LINKED LIST

In arrays, there is always a fixed relationship between the addresses of two consecutive elements as all the items of an array must be stored contiguously. However, note that this contiguity requirement makes expansion or contraction of the size of the array difficult. In linked list, data items may be scattered arbitrarily all over the memory, but we can achieve fast insertion and deletion in a dynamic situation.

Definition: A linked list is a linear ordered collection of finite homogeneous data elements called node, where the linear order is maintained by means of links or pointers.

A linked list allocates space for each element separately in its own block of memory called a "linked list element" or "node". The list structure is created by the use of pointers to connect all its nodes together like the links in a chain.

In an array if the address of one element is known, addresses of all other elements become automatically known. Since, in a linked list, there is no relationship between the addresses of elements, each element of a linked list must store explicitly the address of the element next to it.

# Table 5.1: Difference between Array and Linked list

| Property | Array | Linked List |
| :--- | :--- | :--- |
| Storage | Storage of the array must be available contiguously. | Storage need not be contiguous. |
| Memory utilization | The size of the array needs to be predicted beforehand because memory allocation is done in advance. | Memory of linked list is not pre-allocated, memory is allocated whenever it is required. |
| Memory utilization | Not necessary for storing addresses of any element. | Extra memory space is necessary for storing addresses of the next node |
| Change of size | The array size is fixed, extend or shrink not possible during the execution of a program | Linked list may extend or shrink during the execution of a program |
| Insertion/deletion | Insertion/deletion operations are slow, half of the elements are required to move on an average | Insertion/deletion operations are performed very fast, in a constant amount of time |
| Searching | Linear searching, binary searching, interpolation searching are possible | Binary searching, interpolation searching not possible, only linear searching is possible |
| Access element | Fast access to any element in a constant amount of time. | To access any element in a linked list, traversing is required. |
| Joining/splitting | Joining and splitting of the two arrays | Joining and splitting of two linked list is very easy. |

# Advantages of linked list

Linked lists have many advantages. Some of the very important advantages are:

+   i) Linked list are dynamic data structures. That is, they can extend or shrink during the execution of a program.
+   ii) Storage need not be contiguous.
+   iii) Efficient memory utilization. Here memory is not pre-allocated. Memory is allocated whenever it is required.
+   iv) Insertion or deletion is easy and efficient, may be done very fast, in a constant amount of times,