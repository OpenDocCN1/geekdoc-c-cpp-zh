| Location in text (Part 2 of 2) | Recursion examples and exercises |
|---|---|
| *Chapter 6* | |
| Exercise 6.13 | “What does this program do?” exercise |
| Exercise 6.16 | “What does this program do?” exercise |
| Exercise 6.29 | Determine whether a string is a palindrome |
| Exercise 6.30 | Eight Queens |
| Exercise 6.31 | Print an array |
| Exercise 6.32 | Print a string backward |
| Exercise 6.33 | Minimum value in an array |
| *Chapter 21* | |
| Section 21.7, Fig. 21.5 | Mergesort |
| Exercise 21.8 | Linear search |
| Exercise 21.9 | Binary search |
| Exercise 21.10 | Quicksort |

![](bbox=[0.1388, 0.4472, 0.1744, 0.4768])

# Checkpoint

+   1. **(Fill-in)** Iteration and recursion each have a termination test. Iteration terminates when the loop-continuation condition fails. Recursion terminates when __________.
+      **Answer:** a base case is recognized.
+   
+   2. **(True/False)** Each recursive call creates another copy of the function’s variables; this can consume considerable memory.
+      **Answer:** True.
+   
+   3. **(True/False)** Recursion is preferred over iteration in performance situations.
+      **Answer:** False. If possible, avoid using recursion in performance situations. Recursive calls take time and consume additional memory.

# 5.17 Scope Rules

The portion of a program where an identifier can be used is known as its *scope*. For example, when we declare a local variable in a block, it can be referenced only

+   - from the point of its declaration in that block to the end of that block and
+   - in nested blocks that appear within that block after the variable’s declaration.

This section discusses block scope and global namespace scope. Parameter names in function prototypes have *function parameter scope* and are known only in the prototype in which they appear. Later we’ll see other scopes, including *class scope* in Chapter 9 and *function scope* and *namespace scope* in Chapter 20.

# Block Scope

Identifiers declared in a block have *block scope*, which begins at the identifier’s declaration and ends at the block’s terminating right brace (}). Local variables have block scope, as do