
8. Deallocate memory for Temp Node
9. Return

## Delete a Node from the doubly linked list having a specific DATA value

This algorithm finds and deletes a node whose value is ‘NO’. Temp is a pointer which holds the address of HEADER of the linked list.

### Algorithm to delete a node by value

```
ALGORITHM: DDEL (HEAD, NO)
1. Set Temp = HEAD //to make temp to point the first node
2. [Check for empty list]
If HEAD = NULL then
Print: “The linked list is empty” and Return
3. Repeat Step 4 to 5 until temp is NULL
a) If Temp->DATA = NO then
i) if TEMP = HEAD then// node to be deleted is the first node
Set Temp = Temp->RLINK
Set Temp->RLINK->LLINK = NULL
Else if Temp->RLINK = NULL //Check for last node
Set P=Temp->LLINK
Set POST= Temp->RLINK
Set P->RLINK=NULL
Else
Set POST->LLINK = Temp->LLINK
Set P->RLINK=Temp->RLINK
ii) Deallocate memory for Temp Node // de allocate node
iii)Return
Else
Set Temp = Temp->RLINK
4. Print: “Element not found”
5. Return
```

Following figure 5.26a denotes a doubly linked list where HEAD points to the first node of the list.

![](img/723fa3ef35f5102eb67dc45b74bb823d_138_0.png)

If the first node to be deleted, then how the list will look is presented in the following figure 5.26b.

![](img/723fa3ef35f5102eb67dc45b74bb823d_138_1.png)

In the following figure 5.26c deletion of a node from last position of doubly linked list is described.

![](img/723fa3ef35f5102eb67dc45b74bb823d_139_0.png)

### (c)

In the following figure 5.26d, the deletion of a node which is after a specific node P is shown.

![](img/723fa3ef35f5102eb67dc45b74bb823d_139_1.png)

### (d)

In the succeeding figure it is pictorially presents that how a node to be deleted which is before a specific node of a doubly linked list.

![](img/723fa3ef35f5102eb67dc45b74bb823d_139_2.png)

### (e)

## Figure 5.26 (a-e): Node deletion at any position in a doubly linked list

## Time Complexity of Doubly Linked list

The time complexity for insertion and deletion from a doubly linked list is O(1), as there is no movement of nodes just by exchanging some pointers then a new node can be inserted or an existing node can be deleted. Whereas for traversal, the complexity is O(n).

## Circular Doubly Linked List:

The advantages of both double linked list and circular linked list are incorporated into another list structure that is called circular doubly linked list and it is known to be the best of its kind.

The following is a schematic representation of a circular doubly linked list.

![](img/723fa3ef35f5102eb67dc45b74bb823d_139_3.png)

## Figure 5.27: Circular Doubly linked list

As per above shown illustrations, following are the important points to considered.

- Last Link's rlink points to the first node of the list in both cases of singly as well as doubly linked list.
- First Link's link points to the last node of the list in case of doubly linked list.

## Disadvantages of Linked List

- Linked list consumes more memory space for storing addresses of the next node.
- Searching will be slow as only linear searching will be possible.
- Direct access to any node not possible, therefore, if a node required to access it is required to traverse from the first node onwards until the desired node is found.

Therefore, arrays are suitable when a large number of searching operations are necessary, but insertion/deletion is very small in number. Whereas linked-list are suitable, when there will be frequent insertion/deletion, but very few search operations are required.

## Summary

- A linked list is a linear ordered collection of finite homogeneous data elements called node.
- The linked list overcomes the demerits of array in terms of memory allocation.
- Linked list can be classified into 4 types single linked list, circular linked list, doubly linked list and circular doubly linked list.
- Polynomial addition can be done using linked list.
- Addition, Deletion and Insertion of a node in a linked list is faster than array.

## Exercises

1. What are the advantages and disadvantages of linked list data structure over an array?
2. Write an algorithm to insert the data X after a specific data item Y in the linked list.
3. Write a function to delete the n<sup>th</sup> node of a singly linked list. The error conditions are to be handled properly.
4. Write an algorithm to delete any node from the singly linked list where the key value of the node is known.
5. Write an algorithm to delete a node from a doubly linked list.
6. Write an algorithm to delete all nodes having greater than a given value, from a given singly linked list.
7. Write a function to reverse the direction of all links of a singly linked list.
8. Write an algorithm to add two polynomials using linked list.
9. How the polynomial 4x<sup>3</sup> - 2x<sup>2</sup> + 3 can be represented using linked list?
10. Write a C program to create a doubly linked list in ascending order of information.
11. Write a C program to join two sorted linked list so that the third list is in sorted order.
12. Write a C program to show the information of a doubly linked list in reverse order.
13. Write a C program to INSERT and DELETE node in a circularly doubly linked list. Display the elements of the list.
14. Write C program to insert an element in a sorted doubly linked list, so that the list remain in sorted order after insertion.
15. Write a program in C language to find the predecessor of a node in linked list.
16. Choose the correct alternatives for the following:

- i) The situation when in a linked list START = NULL is
  - a) Underflow b) Overflow c) Saturated d) None

- ii) A linked list follows
  - a) random access mechanism b) sequential access mechanism
  - c) no access mechanism d) none of these.

- iii) A linear collection of data elements where the linear node is given by means of pointer is called
  - a) Linked list b) Node list c) Primitive list d) None of these.

- iv) In linked list representation a node contains at least
  - a) node address field, data field b) node number field, data field
  - c) next address field, information field d) none of these.

- v) Inserting a new node after a given node in a doubly linked list requires
  - a) four pointer exchanges b) two pointer exchanges
  - c) one pointer exchanges d) no pointer exchange.

- vi) The nth node in a singly linked list can be accessed via
  - a) The head node b) The tail node c) (n-1)th node d) None

- vii) Linear order in linked list is provided through
  - a) Index number b) The implied position of the node c) Pointer d) None

- viii) Null pointer is used to tell
  - a) End of a linked list b) Empty pointer field of a structure
  - c) The linked list is empty d) All the above

- ix) In linked list the successive elements
  - a) Must occupy contiguous space in memory
  - b) Need not occupy contiguous space in memory
  - c) Must not occupy contiguous space in memory
  - d) None of the above

- x) Searching in a linked list requires linked list be created
  - a) In sorted order b) In any order c) Without underflow condition d) None of the above

- xi) Deletion of a node in linked list involves keeping track of the address of the node
  - a) Which immediately follows the node that is to be deleted
  - b) Which immediately precedes the node that is to be deleted
  - c) The node to be deleted
  - d) None of the above

- xii) Header in a linked list is a special node at the
  - a) End of the linked list b) At middle of a linked list
  - c) Beginning of the linked list d) None of the above

- xiii) Header linked list in which last node points to the header node is called
  - a) Grounded header list b) Circular header list c) General header list d) None of the above

- xiv) Representing polynomial using linked list requires each node having
  - a) Two fields b) Three fields c) More than three fields d) None of the above

- xv) Inserting a node after a given node in a doubly linked list requires
  - a) One pointer change b) Two pointer change c) Four pointer change d) None of the above
