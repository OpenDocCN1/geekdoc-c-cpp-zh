# 6.7. EXERCISES

+   - The break statement immediately exits a loop, skipping the rest of the loop's body, without checking to see if the condition is true or false. Execution continues with the statement immediately following the body of the loop.

+   - In a nested loop, the break statement exits only the loop in which the break is found.

+   - The goto statement directs the program's execution to a labeled statement within the function. The goto statement is legitimately used only to exit completely from a nested loop.

+   - The continue statement immediately checks the loop's condition, skipping the rest of the loop's body. If the condition is true, the execution continues at the top of the loop as usual; otherwise, the loop is terminated and continues with the statement immediately following the loop's body.

+   - In a nested loop, the continue statement affects only the loop in which the continue is found.

# 6.7 Exercises

+   1. In Listing 6.4 (addnonnegatives.cpp) could the condition of the if statement have used > instead of >= and achieved the same results? Why?

+   2. In 6.4 (addnonnegatives.cpp) could the condition of the while statement have used > instead of >= and achieved the same results? Why?

+   3. Use a loop to write the following code fragment so that it uses cout and one endl.

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

+   4. In 6.4 (addnonnegatives.cpp) what would happen if the statement cin is moved out of the loop? Is moving the assignment out of the loop a good or bad to do? Why?

+   5. How many asterisks direct the following code fragment?

+   6. How many asterisks direct the following code print?

```
int a = 0;
while (a < 100) {
    cout << "*";
}
cout << endl;
```