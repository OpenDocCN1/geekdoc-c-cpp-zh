+   8. Describe how to modify the calculator program in Figure 7.5 on page 364 to allow for comments in the calculator input. Comments appear at the end of the expression, starting with a double slash // and continuing to the end of the line.
+   9. What possible errors could cause a stack underflow in the calculator program in Figure 7.5 on page 364?
+   10. Do an analysis to determine what kind of expressions cause the stack to grow large in the calculator program in Figure 7.5 on page 364.
+   11. How are the iostream functions peek and ignore similar to the top and pop operations of a stack? How are they different?
+   12. What is the time analysis, in big-O notation, of the arithmetic expressions evaluation algorithm? Explain your reasoning.

# 7.3 IMPLEMENTATIONS OF THE STACK CLASS

As a programmer, you can use the STL stack without knowing how it works. As a student of computer science, studying the implementations of a stack is good experience for your other programming. We will give two implementations of our stack class: a static implementation using a fixed-sized array, and a dynamic implementation using a linked list. Typical stack implementations in the Standard Library use a third approach (dynamic arrays).

# Array Implementation of a Stack

Figure 7.6 gives the header file for a stack template class that is similar to the STL stack. The class definition uses two private member variables for the stack:

+   1. An array, called data, that can hold up to CAPACITY items (where CAPACITY is a static constant of the stack class). This is a partially filled array, holding the stack's items in locations data[0], data[1], and so on.
+   2. A single member variable, used, that indicates how much of the partially filled array is currently being used. The entry at data[0] is at "the bottom" of the stack. The entry at data[used-1] is at "the top" of the stack. If the value of used is zero, this will indicate an empty stack.

In other words, our stack implementation is simply a partially filled array implemented in the usual way: an array and a variable to indicate the index of the last array position used. This description is the invariant of our class, so that each member function (except the constructor) may assume that the stack is represented in this way when the operation is activated. Each operation has the responsibility of ensuring that the stack is still represented in this manner when the operation finishes.

the stack entries are stored in a partially filled array