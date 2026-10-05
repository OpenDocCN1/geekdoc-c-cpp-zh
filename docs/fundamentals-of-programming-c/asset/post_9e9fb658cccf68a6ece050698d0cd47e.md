
## 6.6 SUMMARY

x = (y + 2);

the compiler simply ignores them, so there is no efficiency penalty in the compiled code.

We can shorten the loop even further:

```
while (is_prime && trial_factor < value)
is_prime = (value % trial_factor++ != 0);
```

This version uses the post-increment value of the test expression (see Section 4.8). Recall that the post-increment value of the variable is in the surrounding expression (if any), and then the variable is incremented. Since the while's body contains only one statement, the curly braces are not needed.

## 6.6 Summary

- The while statement allows the execution of code sections to be repeated times.
- The condition of the while controls the execution of statements within the while's body.
- The statements within the body of a while are executed over and over until the condition of the while is false.
- If the while's condition is initially false, the body is not executed at all.
- In an infinite loop, the while's condition never becomes false.
- The statements within while's body must eventually lead to the condition being false; otherwise, the loop will be infinite.
- Do not confuse while statements with if statements; their structure is very similar (while reserved instead of the if word intentionally), but they behave differently.
- Infinite loops are be designed by putting a printing statement inside its body.
- An assignment expression has a value; the expression's value is the same as the expression on the right side of the assignment operator. This fact can be used to streamline the control of a loop that repeats on user input.
- A loop contained within another loop is called a nested loop.
- Iteration is a powerful mechanism and can be used to solve many interesting problems.
- A block is any section of source code enclosed within curly braces. A compound statement is one example of a block.
- A variable declared within a block is local to that block.
- Complex iteration using nested loops mixed with conditional statements can be difficult to do correctly.
- Sometimes simple optimizations can speed up considerably the execution of loops.

## 6.7. EXERCISES

- The break statement immediately exits a loop, skipping the rest of the loop's body, without checking to see if the condition is true or false. Execution continues with the statement immediately following the body of the loop.
- In a nested loop, the break statement exits only the loop in which the break is found.
- The goto statement directs the program's execution to a labeled statement within the function. The goto statement is legitimately used only to exit completely from a nested loop.
- The continue statement immediately checks the loop's condition, skipping the rest of the loop's body. If the condition is true, the execution continues at the top of the loop as usual; otherwise, the loop is terminated and continues with the statement immediately following the loop's body.
- In a nested loop, the continue statement affects only the loop in which the continue is found.

## 6.7 Exercises

1. In Listing 6.4 (addnonnegatives.cpp) could the condition of the if statement have used > instead of >= and achieved the same results? Why?

2. In 6.4 (addnonnegatives.cpp) could the condition of the while statement have used > instead of >= and achieved the same results? Why?

3. Use a loop to write the following code fragment so that it uses cout and one endl.

```
cout << 2 << endl;
cout << 4 << endl;
cout << 6 << endl;
cout << 8 << endl;
cout << 10 << endl;
cout << 12 << endl;
cout << 14 << endl;
cout << 16 << endl;
```

4. In 6.4 (addnonnegatives.cpp) what would happen if the statement cin is moved out of the loop? Is moving the assignment out of the loop a good or bad to do? Why?

5. How many asterisks direct the following code fragment?

6. How many asterisks direct the following code print?

```
int a = 0;
while (a < 100) {
    cout << "*";
}
cout << endl;
```

## 6.7. EXERCISES

7. How many asterisks does the following code fragment print?

```
int a = 0;
while (a < 100) {
    cout << "*";
    a++;
}
cout << endl;
```

8. How many asterisks does the following code fragment print?

```
int a = 0;
while (a < 100) {
    int b = 0;
    while (b < 55) {
        cout << "*";
        b++;
    }
}
cout << endl;
```

9. How many asterisks does the following code fragment print?

```
int a = 0;
while (a < 100) {
    if (a % 5 == 0) {
        cout << "*";
    }
    a++;
}
cout << endl;
```

10. How many asterisks does the following code fragment print?

```
int a = 0;
while (a < 100) {
    int b = 0;
    while ((a + b) % 2 == 0) {
        cout << "*";
        b++;
    }
}
```

11. How many asterisks does the following code fragment print?

```
int a = 0;
while (a < 100) {
    int b = 0;
    while (b < 100) {
        cout << "*";
        b++;
    }
}
}
```

12. What is printed by the following code?

```
int a = 0;
while (a < 100) {
    cout << a++;
}
```

13. What is printed by the following code?

```
int a = 0;
while (a < 100) {
    cout << a++;
}
```

14. Rewrite the following code using a break statement and eliminating the done variable.

```
bool done = false;
int n = 0, m = 100;
while (n != m) {
    cin >> n;
    if (n < 0)
        done = true;
}
```

15. Rewrite the following code so it does not use a break statement.

```
int x = 0;
while (x > 0) {
    cin >> y;
    if (y)
}
```

## 6.7. EXERCISES

17. Suppose you were given some code from a language that did not support structured statements like while. Your task is to modernize and adapt it to C++. The following code fragment has been adapted to C++, but you must now structure it with while to still behave identically to this code.

```
int i = 0;
if (i >= 10)
    cout << i << endl;
    ++;
```

18. Simplify. What is printed by the following code?

```
int a = 0;
while (a < 100)
    cout << ++a;
```

20. Write a C++ program that accepts a single integer value entered by the user. If the value entered is less than one, the program prints nothing. If the user enters a positive integer, n, the program prints an x n box drawn with * characters. If the user enters 1, for example, the program prints

![](img/e326304bd50fbc4f7d5a64c1487eb635_155_0.png)

If the user enters a 2, it prints

![](img/e326304bd50fbc4f7d5a64c1487eb635_155_1.png)

An entry of three yields

![](img/e326304bd50fbc4f7d5a64c1487eb635_155_2.png)

and so forth. If the user enters 7, it prints

![](img/e326304bd50fbc4f7d5a64c1487eb635_155_3.png)

that is, a $7 \times 7$ box of • symbols.

21. Write a C++ program that allows the user to enter exactly twenty (20) double-precision floating-point values. The program then prints the sum, average (arithmetic mean), maximum, and minimum of the values entered.

22. Write a C++ program that allows the user to enter any number of non-negative double-precision floating-point values. The user terminates the input list with any negative value. The program then prints the sum, average (arithmetic mean), maximum, and minimum of the values entered. The terminating negative value is not used in the computations.

23. Redesign List 6.20 (startree.cpp) so that it draws a sideways tree pointing right; for example, if the user enters 7, the program would print

![](img/e326304bd50fbc4f7d5a64c1487eb635_156_0.png)

24. Redesign List 6.20 (startree.cpp) so that it draws a sideways tree pointing left; for example, if the user enters 7, the program would print

![](img/e326304bd50fbc4f7d5a64c1487eb635_156_1.png)
