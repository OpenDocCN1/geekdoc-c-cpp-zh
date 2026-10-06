
# Recursion

459

# Call Stack

![](img/06d4e84f27a8884ea40ba6182ec7c778_483_0.png)

**FIGURE 15.1:** This shows the stack for the function count which prints the numbers counting up. When you call the function with 5, it calls itself with 4 before doing anything else. This calls itself with 3 and so on to 0. The call with 0 does nothing but return. It returns back into the call to count(1) that does the print and continues back up the stack.

To understand how this works, consider figure 15.1. This shows a graphical representation for different frames on the call stack and what happens when you call count(5). The call immediately calls count(4) before it does anything else. The call to count(4) gets a new stack frame that keeps track of where it was in the call to count(5) so when it returns it goes back to that point. The call to count(4) also goes straight into a call to count(3), which also gets down to count(0) which does nothing at all. When the call to count(0) finishes, control returns to the call to count(1) and resumes back to the call to count(2), which is with the line with the statement. After it print, count(1) returns to count(2) which similarly does a print. Because the prints are happening as it pops up the stack, the numbers get printed in ascending order even though the function only includes a decrement. The memory of the stack is essential for this to work each stack frame remembers its value of n.

This is a very important point to remember about recursive calls. While the recursive calls have the same names, they are not the same variables. It is like multiple people with the same name. Just because two or three people are named "Pat", that does not mean they are the same person. In this case, there were six versions of n that were created, and they took on the values from 5 down to 0. Each was distinct from the others and occupied different parts of memory.

This example shows how the stack can come into play with recursion, but it does not really show the power of recursion. To do that, we need to have a recursive function that can call itself more than once. In the following sections we will look at several different

# Introduction to Programming and Problem-Solving Using Scala

examples of this and see problems that really require the stack and are significantly harder to convert over loops.

# 15.3 Fibonacci Recursion

The classic example of recursion is Fibonacci numbers. This is a sequence of numbers where each number is defined as the sum of the previous two. In mathematical notation this is written as $f(n) = f(n-1) + f(n-2)$. This is not a complete definition, however, because we need to know how the sequence starts. That is to say that we need a base case for the recursion. It is customary to have the first two elements be 1. So, the sequence then is 1, 2, 3, 5, 8, 13, ...

We can write this function in Scala with a short function definition.

```scala
def fib(n:Int) = if (n<=2) 1 else fib(n-1)+fib(n-2)
```

For n=1 and n=2 we get 1. For n=3 we get 1. For larger numbers, the process is more complex, and it is instructive to visualize it. We do this by considering what happens on the call stack in a manner similar to figure 15.1. Unlike the code for figure 15.1, this function calls itself twice and that makes things a bit more complex.

For example, a call to fib(4). This is equal to fib(3)+fib(2). In order to know what is true, recursive calls have to be made to each of those functions. By convention, we imagine that the calls are processed from left to right. Unlike examples we have seen before, when fib(3) returns, there is another call to fib(2) still waiting. We immediately a new stack frame appears where the one for fib(3) had just been. This process of stack frames being removed to be replaced with new ones happens a lot in this calculation of the Fibonacci numbers as well as other recursive functions that themselves call more than once. Instead of drawing it as a vertical stack as was done in figure 15.1, it is customary to draw it in a branching structure called a tree as is drawn in figure 15.2. Each new stack frame is still below the one it called, but different stack frames at the same depth in the stack are drawn to next horizontally. Arrows are used to keep track of things.

In this representation, boxes represent the stack frames. We have dispensed with the function names and left only the argument value. The straight arrows show function calls. The curved arrows show returns and are labeled with result values. These types of diagrams can be very helpful when you are trying to see what happens in a complex recursive function. When you draw them yourself can dispense with the boxes arrows. Arrows with lines between them typically suffice.

The Fibonacci numbers are a standard example of recursion, but they are not a great one outside of instructional purposes. You can fairly easily write a function that calculates Fibonacci numbers that use a loop instead of recursion, and it will be much faster. That is true of the examples that follow

![](img/06d4e84f27a8884ea40ba6182ec7c778_485_0.png)

**FIGURE 15.2:** This figure shows a call tree for fib(4). Boxes represent stack frames. Straight arrows point in the direction of function calls. Curved arrows show returns and are labeled with result values.

# 15.4 Towers of Hanoi

Our next example of this more powerful recursive functions is somewhat playful. You have likely seen and perhaps played Towers of Hanoi. It is a “game” played with three pegs and a number of disks of different sizes that have holes in them; so, they can be put on the pegs. Your goal in playing is to move the disks from one peg to another following two rules:

- 1. You can move one disk at a time.
- 2. No disk can be placed on a smaller disk than it.

We want to write a program that can solve this. To do so, we need to first analyze the problem bit more. If you start picturing a peg with 7 disks on stacked from largest to the bottom to the smallest and to pick the solution, you will probably have a hard time. The easiest setup is when you have one disk. Move the disk from where it started to the peg you want to end on. This was bit, but we just saw how to move two disks. Using that, we move two disks to the middle peg. Then the largest is moved to the end peg and the two disks are moved on top of it. This points to a general solution. If we make the assumption that we know how to move N - 1 disks, we can move N disks by first moving the N - 1 disks to the off peg, moving the largest one to the destination, then the N - 1 disks back on top of the largest one. This is a recursive definition. A base case is one where we move a single disk across.
