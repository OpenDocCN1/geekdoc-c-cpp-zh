*****MAIN MENU*****
1. PUSH
2. POP
3. PEEK
4. DISPLAY
5. EXIT
Enter your option : 1
Enter the number to be pushed on stack : 500

# 7.4 LINKED REPRESENTATION OF STACKS

We have seen how a stack is created using an array. This technique of creating a stack is easy, but the drawback is that the array must be declared to have some fixed size. In case the stack is a very small one or its maximum size is known in advance, then the array implementation of the stack gives an efficient implementation. But if the array size cannot be determined in advance, then the other alternative, i.e., linked representation, is used.
The storage requirement of linked representation of the stack with n elements is O(n), and the typical time requirement for the operations is O(1).
In a linked stack, every node has two parts—one that stores data and another that stores the address of the next node. The START pointer of the linked list is used as top. All insertions and deletions are done at the node pointed by top. If top = NULL, then it indicates that the stack is empty.
The linked representation of a stack is shown in Fig. 7.13.

![](bbox=[0.285, 0.475, 0.775, 0.5])

Figure 7.13 Linked stack

# 7.5 OPERATIONS ON A LINKED STACK

A linked stack supports all the three stack operations, that is, push, pop, and peek.

# 7.5.1 Push Operation

The push operation is used to insert an element into the stack. The new element is added at the topmost position of the stack. Consider the linked stack shown in Fig. 7.14.

![](bbox=[0.315, 0.65, 0.745, 0.68])

Figure 7.14 Linked stack

To insert an element with value 9, we first check if top=NULL. If this is the case, then we allocate memory for a new node, store the value in its data part and NULL in its next part. The new node will then be called top. However, if top!=NULL, then we insert the new node at the beginning of the linked stack and name this new node as top. Thus, the updated stack becomes as shown in Fig. 7.15.

![](bbox=[0.295, 0.8, 0.775, 0.83])

Figure 7.15 Linked stack after inserting a new node

Figure 7.16 shows the algorithm to push an element into a linked stack. In Step 1, memory is allocated for the new node. In Step 2, the data part of the new node is initialized with the value to be stored in the node. In Step 3, we check if the new node is the first node of the linked list. This