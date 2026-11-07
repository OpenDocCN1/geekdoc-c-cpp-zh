Function `scanf` can input multiple values, as in

```
scanf("%d%d", &number1, &number2); // read two integers
```

If the input into both variables is successful, scanf will return 2. If the user enters a string for the first value, scanf will return 0, and neither number1 nor number2 will receive a value. If the user enters an integer followed by a string, scanf will return 1, and only number1 will receive a value.

![](bbox=[0.061, 0.209, 0.135, 0.232])

To make your input processing more robust, check scanf’s return value to ensure that the number of inputs read matches the number of inputs expected. Otherwise, your program will use the values of the variables as if scanf had completed successfully. This could lead to logic errors, program crashes or even attacks.

# Range Checking

Even if a scanf operates successfully, the values read might still be invalid. For example, grades are typically integers in the range 0–100. In a program that inputs grades, you should validate each grade to ensure that it’s in the range 0–100 by using range checking. You can then ask the user to reenter any value that’s out of range. If a program requires inputs from a specific set of values (such as non-sequential product codes), you can ensure that each input matches a value in the set.

![](bbox=[0.096, 0.469, 0.129, 0.495])

# Self Check

**(Fill-In)** If an input failure occurs, scanf returns the value ______; otherwise, it returns the number of items that were read.

**Answer:** EOF.

**2. (Multiple Choice)** Given the following code:

```
scanf("%d%d", &grade1, &grade2); // read two integers
```

which of the following statements a), b) or c) is **false**?

+   a) If the input is successful, scanf will return 0, indicating that integer values for both variables were input.
+   
+   b) If the user enters a string for the first value, scanf will return 0, and neither grade1 nor grade2 will receive a value.
+   
+   c) If the user enters an integer followed by a string, scanf will return 1, and only grade1 will receive a value.
+   
+   d) All of the above statements are true.

**Answer:** a) is **false**. Actually, if both values are input correctly, scanf will return 2.

# Summary

# Section 4.2 Iteration Essentials

+   - Most programs involve iteration (or looping). A loop is a group of instructions that computer repeatedly executes while some loop-continuation condition (p. 134) remains **true**.

2. For more information, see Chapter 5, “Integer Security,” of Robert Seacord’s book *Secure Coding in C and C++, 2/e*.