6. Write a recursive algorithm to find x^n.

7. What is tail recursion? Explain with a suitable example.

8. Write an algorithm to solve the Tower of Hanoi problem. Also, calculate the time complexity of your algorithm.

9. Write the recursive function for the Tower of Hanoi problem. Also, draw the recursion tree for any set of initial values.

10. Let, a and b denotes positive integers. Suppose a function Q is defined as follows:
Q (a, b) = 0 if a<b
= Q (a-b, b) + 1 if b<=a
Find the value of Q (2, 3) and Q (14, 3).

11. Choose the correct alternatives for the following:
i) The Ackermann function, for all non-negative values of m and n, is recursively defined as
A (m, n) = { n + 1, if m = 0
           { A (m-1, 1), if m!= 0 but n = 0
           { A (m-1, A(m, n-1)), if m!=0 and n!=0
Therefore, the value of A (1, 2) is
a) 4 b) 3 c) 5 d) 2
ii) Which of the following statement is not true?
a) Each time a procedure calls itself, it must be nearer in some sense to solution
b) Recursion functions are always fast and use less memory
c) When last executed statement at a function in a recursive call then it is known as tail recursion
d) Recursion uses the top down and backtracking approach for solving a problem.