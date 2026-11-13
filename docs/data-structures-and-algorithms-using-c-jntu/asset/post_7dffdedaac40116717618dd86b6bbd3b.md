
- Doubly linked list is the one in which each node of it contains two links pointing to either side of the nodes.
- Applications of linked list are sparse matrix representation, polynomial manipulation, dynamic memory storage, in symbol table, etc.

## EXERCISES

### Fill in the Blanks

- 1. Linked lists are ________________.
- 2. A node in a linked list consists of __________ and __________.
- 3. __________ is a pointer to a list of available memory spaces.
- 4. __________ are the types of linked list.
- 5. A node in a doubly linked list contains __________ and __________ pointers.
- 6. __________ are the applications of linked list.
- 7. Circular linked lists are used to overcome __________ disadvantage of a singly linked list.

### Multiple-choice Questions

- 1. Linked lists are __________ structures.
   - a. Static data   b. Dynamic data
   - c. Non-linear data  d. None

- 2. Which of the following statements is true?
   - a. Insertion in a linked list can be done only at front
   - b. Traversing the list in only one direction
   - c. Operations on a linked list can be performed anywhere in the list
   - d. Both a and b

- 3. The situation when in a linked list START=NULL is
   - a. Underflow      b. Overflow
   - c. Houseful       d. Saturated

- 4. Which of the following is a two-way list?
   - a. Grounded header list      b. Circular header list
   - c. Linked list with header and trailer nodes   d. None

- 5. __________ is an application of a linked list.
   - a. Towers of Hanoi   b. Recursion
   - c. Sparse matrices   d. CPU scheduling

### Short-answer Questions

- 1. Define a linked list.
- 2. Define a singly linked list.
- 3. Define a doubly linked list.
- 4. Give one disadvantage and one advantage of a singly linked list.
- 5. Give one disadvantage and one advantage of a doubly linked list.
- 6. List out four applications of linked lists.
- 7. Differentiate between a singly linked list and a doubly linked list.
- 8. Define a circular singly linked list with an example.
- 9. Briefly explain with diagrams how a node can be added to the linked list.
- 10. Differentiate between a doubly linked list and a circular singly linked list.

### ESSAY QUESTIONS

- 1. With an example discuss how the data structure linked list is represented in memory.
- 2. Explain the following operations in a doubly linked list:
   - (i) Create (ii) Insert (iii) Delete
   - (iv) Display (v) Insert at a given position
- 3. Implement concatenation of two circular singly linked lists List1 and List2. Use header nodes to implement the list.
- 4. Write an algorithm to implement the following on a singly linked list.
   - (i) To find the average of a set of values
   - (ii) To replace all the occurrences at a given value by another value from the list.
   - (iii) To insert a given value in to its proper position.
- 5. Write an algorithm to implement insertion and deletion on a singly linked list.
- 6. Write the algorithms for implementing various operations on a circular doubly linked list.
- 7. Write a program to perform polynomial multiplication using a linked list.

## Stacks

Stack data structure is exclusively discussed in this chapter. Representation and implementation of stacks are explained along with examples. Four of the common applications are stated and illustrated in detail.

### 6.1 DEFINITION

A stack is a linear data structure in which insertion and deletion of elements are done at only one end, which is termed as Top of stack. The last element that is inserted will be the first element to be deleted. Therefore, this is referred to as a Last In First Out (LIFO) structure.

- **Examples**
  1. The stack of trays in a cafeteria
  2. A stack of plates in a cupboard

Let ST be a stack with elements 10, 20, 30. The element 30 is pointed by the top. When the new element 40 is to be added, it is inserted at the top. Now Top is pointing to the element 40 as in Figure 6.1(a). When deletion of an element is to be performed, the element pointed by the top is removed first, i.e. 40 is removed first as shown in Figure 6.1(b).

![](img/45784b9f0334626143002ec0d63692fd_191_0.png)

Figure 6.1 Stack and its working

