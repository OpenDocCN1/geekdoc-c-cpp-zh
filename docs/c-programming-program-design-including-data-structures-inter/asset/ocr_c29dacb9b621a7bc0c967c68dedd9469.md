> Note: When the program is compiled, some of the newer IDEs might give warning messages if the program uses the value of a variable without first properly initializing that variable. In this case, if you ignore the warning and execute the program, the program might terminate abnormally with an error message.

> Note: Suppose you want to store a character into a `char` variable using an input statement. During program execution, when you enter the character, you do not include the single quotes. For example, suppose that `ch` is a `char` variable. Consider the following input statement:

```
cin >> ch;
```

If you want to store K into `ch` using this statement, during program execution, you only enter K. Similarly, if you want to store a string into a `string` variable using an input statement, during program execution, you enter only the string without the double quotes.

# EXAMPLE 2-19

This example further illustrates how assignment statements and input statements manipulate variables. Consider the following declarations:

```
int firstNum, secondNum;
double z;
char ch;
string name;
```

Also, suppose that the following statements execute in the order given:

+   1. `firstNum = 4;`
+   2. `secondNum = 2 * firstNum + 6;`
+   3. `z = (firstNum + 1) / 2.0;`
+   4. `ch = 'A';`
+   5. `cin >> secondNum;`
+   6. `cin >> z;`
+   7. `firstNum = 2 * secondNum + static_cast<int>(z);`
+   8. `cin >> name;`
+   9. `secondNum = secondNum + 1;`
+   10. `cin >> ch;`
+   11. `firstNum = firstNum + static_cast<int>(ch);`
+   12. `z = firstNum - z;`