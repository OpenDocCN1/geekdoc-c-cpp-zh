
## Program 4.5

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    double monthlySales, income;

    cout << "Enter the value of monthly sales: ";
    cin >> monthlySales;
    if (monthlySales >= 50000.00)
        income = 375.00 + .16 * monthlySales;
    else if (monthlySales >= 40000.00)
        income = 350.00 + .14 * monthlySales;
    else if (monthlySales >= 30000.00)
        income = 325.00 + .12 * monthlySales;
    else if (monthlySales >= 20000.00)
        income = 300.00 + .09 * monthlySales;
    else if (monthlySales >= 10000.00)
        income = 250.00 + .05 * monthlySales;
    else
        income = 200.00 + .03 * monthlySales;

    cout << setiosflags(ios::showpoint)
         << setiosflags(ios::fixed)
         << setprecision(2)
         << "The income is $" << income << endl;

    return 0;
}
```

A sample run of Program 4.5 follows:

```
Enter the value of monthly sales: 36243.89
The income is $4674.27
```

## EXERCISES 4.3

- 1. (Practice) An acute angle is less than 90 degrees, an obtuse angle is greater than 90 degrees, and a right angle is equal to 90 degrees. Using this information, write a C++ program that accepts an angle, in degrees, and displays the type of angle corresponding to the degrees entered.

Using this information, write, compile, and run a C++ program that accepts a Reynolds number as user input and displays a message indicating whether the flow is laminar, turbulent, or transitional.

### 6. (Program) The tolerance of critical components in a system is determined according to the following schedule:

| Specification Status | Tolerance |
|---|---|
| Space exploration | Less than 0.1% |
| Military grade | Greater than or equal to 0.1% and less than 1% |
| Commercial grade | Greater than or equal to 1% and less than 10% |
| Toy grade | Greater than or equal to 10% |

Using this information, write, compile, and run a C++ program that accepts a component's tolerance reading and determines the specification that should be assigned to it.

### 7. (Program) a. Write, compile, and run a program that accepts two real numbers and a select code from a user. If the entered select code is 1, have the program add the two previously entered numbers and display the result; if the select code is 2, the numbers should be multiplied; and if the select code is 3, the first number should be divided by the second number.

b. Determine what the program written in Exercise 7a does when the entered numbers are 3 and 0 and the select code is 3.

c. Modify the program written in Exercise 7a so that division by 0 isn't allowed, and a message is displayed when this division is attempted.

### 8. (Program) The quadrant in which a line starting from the origin is located is determined by the angle the line makes with the positive x axis, as follows:

| Angle from the Positive x Axis | Quadrant |
|---|---|
| Between 0 and 90 degrees | I |
| Between 90 and 180 degrees | II |
| Between 180 and 270 degrees | III |
| Between 270 and 360 degrees | IV |

a. Using this information, write, compile, and run a C++ program that accepts the angle of the line as user input and determines and displays the correct quadrant for the input data. (Note: If the angle is exactly 0, 90, 180, or 270 degrees, the corresponding line doesn't reside in any quadrant but lies on an axis.)

b. Modify the program written for Exercise 8a to display a message that identifies an angle of 0 degrees as the positive x axis, an angle of 90 degrees as the positive y axis, an angle of 180 degrees as the negative x axis, and an angle of 270 degrees as the negative y axis.

### 9. (Program) Write, compile, and run a C++ program that accepts a number followed by one space and then a letter. If the letter following the number is f, the program is to treat the number entered as a temperature in degrees Fahrenheit, convert the number to the equivalent degrees Celsius, and display a suitable message. If the letter following the number is c, the program is to treat the number entered as a temperature in degrees Celsius, convert the number to the equivalent degrees Fahrenheit, and display a suitable message. If the letter is neither f nor c, the program is to display a message that the data entered is incorrect and then terminate. Use an if-else chain in your program and make use of these conversion formulas: Celsius = (5.0 / 9.0) × (Fahrenheit - 32.0) Fahrenheit = (9.0 / 5.0) × Celsius + 32.0

### 10. (Program) Many states base yearly car registration fees on an automobile's model year and weight, using a schedule similar to the following:

| Model Year | Weight | Weight Class | Registration Fee |
|---|---|---|---|
| 1990 or earlier | Less than 2700 lbs | 1 | 26.50 |
|  | 2700 to 3800 lbs | 2 | 35.50 |
|  | More than 3800 lbs | 3 | 56.50 |
| 1991 to 1999 | Less than 2700 lbs | 4 | 35.00 |
|  | 2700 to 3800 lbs | 5 | 45.50 |
|  | More than 3800 lbs | 6 | 62.50 |
| 2000 or later | Less than 3500 lbs | 7 | 49.50 |
|  | 3500 or more lbs | 8 | 62.50 |

Using this information, write, compile, and run a C++ program that accepts an automobile's year and weight and determines and displays its weight class and registration fee.

### 11. (Debug) Using the commission schedule from Program 4.5, the following program calculates monthly income:

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    double monthlySales, income;

    cout << "Enter the value of monthly sales: ";
    cin >> monthlySales;
    if (monthlySales >= 50000.00)
        income = 375.00 + .16 * monthlySales;
    if (monthlySales >= 40000.00 && monthlySales < 50000.00)
        income = 350.00 + .14 * monthlySales;
    if (monthlySales >= 30000.00 && monthlySales < 40000.00)
        income = 325.00 + .12 * monthlySales;
```

