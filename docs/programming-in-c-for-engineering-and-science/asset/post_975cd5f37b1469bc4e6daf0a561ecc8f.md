
In CHAPTER 5, we saw that the logical flow of execution in a function or program is governed by three basic control mechanisms: sequence, selection, and repetition. We looked at examples where an if statement was used to perform selective execution and for and while statements to perform repetitive execution. Our introductions to these statements were quite brief, however, so we will take a closer look at them in this chapter and the next. We will begin by looking at the if statement in more detail and then introduce the switch statement that sometimes provides a more efficient way to perform selection. In Chapter 9, we will reexamine the for statement and see some of the other ways it can be used to control repetition. We will also introduce the do-while statement, and we will compare it with the while statement we studied in Chapter 5.

## 8.1 INTRODUCTORY EXAMPLE: AIR QUALITY INDEXES REVISITED

The Air Quality Index (AQI) in the introductory example in Chapter 5 involved only two categories: safe and hazardous. In reality, however, there are usually several more. For example, the United States AQI has six categories and a color for each:

| AQI | Level of Health Concern | Color |
| 0 to 50 | Good | Green |
| 51 to 100 | Moderate | Yellow |
| 101 to 150 | Unhealthy for sensitive groups | Orange |
| 151 to 200 | Unhealthy | Red |
| 201 to 300 | Very unhealthy | Purple |
| 301 and above | Hazardous | Maroon |

The program in Example 8.1 is a modification of that in Example 5.1 that classifies the index using these six categories. It uses the if-else if construct that we introduced in Chapter 5 and will consider in more detail in the next section.

### Example 8.1 Air Quality Indexes

```
/* This program reads three pollution levels, calculates an air
quality index (AQI) as their integer average, and then displays
an appropriate air-quality message.

Input:  the three pollution levels
Constant: the cutoff values (parts per million)
Output:  the air quality index, the corresponding level of health
         concern using the six U.S. categories, and its color
---------------------------------------------------------------*/

#include <iostream>           // cin, cout, <<, >>
using namespace std;
```

## 8.2 MORE ABOUT THE if STATEMENT

In Section 5.4 we saw three different forms of the if statement:

The **single-branch** or **simple if** form:

```
if (condition)
    statement
```

The **dual-branch** or **if-else** form:

```
if (condition)
    statement₁
else
    statement₂
```

The **multibranch** or **if-else-if** form:

```
if (condition₁)
    statement₁
else if (condition₂)
    statement₂
...
else if (conditionₙ)
    statementₙ
else
    statementₙ₊₁
```

where each *condition* is a boolean expression.

Although these may look like three distinct statements, the first and last are actually special forms of the second if statement. The first form is a simpler way of writing an if statement in which the else part is empty:

```
if (condition)
    statement₁
else;
```

The multibranch form is simply a series of **nested** if statements written as one. To illustrate this, if we were to write a 5-branch if-else-if and we were to start each new if statement on a new line with each else aligned with its corresponding if, our code would appear as follows:

```
if (condition₁)
    statement₁
else
    if (condition₂)
        statement₂
    else
```

```
if (condition₁)
    statement₁
else
    if (condition₄)
        statement₁
    else
        statement₅
```

However, the free-form nature of C++ allows us to begin each nested if on the same line as the preceding else and align the else-if combinations:

```
if (condition₁)
    statement₁
else if (condition₂)
    statement₂
else if (condition₃)
    statement₃
else if (condition₄)
    statement₄
else
    statement₅
```

This latter style reflects more clearly the multibranch nature and is therefore more readable. It is important, however, to understand that each else is really a continuation of the nearest preceding if:

```
if (condition₁)
    statement₁
else if (condition₂)
    statement₂
else if (condition₃)
    statement₃
else if (condition₄)
    statement₄
else
    statement₅
```

### 8.2.1 Pitfall: The Dangling-Else Problem

Each statementᵢ in an if statement can be any C++ statement and, in particular, may be another if statement; for example,

```
if (x > 0)
    if (y > 0)
        z = sqrt(x) + sqrt(y);
```

When such nested if statements are followed by an else, it is not evident with which if the else corresponds. Does the else match the outer if?

