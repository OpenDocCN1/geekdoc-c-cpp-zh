# 7.6. EXERCISES

+   - The for loop is a top-checking loop that, when used properly, concentrates all the information about its control in one convenient location.

+   - The three parts of the for loop control are initialization, condition, and modification.

+   - The for statement is used for a loop that can be controlled by a single variable with a definite starting value, a definite ending value, and a regular way to update the variable's value.

+   - A for loop is ideal for counting.

+   - Any or all of the three parts in the for loop header can be omitted; however, if you feel the need to one or more of the parts, the while statement may be a better choice.

+   - Best practices avoid modifying the control variable of a for statement within the loop's body; the modification should be limited to the third part of the for header.

+   - The <iomanip> library provides the setw object that provides special formatting for output sent to cout.

# 7.6 Exercises

+   1. Consider the following code fragment.

```
int x;
cin >> x;
switch (x + 3) {
case 5:
cout << x << endl;
break;
case 10:
cout << x - 3 << endl;
break;
case 20:
cout << x + 3 << endl;
break;
}
```

+   (a) What is printed when the user enters 2?
(b) What is printed when the user enters 5?
(c) What is printed when the user enters 7?
(d) What is printed when the user enters 17?
(e) What is printed when the user enters 20?
(f) What is printed when the user enters 5?

+   2. Consider the following code fragment.

```
char ch;
cin >> (ch) {
case 'a':
```