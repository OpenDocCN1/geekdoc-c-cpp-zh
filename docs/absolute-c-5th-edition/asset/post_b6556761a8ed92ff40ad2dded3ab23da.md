
## Branching Mechanisms

### switch Statement

SYNTAX

```
switch (Controlling_Expression)
{
    case Constant_1:
        Statement_Sequence_1
        break;
    case Constant_2:
        Statement_Sequence_2
        break;
        ...
    case Constant_n:
        Statement_Sequence_n
        break;
    default:
        Default_Statement_Sequence
}
```

> You do not place a break statement in each case. If you omit a break, that case continues until a break (or the end of the switch statement) is reached.

## EXAMPLE

```
int vehicleClass;
double toll;
cout << "Enter vehicle class: ";
cin >> vehicleClass;

switch (vehicleClass)
{
    case 1:
        cout << "Passenger car.";
        toll = 0.50;
        break;
    case 2:
        cout << "Bus.";
        toll = 1.50;
        break;
    case 3:
        cout << "Truck.";
        toll = 2.00;
        break;
    default:
        cout << "Unknown vehicle class!";
}
```

> If you forget this break, then passenger cars will pay $ 1.50.

## CHAPTER 2 Flow of Control

The switch statement ends when either a break statement is encountered or the end of the switch statement is reached. A break statement consists of the keyword break followed by a semicolon. When the computer executes the statements after a case label, it continues until it reaches a break statement. When the computer encounters a break statement, the switch statement executes. If you omit the break statement, after executing the code for the next case, the computer will go on to execute the code for the next case.

Note that you can have two case labels for the same section of code, as in the following portion of a switch statement:

```
case 'A':
case 'a':
    cout << "Excellent. "
    cout << "You need not take the final.\n"
    break;
```

Since the first case has no break statement (in fact, no statement at all), the effect is as having two labels for one case, and C++ syntax requires every case for each label, such as 'A' and 'a'.

If no case has a constant that matches the value of the controlling expression, then the statements following the default label are executed. You do not have a default section. If no match is found for the value of the controlling expression, nothing happens when the switch statement executes. However, it is safest to always have a default section. If you think your case labels list all possible outcomes, then you can put an error message in the default section.

## Self-Test Exercises

11. What output will be produced by the following code?

```
int x = 2;
cout << "Start\n";
if (x <= 3)
    if (x != 0)
        cout << "Hello from the second if.\n";
    else
        cout << "Hello from the else.\n";
cout << "Start again\n";
if (x > 3)
    if (x != 0)
        cout << "Hello from the second if.\n";
    else
        cout << "Hello from the else.\n";
cout << "End again\n";
```

## Self-Test Exercises (continued)

12. What output will be produced by the following code?

```
int extra = 2;
if (extra < 0)
    cout << "small";
else if (extra == 0)
    cout << "medium";
else
    cout << "large";
```

13. What would be the output in Self-Test Exercise 12 if the assignment was changed to the following?

```
int extra = -37;
```

14. What would be the output in Self-Test Exercise 12 if the assignment was changed to the following?

```
int extra = 0;
```

15. Write a multway if-else statement that classifies the value of an int variable into one of the following categories and writes out an appropriate message.

```
n < 0 or 0 ≤ n ≤ 100 or n > 100
```

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_94_0.png)

## PITFALL: Forgetting a break in a switch Compiler

If you forget a break in a switch statement, the compiler will not issue an error message. You will have written a syntactically correct switch statement, but it will not do what you intended it to do. Notice the annotation in the example in the box entitled "switch Statement."

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_94_1.png)

## TIP: Use switch statements for Menus

The multiday if-else statement is more versatile than the switch statement, and you can use a multway if-else statement anywhere you can use a switch statement. However, the switch statement is clearer. The switch statement is perfect for implementing menus. Each branch of the switch statement can be one menu choice.

## Flow of Control

### Enumeration Types

enumeration type

An enumeration type is a type whose values are defined by a list of constants of int. An enumeration type is very much like a list of declared constants. Enumeration types can be handy for defining a list of identifiers to use the case labels in a switch statement.

When enumerating an enumeration type, you can use any int values and define any number of constants. For example, the following enumeration type defines a constant for the length of each month:

```
enum JAN_LENGTH = 31, FEB_LENGTH = 28,
MAR_LENGTH = 31, APR_LENGTH = 30, MAY_LENGTH = 31,
JUN_LENGTH = 30, JUL_LENGTH = 31, AUG_LENGTH = 31,
SEP_LENGTH = 30, OCT_LENGTH = 31, NOV_LENGTH = 30,
DEC_LENGTH = 31;
```

As this shows, two or more named constants in an enumeration type can receive the same int value.

If do not specify any numeric values, the identifiers in an enumeration type definition are assigned consecutive values beginning with 0. For example, the type-definition

```
enum Direction { NORTH = 0, SOUTH = 1, EAST = 2, WEST = 3 };
```

is equivalent to

```
enum Direction { NORTH, SOUTH, EAST, WEST };
```

The form that does not explicitly list the int values is normally used when you want a list of names and do not care about what values they are.

Suppose you MyEnum { ONE = 17, TWO, THREE, FOUR = -3, FIVE };

then ONE takes the value 17; TWO takes the next int value, THREE takes the next value, 19; FOUR takes -3; and FIVE takes the next value, -2. In the short, for the first enumeration constant is 0. The increase by 1 unless you set one or more of the enumeration constants.

Although the constants in an enumeration type are as int values and can be used as integers in many contexts, remember that an enumeration type is a separate type and treat it as a different from the type int. Use enumeration types as labels and avoid doing arithmetic with variables of an enumeration type.

## The Conditional Operator

conditional operator

It is possible to embed a conditional inside an expression by using a ternary operator known as the conditional (also called the ternary or arithmetic if). Its is reminiscent of an older programming style, and we do not advise using it. It is included here for the sake of completeness (and in case you disagree with).

The conditional operator is a notational variant on certain forms of the if-else statement. This variant is illustrated as follows. Consider the statement

```
if (n1 > n2)
    max = n1;
else
    max = n2;
```

This can be expressed using the conditional operator as follows:

max = (n1 > n2) ? n1 : n2;

The expression on the right-hand side of the assignment statement is the conditional operator expression:

(n1 > n2) ? n1

The ? : form a ternary operator known as the conditional operator. A conditional operator expression starts with a Boolean expression by a ? and then followed by two expressions separated with a colon: If the Boolean expression is true, then the first of the two expressions is returned; otherwise, the second of the two expressions is returned.

## Self-Test Exercises

16. Given the following declaration and output statement, assume that this has been embedded in a correct program and run. What is the output?

```
enum Direction { N, S, E, W, W };
// ...
cout << W << " " << E << " " << S << " " << N << endl;
```

17. Given the following declaration and output statement, assume that this has been embedded in a correct program and run. What is the output?

```
enum Direction { N = 5, S = 7, E = 1, W };
// ...
cout << W << " " << E << " " << S << " " << N << endl;
```

## 2.3 Loops

Tasks are more like the torture of Sisyphus than housework: repetition: the clean becomes soiled, the soiled is made clean, over and over, day after day.

> SIMONE DE BEAUVOIR
