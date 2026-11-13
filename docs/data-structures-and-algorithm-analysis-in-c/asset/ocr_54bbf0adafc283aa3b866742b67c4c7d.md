![](bbox=[0.073, 0.093, 0.426, 0.363])

Figure 9.88 Grid for Exercise 9.45

+   a. Write a program that computes enough information to output a path in the maze. Give output in the form SEN... (representing go south, then east, then north, etc.).
+   b. If you are using a C++ compiler with a windowing package, write a program that draws the maze and, at the press of a button, draws the path.

9.47 Suppose that walls in the maze can be knocked down, with a penalty of P squares. P is specified as a parameter to the algorithm. (If the penalty is 0, then the problem is trivial.) Describe an algorithm to solve this version of the problem. What is the running time for your algorithm?

+   9.48 Suppose that the maze may or may not have a solution.
+   a. Describe a linear-time algorithm that determines the minimum number of walls that need to be knocked down to create a solution. (Hint: Use a double-ended queue.)
+   b. Describe an algorithm (not necessarily linear-time) that finds a shortest path after knocking down the minimum number of walls. Note that the solution to part (a) would give no information about which walls would be the best to knock down. (Hint: Use Exercise 9.47.)

9.49 Write a program to compute word ladders where single-character substitutions have a cost of 1, and single-character additions or deletions have a cost of p > 0, specified by the user. As mentioned at the end of Section 9.3.6, this is essentially a weighted shortest-path problem.

Explain how each of the following problems (Exercises 9.50-9.53) can be solved by applying a shortest-path algorithm. Then design a mechanism for representing an input, and write a program that solves the problem.

9.50 The input is a list of league game scores (and there are no ties). If all teams have at least one win and a loss, we can generally “prove,” by a silly transitivity argument,