![](img/45784b9f0334626143002ec0d63692fd_192_0.png)

### 6.2 REPRESENTATION OF A STACK

The representation of a stack in the memory can be done in two ways. They are as follows:

- Static representation using arrays
- Dynamic representation using linked lists

#### 6.2.1 ARRAY REPRESENTATION OF A STACK

Stack can be represented using a one-dimensional array. Allocate a block of memory required to accommodate the full capacity of the stack, and the items of a stack are stored in a sequential manner from the first location of the memory block.

![](img/45784b9f0334626143002ec0d63692fd_192_1.png)

Figure 6.2 Stack and its array representation

In Figure 6.2(a), stack is a one-dimensional array. Top is a pointer that points to the top element in the stack.

#### 6.2.2 LINKED REPRESENTATION OF A STACK

Representing a stack using arrays is easy and convenient. However, it is useful for fixed sized stacks. Sometimes in a program, the size of a stack may be required to increase during execution, i.e. dynamic creation of a stack. Using a linked list, a stack can be dynamically created. A singly linked list is used to represent a stack. Figure 6.3 shows the linked representation of the stack. Here, the node consists of data and link fields. Data field is to store the items and data link field is to point to the next field.

![](img/45784b9f0334626143002ec0d63692fd_193_0.png)

Figure 6.3 Linked representation of a stack

The item in the first node is the top of the stack and the item in the last node is the bottom of the stack.

### 6.3 OPERATIONS ON STACK

The basic operations on stacks are:

- (i) PUSH—insertion of the elements into a stack
- (ii) POP—deletion of the elements from the stack

Push operation: Inserting an element into the stack is called push operation. Check for Stack Overflow condition i.e. whether the stack is full of elements or not before performing Push operation. Every time an element is pushed into the stack, the top must be incremented. In Figure 6.4, the stack has 2 elements 10, 5.

![](img/45784b9f0334626143002ec0d63692fd_193_1.png)

Figure 6.4 Push operation

Pop operation: Deleting an element from the stack is called Pop operation. Check for the Stack Underflow condition before performing Pop operation, i.e. whether the stack is empty or not. Every time an element from the stack is deleted, the top must be decremented by one. Now, the top points to the current top element of the stack. In Figure 6.5, the stack is empty after popping all the elements.

![](img/45784b9f0334626143002ec0d63692fd_194_0.png)

Figure 6.5 Pop operation

Push and Pop are the two important operations that are performed on the stack. In addition, Show and Size operations can also be performed on a stack. Show operation displays all the elements of the stack if it already has some elements. If not (i.e., if the stack is empty) it displays a message that the stack is empty. Size operation returns the number of elements in the stack.

#### 6.3.1 ARRAY IMPLEMENTATION OF A STACK

Suppose STACK [1 : N] is a linear array that represents a stack. Top is a pointer variable that holds the location of the top element of the stack and N is the number of elements that can be stored in a stack. Top = 0 or NULL represents that the stack is empty, and Top = N represents that the stack is full. The following are the algorithms for Push and Pop operations using arrays.

#### Algorithm 6.1: PUSH (STACK, N, TOP, ITEM)

This algorithm pushes an ITEM into a STACK; N is the maximum size of a stack.

- 1. [check for stack overflow]
   If Top=N then write:"stack overflow" and return
- 2. Set Top=Top+1 //increment Top by 1
- 3. Set STACK[Top] = ITEM //insert item in new Top position
- 4. End

#### Algorithm 6.2: POP (STACK, TOP, ITEM)

This algorithm deletes the top element of the STACK and assigns it to the variable ITEM.

- 1. [check for stack underflow]
   If Top=0 then write:stack underflow and return
- 2. Set ITEM=STACK[Top] //initializing Item with Top element
- 3. Set Top=Top-1 //Decrementing top by 1
- 4. End

Consider a stack with five elements called NUMBERS [1:5] of numerical values. The insertion of values 10,20, 30,40,50 and deletion are shown in Figure 6.6.
