```
1\tinitialize total to zero
2\tinitialize counter to zero
3
4\tprompt the user to enter the first grade
5\tinput the first grade (possibly the sentinel)
6
7\twhile the user has not yet entered the sentinel
8\t\tadd this grade into the running total
9\t\tadd one to the grade counter
10\t\tprompt the user to enter the next grade
11\t\tinput the next grade (possibly the sentinel)
12
13\tif the counter is not equal to zero
14\t\tset the average to the total divided by the counter
15\t\tprint the average
16\telse
17\t\tprint “No grades were entered”
```

We use blank lines to make the pseudocode more readable and indentation to emphasize the actions that should be placed in the control statements’ bodies. The blank lines separate the algorithms into their phases and set off control statements; the indentation emphasizes the bodies of the control statements.

Our pseudocode algorithm solves the more general class-average problem. This algorithm required only two refinements—sometimes, more are needed. You terminate the top-down, stepwise refinement process when you feel your pseudocode algorithm has sufficient detail for you to convert the algorithm to C++.

Some programmers do not use program development tools like pseudocode. They feel that their ultimate goal is to solve the problem on a computer and that writing pseudocode merely delays the final product. This may work for simple and familiar problems but can lead to significant errors and delays in large, complex projects.

# 3.9.3 Implementing Sentinel-Controlled Iteration

Figure 3.2 implements sentinel-controlled iteration. Although each grade entered by the user is an integer, the average calculation will likely produce a floating-point number, which an int cannot represent. C++ provides types `float`, `double` and `long double` to store floating-point numbers:

+   - A double variable typically stores numbers with larger magnitude and finer detail than a float—that is, more digits to the right of the decimal point, also known as the number’s **precision**.
+   - Similarly, a long double variable typically stores values with larger magnitude and more precision than double.

To calculate a floating-point average in this example, we’ll store the total as a `double`—C++’s default type for floating-point literals, such as `-7.2`, `0.0` or `98.6`.