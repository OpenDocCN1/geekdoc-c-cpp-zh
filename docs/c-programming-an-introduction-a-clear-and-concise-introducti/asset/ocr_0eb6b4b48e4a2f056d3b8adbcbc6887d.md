```
```cpp
int numGrade;

string letterGrade;

cout << "Enter the numerical score: ";

cin >> numGrade;

if (numGrade >= 90)
    letterGrade = "A";

if (numGrade >= 80)
    letterGrade = "B";

if (numGrade >= 70)
    letterGrade = "C";

if (numGrade >= 60)
    letterGrade = "D";

if (numGrade < 60)
    letterGrade = "F";
```
```

This program solves the problem but results in unnecessary computation. If the user enters the number 86, the program will assign the value "B" to letterGrade, but will then continue down testing numGrade in each of the remaining if statements. What we would prefer to happen is that once the program assigns the letter grade to the variable the program should not perform any more tests on numGrade and move on to its next task.

The solution to this problem is to use another variation of the if statement – the if-else if statement. The general form of the if-else if statement looks like this:

```
```cpp
if (condition)
    statement;
else if (condition)
```
```