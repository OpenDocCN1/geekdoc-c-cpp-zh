in which the exclamation point denotes the factorial function. Moreover, $C(n, 0) = C(n, n) = 1$. It is also known that $C(n, r) = C(n-1, r-1) + C(n-1, r)$.

a. Write a recursive algorithm to determine $C(n, r)$. Identify the base case(s) and the general case(s).

b. Using your recursive algorithm, determine $C(5, 3)$ and $C(9, 4)$.

# PROGRAMMING EXERCISES

+   1. Write a recursive function that takes as a parameter a nonnegative integer and generates the following pattern of stars. If the nonnegative integer is 4, then the pattern generated is:
+   
+   ```text
+   ****
+   ***
+   **
+   *
+   *
+   **
+   ***
+   ****
+   ```
+   
+   Also, write a program that prompts the user to enter the number of lines in the pattern and uses the recursive function to generate the pattern. For example, specifying 4 as the number of lines generates the above pattern.

+   2. Write a recursive function to generate the following pattern of stars:
+   
+   ```text
+      *
+     * *
+    * * *
+   * * * *
+    * * *
+     * *
+      *
+   ```
+   
+   Also, write a program that prompts the user to enter the number of lines in the pattern and uses the recursive function to generate the pattern. For example, specifying 4 as the number of lines generates the above pattern.

+   3. Write a recursive function, that returns the number of vowels in a string. Also, write a program to test your function.

+   4. Write a recursive function named `sumSquares` that returns the sum of the squares of the numbers from 0 to num, in which num is a nonnegative int variable. Do not use global variables; use the appropriate parameters. Also write a program to test your function.

+   5. Write a recursive function that finds and returns the sum of the elements of an int array. Also, write a program to test both your function.

+   6. A palindrome is a string that reads the same both forward and backward. For example, the string "madam" is a palindrome. Write a program that uses