```
if (monthlySales >= 20000.00 && monthlySales < 30000.00)
    income = 300.00 + .09 * monthlySales;
if (monthlySales >= 10000.00 && monthlySales < 20000.00)
    income = 250.00 + .05 * monthlySales;
if (monthlySales < 10000.00)
    income = 200.00 + .03 * monthlySales;
```

```
cout << setiosflags(ios::showpoint)
    << setiosflags(ios::fixed)
    << setprecision(2)
    << "\n\nThe income is $" << income << endl;
```

```
return 0;
}
```

- a. Will this program produce the same output as Program 4.5?
- b. Which program is better? Why?

### 12. (Debug) The following program was written to produce the same result as Program 4.5:

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    double monthlySales, income;

    cout << "Enter the value of monthly sales: ";
    cin >> monthlySales;
```

```
if (monthlySales < 10000.00)
    income = 200.00 + .03 * monthlySales;
else if (monthlySales >= 10000.00)
    income = 250.00 + .05 * monthlySales;
else if (monthlySales >= 20000.00)
    income = 300.00 + .09 * monthlySales;
else if (monthlySales >= 30000.00)
    income = 325.00 + .12 * monthlySales;
else if (monthlySales >= 40000.00)
    income = 350.00 + .14 * monthlySales;
else if (monthlySales >= 50000.00)
    income = 375.00 + .16 * monthlySales;
```

```
cout << setiosflags(ios::showpoint)
    << setiosflags(ios::fixed)
    << setprecision(2)
    << "The income is $" << income << endl;

return 0;
}
```

- a. What does this program do?
- b. For what values of monthly sales does this program calculate the correct income?

## 4.4 The switch Statement

An if-else chain is used in programming applications in which one set of instructions must be selected from many possible alternatives. A switch statement is an alternative to the if-else chain for cases that involve comparing an integer expression with a specific value. It has this general form:

```
switch (integer_expression)
{   // start of compound statement
    case value_1:  // terminated with a colon
        statement1;
        statement2;
        .
        .
        break;
    case value_2:  // terminated with a colon
        statementm;
        statementn;
        .
        .
        break;
    .
    .
    case value_n:  // terminated with a colon
        statementw;
        statementx;
        .
        .
        break;
    default:  // terminated with a colon
        statementaa;
        statementbb;
        .
        .
}   // end of switch and compound statement
```
