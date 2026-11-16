
Dynamic data structures can be broadly classified as linear data structures and non-linear data structures. Linear data structures have a linear relationship between its adjacent elements. Linked lists are examples of linear data structures. A linked list is a linear dynamic data structure that can grow and shrink during its execution time. Elements can be inserted and deleted from any end of the list. If the elements are inserted and deleted in the same end, then the list is referred to as a Stack. If the elements are inserted in one end and deleted in another end, then the list is referred to as a Queue. A circular linked list is similar to a linked list except that the first and last nodes are interconnected.

Non-linear data structures does not have a linear relationship between its adjacent elements. In a linear data structure, each node has a link which points to another node, whereas in a non-linear data structure, each node may point to several other nodes. A tree is a non-linear dynamic data structure that may point to one or more nodes at a time. A graph is similar to tree except that it has no hierarchical relationship between its adjacent elements.

## 3.1.1 Stacks

A stack is an ordered collection of elements in which insertions and deletions are restricted to one end. The end from which elements are added and/or removed is referred to as the top of the stack. Stacks are also referred as “piles” and “push-down lists”. The first element placed in the stack will be at the bottom of the stack. The last element placed in the stack will be at the top of the stack. The last element added to stack is the first element to be removed. Hence stacks are referred as Last-In-First-Out (LIFO) lists.

Consider Fig. 3.1 where five discs are placed one over the other through a shaft. If we want to insert a new disc say 6. It is possible to insert the disc on the top of disc 5. Because of the presence of shaft, it is not possible to insert the disc 6 in the middle of the discs. Similarly, if we want to remove a disc say 4, it is only possible to remove the disc 5 first and then the disc 4 and so on. Because of the presence of the shaft, it is not possible to remove the disc from the middle of the discs. A similar operation is carried out in a stack.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_157_0.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_157_1.png)

Fig. 3.1 : Shaft with five discs.

Fig. 3.2 : Stack operation.

## 3.2 Array and its Representation using Stack

A stack is referenced via a pointer to the top element of the stack referred as *top pointer*. The top pointer keeps track of the top element in the stack. Initially, when the stack is empty, the top pointer has a value zero and when the stack contains a single element, the top pointer has a value one and so on. Fig. 3.1 shows the representation of a stack.

The primary operations that can be carried on a stack are insertions and deletions. These operations on a stack are referred as *PUSH* and *POP* operations respectively. A *PUSH* operation adds a new element to the stack. Each time a new element is inserted in the stack, the top pointer is incremented by one before the element is placed on the stack. A *POP* operation deletes the topmost element in the stack. Each time an element is removed from the stack the top pointer is decremented by one. The stack shown in *Fig. 3.2* consists of seven elements. We know that insertions and deletions can occur only at the top of the stack, which means *EIE* cannot be deleted until *IT* is deleted, *CSE* cannot be deleted until *IT* and *EIE* are deleted and so on. The elements from the stack may be popped (i.e., removed/deleted) only in the reverse order in which they are pushed (i.e., inserted/added) on to the stack.

One of the simplest ways of representing a stack is by means of a single dimensional array. Both stacks and arrays are ordered collection of elements, but an array and a stack are two different things. The number of elements in the array is fixed and it is not possible to change the number of elements, but the size of the stack varies continuously when elements are pushed and popped. The stack is stored in a part of the array, so an array can be declared large enough to hold the maximum number of elements of the stack.

During execution of a program, the stack size can be varied within the space reserved for it. One end of the array (i.e., bottom of the stack) is fixed and the other end of the array (i.e., top of the stack) is constantly changed depending upon the elements pushed and/or popped in the stack. Care must be taken in handling extreme cases, like not to push an element into a fully occupied stack and not to pop an element from an empty stack.

To represent a stack using arrays, we need,

- An Array to hold the elements of the stack, which can be of any data type such as int, char, float, etc.
- An integer variable to indicate the top position of the stack within the array.

### 3.2.1 Push Operation

PUSH is an operation used to add a new element into a stack. The PUSH operation of a stack is implemented using arrays. When implementing the PUSH operation, overflow condition of a stack is to be checked (i.e., you have to check whether the stack is full or not). If the size of the stack is defined as 15, then it is possible to insert (i.e., add) only 15 elements into the stack. It is not possible to add any more elements to the stack, since there is no space to accommodate the elements in the array.

The following procedure helps you to understand things better.

- Create a function PUSH() with one argument, the ELEMENT to be added.
- Assign the new element in the array by incrementing the TOP variable by 1.

### 3.2.2 Pop Operation

POP is an operation used to remove an element from the TOP of the stack. POP operation of a stack is also implemented using arrays. When implementing the POP operation, underflow condition of a stack is to be checked (i.e., You have to check whether the stack is empty or not). The user should not POP an element from an empty stack. This type of an attempt is illegal and should be avoided. If such an attempt is made, the user should be informed of the underflow condition.

The following procedure can help you to understand things better.

- Create a function POP() with one argument, the address of the element to store the popped value.
- Decrement the TOP variable by 1.

### 3.2.3 PEEK Operation

PEEK is an operation used to display the element from the TOP of the stack, pointed by the TOP pointer without actually removing it. PEEK operation of a stack is implemented using arrays. When implementing the PEEK operation, underflow condition of a stack is to be checked (i.e., You have to check whether the stack is empty or not). The user should not try to PEEK an element from an empty stack. This type of an attempt is illegal and should be avoided. If such an attempt is made, the user should be informed of the underflow condition.

The following procedure can help you to understand things better.

- Create a function PEEK() with one argument, the address of the element to store the top value.

### 3.2.4 Empty Stack

If a stack contains no elements, it is referred to as an empty stack. If an element is to be popped from a stack, or to view the contents of the stack, you have to check whether the stack is empty or not, since elements cannot be popped from an empty stack nor contents cannot be displayed from an empty stack. This type of an attempt is illegal and should be avoided. If such an attempt is made, the user should be informed of the underflow condition. To check whether the stack is empty or not, we are using a variable top in Program 3.1. Assume that you are initializing the variable top to -1. If the variable top is -1 during execution the output message “Stack underflow on POP” is displayed. This condition is referred as empty condition of a stack.
