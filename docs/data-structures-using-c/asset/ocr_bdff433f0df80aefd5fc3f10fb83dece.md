should be combined to get the final solution. If the sub-problem is still large, the technique is reapplied. The reapplication is expressed better by the recursive function. Recursion is a technique that allows us to break down a problem into one or more sub-problems that are similar in form to the original problem. Examples include binary search, merge sort, and quick sort.

# 4.6.1 Writing Recursive Code

The general approach to writing a recursive function is listed in the following sequence:

+   1. Write the function header so you are sure what the function will do and how it will be called. Identify some unit of measure for the size of the problem function or procedure will work on. Then, pretend that the task is to write a function that will work on problems of all sizes.
+   
+   2. Decompose the problem into sub-problems. Identify clearly the non-recursive case of the problem. Make it as small as possible. The function will nearly always begin by testing for this non-recursive case, also known as the *base case* or the *end condition*.
+   
+   3. Write recursive calls to solve those sub-problems whose form is similar to that of the original problem.
+   
+   4. Write the code to combine, enhance, or modify the results of the recursive call(s), if necessary, to construct the desired return value or create the desired side effects.
+   
+   5. Write the end condition(s) to handle any situations that are not handled properly by the recursive portion of the program.

# 4.6.2 Tower of Hanoi: An Example of Recursion

The use of recursion often makes everything simpler. First, find out the recurring data and the essential feature of the problem that should change as the function calls itself. In the Tower of Hanoi solution, one recurs on the largest disk to be moved. That is, one has to write a recursive function that takes the largest disk as a parameter in the tower to be moved. The function should take three parameters indicating from which peg the tower should be moved (source), to which peg it should go (dest), and the last peg (spare), which is used temporarily. Let us consider the initial position of the problem as in Fig. 4.2.

![](bbox=[0.2, 0.74, 0.89, 0.9])