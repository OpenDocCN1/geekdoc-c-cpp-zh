# EXAMPLE: *(continued)*

Stacks are used for many language processing tasks. Chapter 13 discussed how the computer system uses a stack to keep track of C++ function calls. However, here we will only be concerned with one very simple application. Our goal in this example is to show how you can use the linked list techniques to implement specific data structures, such as a stack.

The interface for our stack class is given in Display 17.17. This is a template class with a type parameter T for the type of data stored in the stack. One item stored in the stack is a value of type T. In the example we present, T is replaced by the type char. However, in most applications, an item stored in the stack is likely to be a struct or class object. Each record (item of type T) that is stored in the stack is called a **stack frame**, which will explain why we occasionally use stackFrame as an identifier name in the definition of the stack template class. There are two basic operations you can perform on a stack: adding an item to the stack and removing an item from the stack.

Adding an item is called **pushing** the item onto the stack, and so we called the member function that does this push. Removing an item from a stack is called **popping** the item off the stack, and so we called the member function that does this pop.

The names push and pop derive from a particular way of visualizing a stack. A stack is analogous to a mechanism that is sometimes used to hold plates in a cafeteria. The mechanism stores plates in a hole in the countertop. There is a spring underneath the plates with its tension adjusted so that only the top plate protrudes above the countertop. If this sort of mechanism were used as a stack data structure, the data would be written on plates (which might violate some health laws but still makes a good analogy). To add a plate to the stack, put it on top of the other plates, and the weight of this new plate pushes down the spring. When you remove a plate, the plate below it pops into view.

Display 17.18 shows a simple program that illustrates how the Stack class is used. This program reads a line of text one character at a time and places the characters in a stack. The program then removes the characters one by one and writes them to the screen. Because data is removed from a stack in the reverse of the order in which it enters the stack, the output shows the line written backward. We have included the implementation of the Stack class in our application program, as we normally do with template classes. That means we cannot run or even compile our application program until we do the implementation of our Stack class template.

The definitions of the member functions for the template class Stack are given in the implementation file shown in Display 17.19. Our stack class is implemented as a linked list in which the head of the list serves as the top of the stack.

+   - push
+   - pop