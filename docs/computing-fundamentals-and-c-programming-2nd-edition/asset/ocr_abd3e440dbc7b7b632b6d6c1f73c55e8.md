+   13. Write a program to compute the value of Euler's number e, that is used as the base of natural logarithms. Use the following formula
+       e = 1 + 1/1! + 1/2! + 1/3! + . . . . + 1/n!
+       Use a suitable loop construct. The loop must terminate when the difference between two successive values of e is less than 0.00001.

+   14. Write programs to evaluate the following functions to 0.0001% accuracy.
+       (a) sinx = x - x^3/3! + x^5/5! - x^7/7! + . . . . .
+       (b) cosx = 1 - x^2/2! + x^4/4! - x^6/6! + . . . .
+       (c) SUM = 1 + (1/2)^2 + (1/3)^3 + (1/4)^4 + . . . .

+   15. The present value (popularly known as book value) of an item is given by the relationship.
+       P = c (1-d)^n
+       where c = original cost
+             d = rate of depreciation (per year)
+             n = number of years
+             p = present value after y years.
+       If P is considered the scrap value at the end of useful life of the item, write a program to compute the useful life in years given the original cost, depreciation rate, and the scrap value.
+       The program should request the user to input the data interactively.

+   16. Write a program to print a square of size 5 by using the character S as shown below:
+       ```
+       (a) S S S S S        (b) S S S S S
+           S S S S S            S         S
+           S S S S S            S         S
+           S S S S S            S         S
+           S S S S S            S S S S S
+       ```

+   17. Write a program to graph the function
+       y = sin (x)
+       in the interval 0 to 180 degrees in steps of 15 degrees. Use the concepts discussed in the Case Study 4 in Chapter 8.

+   18. Write a program to print all integers that are **not divisible** by either 2 or 3 and lie between 1 and 100. Program should also count the number of such integers and print the result.

+   19. Modify the program of Exercise 8.16 to print the character O instead of S at the centre of the square as shown below.
+       ```
+       S S S S S
+       S S S S S
+       S S O S S
+       S S S S S
+       S S S S S
+       ```

+   20. Given a set of 10 two-digit integers containing both positive and negative values, write a program using **for** loop to compute the sum of all positive values and the sum of the number of values added. The program should use **scanf** to read the values and terminate when the sum exceeds 999. Do not use **goto** statement.