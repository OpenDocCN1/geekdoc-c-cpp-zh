# FIGURE 6-13 Railroad switching system for Exercise 4

![](bbox=[0.25, 0.13, 0.58, 0.28])

b. The nature of the stack-based algorithm makes it simple to display the string in reverse order, but somewhat harder to display it in its correct order. Write a pseudocode algorithm that displays the string in its correct forward order.

c. Implement the read-and-correct algorithm as a C++ function, but make the stack local to the function instead of an argument. Let the function construct a string that contains the corrected input characters in forward order, and return it.

+   7. Revise the solution to the balanced-braces problem so that the expression can contain three types of delimiters: ( ), [ ], and { }. Thus, {ab(c[d]e)} is valid, but {ab(c)} is not.

+   8. For each of the following strings, trace the execution of the language-recognition algorithm described in Section 6.2.2, and show the contents of the stack at each step.
+   a. xySyy
+   b. ySyx
+   c. xySy
+   d. xySx
+   e. xxSxx

+   9. Write a pseudocode function that uses a stack to determine whether a string is in the language L, where
+   a. L = {s : s contains equal numbers of As and Bs}
+   b. L = {s : s is of the form A^n B^n for some n >= 0}

+   10. Write a function that uses a stack to determine whether a string is in the language L, where
+   L = {ss' : s is a string of characters, s' = reverse(s)}
+   Note: The following strings are not in the language: The empty string, a string with fewer than two characters, and a string with an odd number of characters.

+   11. Evaluate the following postfix expressions by using the algorithm given in this chapter. Show the status of the stack after each step of the algorithm. Assume the following values for the identifiers: a = 7, b = 3, c = 12, d = -5, e = 1.
+   a. a b c + -
+   b. a b c - d * +
+   c. a b + c - e * +

+   12. Convert the following infix expressions to postfix form by using the algorithm given in this chapter. Show the status of the stack after each step of the algorithm.
+   a. a - b + c
+   b. a - (b / c * d)
+   c. a / (b * c)
+   d. a / (b - c / (d + e)) * f
+   e. (a + b) * c
+   f. a * (b / c / d) + e
+   g. a - (b + c)
+   h. a - (b + c * d) / e