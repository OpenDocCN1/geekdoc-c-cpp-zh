distance apart, whereas linked lists do not necessarily contain consecutive memory locations. These data items can be stored anywhere in the memory in a scattered manner. To maintain the specific sequence of these data items, we need to maintain link(s) with a successor (and/ or a predecessor). It is called as a linked list as each node is linked with its successor (and/ or predecessor). Figures 6.1 and 6.2 show the realization of a linear list using a linked list.

![](bbox=[0.25, 0.23, 0.85, 0.27])

# Fig. 6.1 A linked list of n elements

![](bbox=[0.25, 0.31, 0.85, 0.42])

# Fig. 6.2 A linked list of days in a week

The linked list, as a data structure in programming, is used quite frequently since it is very efficient. To use linked lists effectively, the concepts of pointers must be very clear to the programmer. In fact, frequent use of linked lists makes the concept of pointers very clear to the programmer. This study of the linked list will introduce us to its strengths and weaknesses. This study gives us an appreciation of the time, space, and code complexity issues. Linked list examples are a classic combination of algorithms and manipulation of pointers. Let us now learn about the linked list.

# 6.2 LINKED LIST

A linked list is an ordered collection of data in which each element (node) contains a minimum of two values, data and link(s) to its successor (and/or predecessor). A list with one link field using which every element is associated to its successor is known as a singly linked list (SLL). In a linked list, before adding any element to the list, a memory space for that node must be allocated. A link is made from each item to the next item in the list as shown in Fig. 6.3.

![](bbox=[0.25, 0.78, 0.85, 0.88])

# Fig. 6.3 Linked list