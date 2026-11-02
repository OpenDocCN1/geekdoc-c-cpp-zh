
```
22
23 return 0;
24 }
```

## Program Run

Floor: 20
The elevator will travel to the actual floor 19

![](img/d61019b035dd82beb581604273c0ee6b_118_0.png)

## Common Error 3.1
### A Semicolon After the if Condition

The following code fragment has an unfortunate error:

```
if (floor > 13) ; // ERROR
{
    floor--;
}
```

There should be no semicolon after the if condition. The compiler interprets this statement as follows: If floor is greater than 13, execute the statement that is denoted by a single semicolon, that is, the do-nothing statement. The statement enclosed in braces is no longer a part of the if statement. It is always executed. Even if the value of floor is not above 13, it is decremented. Placing a semicolon after the else reserved word is also wrong:

```
if (floor > 13)
{
    actual_floor = floor - 1;
}
else ;
{
    actual_floor = floor;
}
```

In this case, the do-nothing statement is executed if floor > 13 is not fulfilled. This is the end of the if statement. The next statement, enclosed in braces, is executed in both cases; that is, actual_floor is always set to floor.

![](img/d61019b035dd82beb581604273c0ee6b_118_1.png)

## Programming Tip 3.1
### Brace Layout

Programmers vary in how they align braces in their code. In this book, we follow the simple rule of making { and } line up.

```
if (floor > 13)
{
    floor--;
}
```

This style makes it easy to spot matching braces.

Some programmers put the opening brace on the same line as the if:

```
if (floor > 13) {
    floor--;
}
```

This style makes it harder to match the braces, but it saves a line of code, allowing you to view more code on the screen without scrolling. There are passionate advocates of both styles.

![](img/d61019b035dd82beb581604273c0ee6b_118_2.png)

© Timothy Large/iStockphoto.
Properly lining up your code makes your programs easier to read.

![](img/d61019b035dd82beb581604273c0ee6b_120_0.png)

## Programming Tip 3.4
### Avoid Duplication in Branches

Look to see whether you duplicate code in each branch. If so, move it out of the if statement. Here is an example of such duplication:

```
if (floor > 13)
{
    actual_floor = floor - 1;
    cout << "Actual floor: " << actual_floor << endl;
}
else
{
    actual_floor = floor;
    cout << "Actual floor: " << actual_floor << endl;
}
```

The output statement is exactly the same in both branches. This is not an error—the program will run correctly. However, you can simplify the program by moving the duplicated statement, like this:

```
if (floor > 13)
{
    actual_floor = floor - 1;
}
else
{
    actual_floor = floor;
}
cout << "Actual floor: " << actual_floor << endl;
```

Removing duplication is particularly important when programs are maintained for a long time. When there are two sets of statements with the same effect, it can easily happen that a programmer modifies one set but not the other.

![](img/d61019b035dd82beb581604273c0ee6b_120_1.png)

## Special Topic 3.1
### The Conditional Operator

C++ has a conditional operator of the form

```
condition ? value1 : value2
```

The value of that expression is either value1 if the test passes or value2 if it fails. For example, we can compute the actual floor number as

```
actual_floor = floor > 13 ? floor - 1 : floor;
```

which is equivalent to

```
if (floor > 13)
{
    actual_floor = floor - 1;
}
else
{
    actual_floor = floor;
}
```

You can use the conditional operator anywhere that a value is expected, for example:

```
cout << "Actual floor: " << (floor > 13 ? floor - 1 : floor);
```

We don't use the conditional operator in this book, but it is a convenient construct that you will find in many C++ programs.

## 3.2 Comparing Numbers and Strings

Relational operators (< <= > >= == !=) are used to compare numbers and strings.

Every if statement contains a condition. In many cases, the condition involves comparing two values. For example, in the previous examples we tested floor > 13. The comparison > is called a relational operator. C++ has six relational operators (see Table 1).

![](img/d61019b035dd82beb581604273c0ee6b_121_0.png)

© arturbo iStockphoto.

*In C++, you use a relational operator to check whether one value is greater than another.*

As you can see, only two C++ relational operators (< and >) look as you would expect from the mathematical notation. Computer keyboards do not have keys for ≥, ≤, or ≠, but the >=, <=, and != operators are easy to remember because they look similar. The == operator is initially confusing to most newcomers to C++. In C++, = already has a meaning, namely assignment. The == operator denotes equality testing:

