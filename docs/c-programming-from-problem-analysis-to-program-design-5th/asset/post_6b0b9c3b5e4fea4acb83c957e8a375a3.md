
### EXAMPLE 4-16

```cpp
if (score >= 90)
    cout << "The grade is A." << endl;
else if (score >= 80)
    cout << "The grade is B." << endl;
else if (score >= 70)
    cout << "The grade is C." << endl;
else if (score >= 60)
    cout << "The grade is D." << endl;
else
    cout << "The grade is F." << endl;
```

### EXAMPLE 4-17

Assume that all variables are properly declared, and consider the following statements:

```cpp
if (temperature >= 50)                         //Line 1
    if (temperature >= 80)                     //Line 2
        cout << "Good day for swimming." << endl;  //Line 3
    else                                       //Line 4
        cout << "Good day for golfing." << endl;   //Line 5
else                                           //Line 6
    cout << "Good day to play tennis." << endl;    //Line 7
```

In this C++ code, the else in Line 4 is paired with the if in Line 2, and the else in Line 6 is paired with the if in Line 1. Note that the else in Line 4 cannot be paired with the if in Line 1. If you pair the else in Line 4 with the if in Line 1, the if in Line 2 becomes the action statement part of the if in Line 1, leaving the else in Line 6 dangling. Also, the statements in Lines 2 through 5 form the statement part of the if in Line 1. The indentation does not determine the pairing, but should be used to communicate the pairing.

### EXAMPLE 4-18

Assume that all variables are properly declared, and consider the following statements:

```cpp
if (temperature >= 70)                         //Line 1
    if (temperature >= 80)                     //Line 2
        cout << "Good day for swimming." << endl;  //Line 3
    else                                       //Line 4
        cout << "Good day for golfing." << endl;   //Line 5
```

```cpp
if (month == 4)
    cout << "April" << endl;
if (month == 5)
    cout << "May" << endl;
if (month == 6)
    cout << "June" << endl;
```

Program segment (a) is written as a sequence of **if...else** statements; program segment (b) is written as a series of **if** statements. Both program segments accomplish the same thing. If month is 3, then both program segments output March. If month is 1, then in program segment (a), the expression in the **if** statement in Line 1 evaluates to **true**. The statement (in Line 2) associated with this **if** then executes; the rest of the structure, which is the **else** of this **if** statement, is skipped; and the remaining **if** statements are not evaluated. In program segment (b), the computer has to evaluate the expression in each **if** statement because there is no **else** statement. As a consequence, program segment (b) executes more slowly than does program segment (a).

## Short-Circuit Evaluation

Logical expressions in C++ are evaluated using a highly efficient algorithm. This algorithm is illustrated with the help of the following statements:

```cpp
(x > y) || (x == 5)      //Line 1
(a == b) && (x >= 7)     //Line 2
```

In the statement in Line 1, the two operands of the operator **||** are the expressions (x > y) and (x == 5). This expression evaluates to **true** if either the operand (x > y) is **true** or the operand (x == 5) is **true**. With short-circuit evaluation, the computer evaluates the logical expression from left to right. As soon as the value of the entire logical expression is known, the evaluation stops. For example, in statement 1, if the operand (x > y) evaluates to **true**, then the entire expression evaluates to **true** because **true || true** is **true** and **true || false** is **true**. Therefore, the value of the operand (x == 5) has no bearing on the final outcome.

Similarly, in the statement in Line 2, the two operands of the operator **&&** are (a == b) and (x >= 7). If the operand (a == b) evaluates to **false**, then the entire expression evaluates to **false** because **false && true** is **false** and **false && false** is **false**.

**Short-circuit evaluation** (of a logical expression): A process in which the computer evaluates a logical expression from left to right and stops as soon as the value of the expression is known.

### EXAMPLE 4-20

Consider the following expressions:

```cpp
(age >= 21) || (x == 5)       //Line 1
(grade == 'A') && (x >= 7)     //Line 2
```

For the expression in Line 1, suppose that the value of age is 25. Because (25 >= 21) is true and the logical operator used in the expression is ||, the expression evaluates to true. Due to short-circuit evaluation, the computer does not evaluate the expression (x == 5). Similarly, for the expression in Line 2, suppose that the value of grade is 'B'. Because ('B' == 'A') is false and the logical operator used in the expression is &&, the expression evaluates to false. The computer does not evaluate (x >= 7).

## Comparing Floating-Point Numbers for Equality: A Precaution

