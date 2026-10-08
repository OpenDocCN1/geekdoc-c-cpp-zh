# Chapter 19 Custom Linked Data Structures

firstNode lastNode

![](bbox=[0.15, 0.143, 0.848, 0.253])

Fig. 19.12 | Circular, doubly linked list.

# 19.5 Stacks

A stack may be viewed as a constrained version of a linked list—it receives new nodes and releases nodes only at the top. For this reason, a stack is referred to as a last-in, first-out (LIFO) data structure.

The primary operations to manipulate a stack are push and pop. Operation push adds a new node to the top of the stack. Operation pop removes the top of the stack and returns the data item from the popped node.

Stacks have many interesting applications. For example, when a program calls a method, the method must know how to return to its caller, so the return address is pushed onto the method-call stack. If a series of method calls occurs, the successive return values are pushed onto the stack in-list, first-out order so that each method can return to its caller. Stacks support recursive method calls in the same manner that they do for nonrecursive method calls.

In our next example, we take advantage of the close relationship between lists and stacks to implement a class by reusing a list class. We demonstrate two different forms of reusability. First, we implement the stack by inheriting from class List of Fig. 19.4. Then we implement an identically performing stack class through composition by including a List object as a private member of a stack class. The System.Generic namespace contains class for implementing and manipulating stacks that grow and shrink during program execution.

# Stack Class That Inherits from List

The code in Fig. 19.13 creates a stack by inheriting from class List of Fig. 19.4 (line 8 of Fig. 19.13). We want the stack to have methods Push, Pop, IsEmpty and Display. Essentially, these are the methods InsertAtFront, RemoveFront, IsEmpty and Display of class List. Of course, class List contains other methods (such as InsertBack and RemoveBack) that we would rather not make accessible through the public interface of the stack. It's important to remember that all methods in the public interface of class List are also public methods of the derived class StackInheritance (Fig. 19.13).