```
floor = 13; // Assign 13 to floor
if (floor == 13) // Test whether floor equals 13
```

You must remember to use == inside tests and to use = outside tests. (See Common Error 3.2 for more information.)

Table 1 Relational Operators

| C++ | Math Notation | Description |
|---|---|---|
| > | > | Greater than |
| >= | ≥ | Greater than or equal |
| < | < | Less than |
| <= | ≤ | Less than or equal |
| == | = | Equal |
| != | ≠ | Not equal |

You can compare strings as well:

```
if (input == "quit") . . .
```

Use != to check whether two strings are different. In C++, letter case matters. For example, 'Quit' and 'quit' are not the same string.

## Syntax 3.2 Comparisons

![](img/d61019b035dd82beb581604273c0ee6b_122_0.png)

EXAMPLE CODE See sec02 of your companion code for a program that compares numbers and strings.

Table 2 summarizes how to use relational operators in C++.

| Expression | Value | Comment |
|---|---|---|
| 3 <= 4 | true | 3 is less than 4; <= tests for "less than or equal". |
| 3 =< 4 | Error | The "less than or equal" operator is <=, not =<. The "less than" symbol comes first. |
| 3 > 4 | false | > is the opposite of <=. |
| 4 < 4 | false | The left-hand side must be strictly smaller than the right-hand side. |
| 4 <= 4 | true | Both sides are equal; <= tests for "less than or equal". |
| 3 == 5 - 2 | true | == tests for equality. |
| 3 != 5 - 1 | true | != tests for inequality. It is true that 3 is not 5 - 1. |
| 3 = 6 / 2 | Error | Use == to test for equality. |
| 1.0 / 3.0 == 0.333333333 | false | Although the values are very close to one another, they are not exactly equal. See Common Error 3.3. |
| "10" > 5 | Error | You cannot compare a string to a number. |

![](img/d61019b035dd82beb581604273c0ee6b_123_0.png)

## Common Error 3.2
### Confusing = and ==

The rule for the correct usage of = and == is very simple: In tests, always use == and never use =. If it is so simple, why can't the compiler be helpful and flag any errors? Actually, the C++ language allows the use of = inside tests. To understand this, we have to go back in time. The creators of C, the predecessor to C++, were very frugal. They did not want to have special values true and false. Instead, they allowed any numeric value inside a condition, with the convention that 0 denotes false and any non-0 value denotes true. Furthermore, in C and C++ assignments have values. For example, the value of the assignment expression floor = 13 is 13.

These two features—namely that numbers can be used as truth values and that assignments are expressions with values—conspire to make a horrible pitfall. The test

```
if (floor = 13) // ERROR
```

is legal C++, but it does not test whether floor and 13 are equal. Instead, the code sets floor to 13, and because that value is not zero, the condition of the if statement is always fulfilled.

Fortunately, most compilers issue a warning when they encounter such a statement. You should take such warnings seriously. (See Programming Tip 3.5 for more advice about compiler warnings.)

Some shell-shocked programmers are so nervous about using = that they use == even when they want to make an assignment:

```
floor == floor - 1; // ERROR
```

This statement tests whether floor equals floor - 1. It doesn't do anything with the outcome of the test, but that is not an error. Some compilers will warn that “the code has no effect”, but others will quietly accept the code.

![](img/d61019b035dd82beb581604273c0ee6b_123_1.png)

## Common Error 3.3
### Exact Comparison of Floating-Point Numbers

Floating-point numbers have only a limited precision, and calculations can introduce roundoff errors. You must take these inevitable roundoffs into account when comparing floating-point numbers. For example, the following code multiplies the square root of 2 by itself. Ideally, we expect to get the answer 2:

![](img/d61019b035dd82beb581604273c0ee6b_123_2.png)

© caracterdesign/iStockphoto.

Take limited precision into account when comparing floating-point numbers.

```
double r = sqrt(2.0);
if (r * r == 2)
{
    cout << "sqrt(2) squared is 2" << endl;
}
else
{
    cout << "sqrt(2) squared is not 2 but " << setprecision(18) << r * r << endl;
}
```

This program displays
sqrt(2) squared is not 2 but 2.0000000000000044

It does not make sense in most circumstances to compare floating-point numbers exactly. Instead, we should test whether they are close enough. That is, the magnitude of their
