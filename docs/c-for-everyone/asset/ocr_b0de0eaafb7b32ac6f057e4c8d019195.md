# Implement decisions whose branches require further decisions.

![](bbox=[0.078, 0.116, 0.163, 0.191])

+   - When a decision statement is contained inside the branch of another decision statement, the statements are nested.
+   - Nested decisions are required for problems that have two levels of decision making.

# Draw flowcharts for visualizing the control flow of a program.

+   - Flow charts are made up of elements for tasks, input/outputs, and decisions.
+   - Each branch of a decision can contain tasks and further decisions.
+   - Never point an arrow inside another branch.

![](bbox=[0.729, 0.229, 0.889, 0.307])

# Design test cases for your programs.

+   - Each branch of your program should be covered by a test case.
+   - It is a good idea to design test cases before implementing a program.

# Use the Boolean data type to store and combine conditions that can be true or false.

![](bbox=[0.078, 0.441, 0.184, 0.554])

+   - The Boolean type has two values, false and true.
+   - C++ has two Boolean operators that combine conditions: && (and) and || (or).
+   - To invert a condition, use the ! (not) operator.
+   - The && and || operators are computed using *short-circuit evaluation*: As soon as the truth value is determined, no further conditions are evaluated.
+   - De Morgan’s law tells you how to negate && and || conditions.

# Apply if statements to detect whether user input is valid.

+   - When reading a value, check that it is within the required range.
+   - Use the fail function to test whether the input stream has failed.

![](bbox=[0.778, 0.6, 0.891, 0.682])

# REVIEW EXERCISES

+   **R3.1** Find the errors in the following if statements.

```
a. if (x > 0) then cout << x;
b. if (x > 0) { y = 1; } else { y = -1; }
c. if (1 + x > pow(x, sqrt(2)) { y = y + x; }
d. if (x == 1) { y++; }
e. cin >> x; if (cin.fail()) { y = y + x; }
```

+   **R3.2** What do these code fragments print?

```
a. int n = 1; int m = -1;
   if (n < m) { cout << n; } else { cout << m; }

b. int n = 1; int m = -1;
   if (-n >= m) { cout << n; } else { cout << m; }
```