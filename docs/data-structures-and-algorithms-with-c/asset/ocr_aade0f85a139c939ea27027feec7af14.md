# RECURSION

> "Intelligence is the ability to avoid doing work, yet getting the work done" -Linus Torvalds

+   - Recursion essentials
+   - Types of Recursion
+   - Recursion tree
+   - Tower of Hanoi
+   - Non-attacking 8 queens

There are two approaches for writing repetitive algorithms. One uses iteration/loop and the other uses recursion. Iteration is one of the categories of control structures. It allows for the processing of some action many times. Iteration is also known as looping and repetition. The math term "to iterate" means to perform the statement parts of the loop. Many problems/tasks require the use of repetitive algorithms. Recursion is defined as defining anything in terms of itself. With most programming languages, this can be done with either:

+   i) Looping control structures, specifically the for loop (an iterative approach)
+   ii) The recursive calling of a function

Both approaches provide repetition, and either can be converted to the other's approach.

Definition: Recursion is a repetitive process in which a function calls itself either directly or indirectly.

In the other words, recursion is a technique that allows us to break down a problem into one or more sub-problems that are similar in form to the original problem.

In recursion, each time when the recursive function is called, the current state including all the local variables, formal parameters, and return address are pushed into the stack. A block of memory of contiguous locations set aside for this purpose. When the return statement is encountered, the control comes back to the previous function call, by restoring the state that resides on the stack.

# Recursion Essentials

There are two key requirements to make sure that the recursion is successful:

+   - A recursion definition must always have certain criteria, called *base criteria* or base case for which the function stop calling itself.
+   - Every recursive call must simplify the computation in some way, which is known as an *inductive clause*. In other words, each time a function does call itself (directly or indirectly), it must be closer to the base criteria that terminates the recursion.

# Infinite Regress

When the recursion does not terminate, we have an infinite regress. Infinite regress often occurs when:

+   i) A base criterion is omitted or
+   ii) When a base criterion is never reached.