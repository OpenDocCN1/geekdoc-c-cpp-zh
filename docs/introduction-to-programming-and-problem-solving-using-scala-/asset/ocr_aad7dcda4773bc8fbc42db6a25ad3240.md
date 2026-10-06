# Recursion

459

# Call Stack

![](bbox=[0.373, 0.133, 0.006626, 0.396])

**FIGURE 15.1:** This shows the stack for the function count which prints the numbers counting up. When you call the function with 5, it calls itself with 4 before doing anything else. This calls itself with 3 and so on to 0. The call with 0 does nothing but return. It returns back into the call to count(1) that does the print and continues back up the stack.

To understand how this works, consider figure 15.1. This shows a graphical representation for different frames on the call stack and what happens when you call count(5). The call immediately calls count(4) before it does anything else. The call to count(4) gets a new stack frame that keeps track of where it was in the call to count(5) so when it returns it goes back to that point. The call to count(4) also goes straight into a call to count(3), which also gets down to count(0) which does nothing at all. When the call to count(0) finishes, control returns to the call to count(1) and resumes back to the call to count(2), which is with the line with the statement. After it print, count(1) returns to count(2) which similarly does a print. Because the prints are happening as it pops up the stack, the numbers get printed in ascending order even though the function only includes a decrement. The memory of the stack is essential for this to work each stack frame remembers its value of n.

This is a very point to remember about recursive calls. While the recursive calls have the same names, they are not the same variables. It is like multiple people with the same name. Just because two or three people are named "Pat", that does not mean they are the same person. In this case, there were six versions of n that were created, and they took on the values from 5 down to 0. Each was distinct from the others and occupied different parts of memory.

This example shows how the stack can come into play with recursion, but it does not really show the power of recursion. To do that, we need to have a recursive function that can call itself more than once. In the following sections we will look at several different