Comparison of floating-point numbers for equality may not behave as you would expect. For example, consider the following program:

```cpp
#include <iostream>
#include <iomanip>
#include <cmath>

using namespace std;

int main()
{
    double x = 1.0;
    double y = 3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0;

    cout << fixed << showpoint << setprecision(17);

    cout << "3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0 = "
         << 3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0 << endl;

    cout << "x = " << x << endl;
    cout << "y = " << y << endl;

    if (x == y)
        cout << "x and y are the same." << endl;
    else
        cout << "x and y are not the same." << endl;

    if (fabs(x - y) < 0.000001)
        cout << "x and y are the same within the tolerance "
             << "0.000001." << endl;
    else
        cout << " x and y are not the same within the "
             << "tolerance 0.000001." << endl;

    return 0;
}
```

**Sample Run:**

```text
3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0 = 0.9999999999999989
x = 1.000000000000000000
y = 0.9999999999999989
x and y are not the same.
x and y are the same within the tolerance 0.000001.
```

In this program, x is initialized to 1.0 and y is initialized to 3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0. Now, due to rounding, as shown by the output, this expression evaluates to 0.9999999999999989. Therefore, the expression (x == y) evaluates to *false*. However, if you evaluate the expression 3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0 by hand using a paper and a pencil, you will get 3.0 / 7.0 + 2.0 / 7.0 + 2.0 / 7.0 = (3.0 + 2.0 + 2.0) / 7.0 = 7.0 / 7.0 = 1.0. That is, the value of y should be set to 1.0.

The preceding program and its output show that you should be careful when comparing floating-point numbers for equality. One way to check whether two floating-point numbers are equal is to check whether the absolute value of their difference is less than a certain tolerance. For example, suppose the tolerance is 0.000001. Then, x and y are equal if the absolute value of (x - y) is less than 0.000001. To find the absolute value, you can use the function fabs of the header file *cmath*, as shown in the program. Therefore, the expression fabs(x - y) < 0.000001 determines whether the absolute value of (x - y) is less than 0.000001.

### Associativity of Relational Operators: A Precaution

Sometimes logical expressions do not behave as you might expect, as shown by the following program, which determines if a number is between 0 and 10 (inclusive).

```cpp
#include <iostream>

using namespace std;

int main()
{
    int num;

    cout << "Enter an integer: ";
    cin >> num;
    cout << endl;

    if (0 <= num <= 10)
        cout << num << " is within 0 and 10." << endl;
    else
        cout << num << " is not within 0 and 10." << endl;

    return 0;
}
```

**Sample Runs:** In these sample runs, the user input is shaded.

**Sample Run 1:**

```text
Enter an integer: 5

5 is within 0 and 10.
```

**Sample Run 2:**

```text
Enter an integer: 20

20 is within 0 and 10.
```

**Sample Run 3:**

```text
Enter an integer: -10

-10 is within 0 and 10.
```

Clearly, Sample Run 1 is correct and Sample Runs 2 and 3 are incorrect. Because the `if` statement determines whether an integer is between 0 and 10, the problem is in the expression in the `if` statement. So, let us look at this expression, which is:

```cpp
0 <= num <= 10
```

Although this statement is a legal C++ expression, you do not get the desired result. Let us evaluate this expression for certain values of num. Suppose that the value of num is 5. Then:

|  |  |  |
| --- | --- | --- |
| 0 <= num <= 10 | = 0 <= 5 <= 10 |  |
|  | = (0 <= 5) <= 10 | (Because relational operators are evaluated from left to right) |
|  | = 1 <= 10 | (Because 0 <= 5 is true, 0 <= 5 evaluates to 1) |
|  | = 1 (true) |  |

Now, suppose that num = 20. Then:

|  |  |  |
| --- | --- | --- |
| 0 <= num <= 10 | = 0 <= 20 <= 10 |  |
|  | = (0 <= 20) <= 10 | (Because relational operators are evaluated from left to right) |
|  | = 1 <= 10 | (Because 0 <= 20 is true, 0 <= 20 evaluates to 1) |
|  | = 1 (true) |  |

Now, you can see why the expression evaluates to `true` when `num` is 20. Similarly, if `num` is -10, the expression `0 <= num <= 10` evaluates to `true`. In fact, this expression will always evaluate to `true`, no matter what `num` is. This is due to the fact that the expression `0 <= num` evaluates to either 0 or 1, and `0 <= 10` is `true` and `1 <= 10` is `true`. So what is