Or does it match the inner if?

```
if (x > 0)
    if (y > 0)
        z = sqrt(x) + sqrt(y);
else
    cerr << "\n*** Unable to compute z!" << endl;
```

```
if (x > 0)
    if (y > 0)
        z = sqrt(x) + sqrt(y);
else
    cerr << "\n*** Unable to compute z!" << endl;
```

This ambiguity is known as the dangling else problem, and C++ resolves it by stipulating that

> In a nested if statement, an else is matched with the nearest preceding unmatched if.

Thus, for the preceding if statement, the second matching is used; that is, the else is associated with the inner if (whose condition is y > 0). Consequently, the output statement is executed only in the case that x is positive and y is nonpositive. If we wish to associate this else with the outer if, we can force the association by enclosing the inner if in curly braces as follows:

```
if (x > 0)
{
    if (y > 0)
        z = sqrt(x) + sqrt(y);
}
else
    cerr << "*** Unable to compute z!" << endl;
```

Putting the inner if inside a block makes it a complete statement, so that the else must associate with the outer if. Thus, the output statement is executed whenever x is nonpositive.

### 8.2.2 Pitfall: Confusing = and ==

We turn now to what is one of the most common errors made by beginning C++ programmers in constructing boolean expressions, and, as a consequence, in writing if statements. We begin by looking at two features of C++ that are relevant to this problem.

+   1. True and false in C++. To maintain compatibility with its parent language C, in any boolean context, C++ interprets the value 0 as equivalent to the boolean value false and any nonzero value as equivalent to the boolean value true. Thus, the statement

```
if (0)
    cout << "T\n";
```

> C has no bool type. In its place, C uses the zero/nonzero mechanism described here.

```
else
    cout << "F\n";
```

will always display F because the condition controlling the selection is zero, which C++ treats as false. Similarly, the statement

```
if (!23)
    cout << "T\n";
else
    cout << "F\n";
```

will always display the value T because the condition controlling the selection is non-zero, which is interpreted as true in C++.

2. Assignments are expressions. We saw in Chapter 3 that in C++, assignment (=) is an operator that, in addition to assigning a value to a variable, returns the value being assigned as its result. For example, the assignment expression

```
x = 23
```

does two things: It assigns x the value 23 and it produces the value 23 as its result. Similarly,

```
x = 0
```

both assigns x the value 0 and produces the value 0 as its result.

By themselves, neither of these C++ features is particularly troublesome, but when coupled with the similarity of the assignment and equality operators, they make it easy to write if statements that contain logical errors. To illustrate, suppose that a programmer encodes the instruction

If x is equal to zero, then
    Display the character string "Zero"
Otherwise
    Display the character string "Nonzero"

as

```
if (x = 0)
    cout << "Zero\n";
else
    cout << "Nonzero\n";
```

Because the assignment operator

```
x = 0
```

is used instead of an equality comparison

```
x == 0
```

and the value returned by the assignment operator is the value that was assigned, this statement is equivalent to

```
if (0)
    cout << "Zero\n";
else
    cout << "Nonzero\n";
```

Because 0 is treated as false, the statement to output Nonzero will *always* be selected, regardless of the value of x.

Similarly, if a programmer writes

```
cout << MENU;             // display menu of choices: A, B, C
cin >> choice;
if (choice = 'A')
    statement₁;            // do something when choice is A
else if (choice = 'B')
    statement₂;            // do something else when choice is B
else if (choice = 'C')
    statement₃;            // do something else when choice is C
else
    cout << choice << " must be A, B, or C.\n";
```

then the statement associated with choice A will *always* be selected, regardless of the value entered by the user. The reason is that instead of the first condition testing whether choice is equal to A,

```
choice == 'A'
```

it assigns choice the numeric code of A (65 in ASCII):

```
choice = 'A'
```

The result produced by the assignment operator is the value assigned (65), and so this if-else-if form is equivalent to

```
cout << MENU;             // display menu of choices: A, B, C
cin >> choice;
if (65)
    statement₁;            // do something when choice is A
else if (choice = 'B')
    statement₂;            // do something else when choice is B
else if (choice = 'C')
```
