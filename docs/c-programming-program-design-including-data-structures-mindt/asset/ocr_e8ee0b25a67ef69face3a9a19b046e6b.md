**Sample Run:** In this sample run, the user input is shaded.

`Enter number in decimal: 78`

`Decimal 78 = 1001110 binary`

# QUICK REVIEW

+   1. The process of solving a problem by reducing it to smaller versions of itself is called recursion.
+   2. A recursive definition defines a problem in terms of smaller versions of itself.
+   3. Every recursive definition has one or more base cases.
+   4. A recursive algorithm solves a problem by reducing it to smaller versions of itself.
+   5. Every recursive algorithm has one or more base cases.
+   6. The solution to the problem in a base case is obtained directly.
+   7. A function is called recursive if it calls itself.
+   8. Recursive algorithms are implemented using recursive functions.
+   9. Every recursive function must have one or more base cases.
+   10. The general solution breaks the problem into smaller versions of itself.
+   11. The general case must eventually be reduced to a base case.
+   12. The base case stops the recursion.
+   13. While tracing a recursive function:
+       - Logically, you can think of a recursive function as having an unlimited number of copies of itself.
+       - Every call to a recursive function—that is, every recursive call—has its own code and its own set of parameters and local variables.
+       - After completing a particular recursive call, control goes back to the calling environment, which is the previous call. The current (recursive) call must execute completely before control goes back to the previous call. The execution in the previous call begins from the point immediately following the recursive call.
+   14. A function is called directly recursive if it calls itself.
+   15. A function that calls another function and eventually results in the original function call is said to be indirectly recursive.
+   16. A recursive function in which the last statement executed is the recursive call is called a tail recursive function.
+   17. To design a recursive function, you must do the following:
+       a. Understand the problem requirements.