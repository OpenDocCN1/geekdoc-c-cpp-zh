This pseudocode may be written in C++ as:

```
```cpp
if (studentGrade >= 90) {
    cout << "A";
}
else {
    if (studentGrade >= 80) {
        cout << "B";
    }
    else {
        if (studentGrade >= 70) {
            cout << "C";
        }
        else {
            if (studentGrade >= 60) {
                cout << "D";
            }
            else {
                cout << "F";
            }
        }
    }
}
```
```

If variable `studentGrade` is greater than or equal to 90, the first four conditions in the nested if…else statement will be true, but only the statement in the if part of the first if…else statement will execute. After that statement executes, the else part of the “outermost” if…else statement is skipped. In a nested if…else statement, ensure that you test for all possible cases.

The preceding nested if…else statement also can be written in the following form, which is identical but uses fewer braces, less spacing and indentation:

```
```cpp
if (studentGrade >= 90) {
    cout << "A";
}
else if (studentGrade >= 80) {
    cout << "B";
}
else if (studentGrade >= 70) {
    cout << "C";
}
else if (studentGrade >= 60) {
    cout << "D";
}
else {
    cout << "F";
}
```
```

This form avoids deep indentation of the code to the right, which sometimes can force lines to wrap. Throughout the text, we enclose control-statement bodies in braces ({ and }), which avoids a logic error called the “dangling-else” problem. We investigate this problem in Exercises 3.13–3.15.