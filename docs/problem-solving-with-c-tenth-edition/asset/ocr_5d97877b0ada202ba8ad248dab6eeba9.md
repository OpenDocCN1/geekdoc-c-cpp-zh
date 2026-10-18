in the order 'C', 'B', and then 'A'. This use of a stack is diagrammed in Display 13.16. As shown there, you can think of a stack as a hole in the ground. In order to get something out of the stack, you must first remove the items on top of the one you want. For this reason a stack is often called a last-in/first-out (LIFO) data structure.

Stacks are used for many language processing tasks. In Chapter 14 we will discuss how the computer system uses a stack to keep track of C++ function calls. However, here we will do only one very simple application. Our goal in this example is to show you how you can use the linked list techniques to implement specific data structures; a stack is one simple example of the use of linked lists. You need not read Chapter 14 to understand this example.

# PROGRAMMING EXAMPLE

# A Stack Class

The interface for our Stack class is given in Display 13.17. This particular stack is used to store data of type char. You can define a similar stack to store data of any other type. There are two basic operations you can perform on a stack: adding an item to the stack and removing an item from the stack.

# DISPLAY 13.17 Interface File for a Stack Class (part 1 of 2)

```
1  //This is the header file stack.h. This is the interface for the class Stack,
2  //which is a class for a stack of symbols.
3  #ifndef STACK_H
4  #define STACK_H
5  namespace stacksavitch
6  {
7      struct StackFrame
8      {
9          char data;
10         StackFrame *link;
11     };
12     typedef StackFrame* StackFramePtr;
13     class Stack
14     {
15     public:
16         Stack();
17         //Initializes the object to an empty stack.
18         Stack(const Stack& aStack);
19         //Copy constructor.
20         ~Stack();
21         //Destroys the stack and returns all the memory to the freestore.
```

(continued)