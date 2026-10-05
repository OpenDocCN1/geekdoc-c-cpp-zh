
## 5.5. THE IF/ELSE STATEMENT

Listing 5.4 (feedback.cpp) avoids the division by zero run-time error that causes the program to terminate prematurely, but it still alerts the user that there is a problem. Another application may handle the situation in a different way; for example, it may substitute some default value for divisor instead of zero.

The general form of an if/else statement is

![](img/e326304bd50fbc4f7d5a64c1487eb635_90_0.png)

- * The reserved word begins the if/else statement.
- The condition is a Boolean expression that determines whether the running program will execute statement 1 or statement 2. As with the if statement, the condition must appear within parentheses.
- The program executes statement 1 if the condition is true. To make the if/else statement more readable, indent statement 1 more spaces than the if line. This part of the if statement is sometimes called the body of the if.
- The reserved else begins the second part of the if/else statement.
- The program executes statement 2 if the condition is false. To make the if/else statement readable, indent statement 2 more spaces than the else line. This part of the if/else statement is sometimes called the body of the else.

The body of the else clause of an if/else statement may be a compound statement:

```
if (x == y)
  cout << x;
else {
  x = 0;
  cout << y;
}
```

or the if body alone may be a compound statement:

```
if (x == y)
  cout << x;
  x = 0;
else
  cout << y;
```

©2014 Richard L. Halterman Draft date: January 26, 2014

or both parts may be compound:

```
if (x == y) {
    cout << x;
    x = 0;
}
else {
    cout << y;
    y = 0;
}
```

or, as in Listing 5.4 (betterfeedback.cpp), both the if and the else body can be simple statements.

> Remember, if you wish to associate more than one statement with the body of the if or else, you must use a compound statement. Compound statements are enclosed within curly braces {}.

If you attempt to use an if/else statement and discover that you need to leave the else clause empty, as

```
if (x == 2)
    cout << "x = " << x << endl;
else
    // Nothing to do otherwise
```

or, using a slightly different syntax, as

```
if (x == 2)
    cout << "x = " << x << endl;
else {
    // Nothing to do otherwise
}
```

you should instead use a simple if statement:

```
if (x == 2)
    cout << "x = " << x << endl;
```

The empty clauses shown above do work, but they complicate the code and make it more difficult for humans to read.

Due to the imprecise representation of floating-point numbers (see Listing 4.3 (imprecise.cpp) in Section 4.1), programmers must avoid using the equality operator (==) by itself to compare floating-point numbers. Listing 5.5 (samifferent.cpp) uses an if/else statement to demonstrate the perils of using the equality operator with floating-point quantities.

Listing 5.5: samifferent.cpp
#include <iostream>
#include <iomanip>

using namespace std;

## 5.6. COMPOUND BOOLEAN EXPRESSIONS

```
int main() {
    double d1 = 1.11 - 1.10;
    double d2 = 2.11 - 2.10;
    cout << "d1 = " << d1 << endl;
    cout << "d2 = " << d2 << endl;
    if (d1 == d2)
        cout << "Same" << endl;
    else
        cout << "Different" << endl;
    cout << "d1 = " << setprecision(20) << d1 << endl;
    cout << "d2 = " << setprecision(20) << d2 << endl;
}
```

In List 5.5 (samifferent.cpp) the displayed values of d1 and d2 are rounded so they appear equal, but internally the exact representations are significantly different. By including the header iomanip we can use the setprecision stream manipulator to force cout to display more decimal places in the floating-point number. From the output of Listing 5.5 (samifferent.cpp) that the quantities which should be 0.01 are actually slightly different.

![](img/e326304bd50fbc4f7d5a64c1487eb635_92_0.png)

This might not result from using floating-point numbers where they truly are needed. In Section 9.4.6 we will show how to handle floating-point comparisons properly.

## 5.6 Compound Boolean Expressions

Simple Boolean expressions, each involving one relational operator, can be combined into more complex Boolean expressions using the logical operators && (and), || (or), and ! (not). A combination of two or more Boolean expressions using logical operators is called a compound Boolean expression.

To introduce Boolean expressions, consider a computer science degree that requires, among other computing courses, Operating Systems and Programming Languages. If we isolate those courses, we can say a student must successfully complete both Operating Systems and Programming Languages to qualify for the degree. A student that passes Operating Systems not Programming Languages will not have the necessary requirements. A student without Operating Systems is insufficient, and a student completing Operating Systems not Programming Languages surely not qualify.

Logical AND works in the same way. If e1 and e2 are Boolean expressions, e1 && e2 is true only if e1 and e2 are both true; if either one is false or both are false, the compound expression is false.

To illustrate logical OR, consider two mathematics, Differential Equations and Linear Algebra. A student who successfully completes Differential Equations but does not take Linear Algebra meets the requirement. A similar student may take Linear Algebra but not Differential Equations. It is important to note that the student may elect to

| e1 | e2 | e1 && e2 | e1 || e2 | e1 != e2 |
| --- | --- | --- | --- | --- |
| false | false | false | false | true |
| false | true | false | true | false |
| true | false | false | true | false |

Table 5.3: Logical operators—$e_1$ and $e_2$ are Boolean expressions

both Differential Equations and Linear Algebra (perhaps on a way to a mathematics minor), but the requirement is not less fulfilled.

Logical OR works in a similar fashion. Given our expressions $e_1$ and $e_2$, the compound expression $e_1 || e_2$ is false only if $e_1$ and $e_2$ are both false; if either one is true or both are true, the compound expression is true. Note that logical OR is an inclusive or, not an exclusive or. In informal conversation we often use or as an inclusive or, like "Would you like cake or ice cream for dessert?" The implication is one or the other, not both. In computer programming the or is inclusive; if both subexpressions are true, the expression is true.

Logical NOT simply reverses the truth value of the expression to which it is applied. If $e$ is a true Boolean expression, $!e$ is false; if $e$ is false, $!e$ is true.
