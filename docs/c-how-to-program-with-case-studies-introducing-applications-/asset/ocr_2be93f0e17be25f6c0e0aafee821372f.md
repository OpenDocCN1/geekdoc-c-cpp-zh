that makes the loop-continuation condition fail; recursion keeps producing simpler versions of the original problem until the base case is reached.

+   - Both iteration and recursion can occur infinitely: An infinite loop occurs with iteration if the loop-continuation test never becomes false; infinite recursion occurs if the recursion step does not reduce the problem each time in a manner that converges on the base case. Infinite iteration and recursion typically occur as a result of errors in a program's logic.

# Negatives of Recursion

Recursion has many negatives. It repeatedly invokes the mechanism, and consequently the overhead, of function calls. This can be expensive in both processor time and memory space. Each recursive call causes another copy of the function (actually only the function's variables) to be created; this can consume considerable memory. Iteration normally occurs within a function, so the overhead of repeated function calls and extra memory assignment is omitted. So why choose recursion?

# Recursion Is Not Required

Any problem that can be solved recursively can also be solved iteratively (nonrecursively). A recursive approach is chosen in preference to an iterative approach when the recursive approach more naturally mirrors the problem and results in a program that's easier to understand and debug. Another reason to choose a recursive solution is that an iterative solution may not be apparent.

# Recursion Examples and Exercises Throughout This Book

Most programming textbooks introduce recursion much later than we've done here. We feel that recursion is such a sufficiently rich and complex topic that it's better to introduce it earlier and spread the examples over the remainder of the text. The following table summarizes by chapter the recursion examples and exercises in the text.

| Recursion examples and exercises |  |  |
|---|---|---|
| Chapter 5 | Print an array backward | Chapter 12 |
| Factorial function | Print a string backward | Search a linked list |
| Fibonacci function | Check whether a string is a palindrome | Print a linked list backward |
| Greatest common divisor | Minimum value in an array | Binary tree insert |
| Multiply two integers | Linear search | Preorder traversal of a binary tree |
| Raising an integer to an integer power | Binary search | Inorder traversal of a binary tree |
| Towers of Hanoi | Eight Queens | Postorder traversal of a binary tree |
| Recursive main | Chapter 7 | Printing trees |
| Visualizing recursion | Maze traversal | Chapter 13 |
| Chapter 6 | Chapter 8 | Selection sort |
| Sum of the elements of an array | Printing a string input at the keyboard backward | Quicksort |
| Print an array |  |  |