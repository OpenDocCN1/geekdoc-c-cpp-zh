![](bbox=[0.131, 0.117, 0.188, 0.158])

# Common Programming Error 6.14

Recall that the && and || operators use short-circuit evaluation. Placing an expression with a side effect on the right side of a && or || operator is a logic error if that expression should always be evaluated.

# Exponential Complexity

A word of caution is in order about recursive programs like the one we use here to generate Fibonacci numbers. Each level of recursion in function `fibonacci` has a *doubling* effect on the number of function calls; i.e., the number of recursive calls that are required to calculate the *n*th Fibonacci number is on the order of 2ⁿ. This rapidly gets out of hand. Calculating only the 20ᵗʰ Fibonacci number would require on the order of 2²⁰ or about a million calls, calculating the 30ᵗʰ Fibonacci number would require on the order of 2³⁰ or about a billion calls, and so on. Computer scientists refer to this as **exponential complexity**. Problems of this nature humble even the world’s most powerful computers! Complexity issues in general, and exponential complexity in particular, are discussed in detail in the upper-level computer science course generally called “Algorithms.”

![](bbox=[0.131, 0.421, 0.188, 0.46])

# Performance Tip 6.8

Avoid Fibonacci-style recursive programs that result in an exponential “explosion” of calls.

# 6.22  Recursion vs. Iteration

In the two previous sections, we studied two recursive functions that can also be implemented with simple iterative programs. This section compares the two approaches and discusses why you might choose one approach over the other in a particular situation.

+   - Both iteration and recursion are *based on a control statement*: Iteration uses a *repetition structure*; recursion uses a *selection structure*.

+   - Both iteration and recursion involve *repetition*: Iteration explicitly uses a *repetition structure*; recursion achieves repetition through *repeated functional calls*.

+   - Iteration and recursion each involve a *termination test*: Iteration terminates when the *loop-continuation condition fails*; recursion terminates when a *base case is recognized*.

+   - Iteration with counter-controlled repetition and recursion each gradually approach termination: Iteration *modifies a counter* until the counter assumes a value that makes the loop-continuation condition fail; recursion produces *simpler versions of the original problem* until the base case is reached.

+   - Both iteration and recursion *can occur infinitely*: An infinite loop occurs with iteration if the loop-continuation test never becomes false; *infinite recursion* occurs if the recursion step does not reduce the problem during each recursive call in a manner that converges on the base case.

# Iterative Factorial Implementation

To illustrate the differences between iteration and recursion, let’s examine an iterative solution to the factorial problem (Fig. 6.31). A repetition statement is used (lines 23...24 of