# 130 Chapter 3 Introduction to C# App Programming

The if statement executes. If the condition is false, the body is skipped—it does not execute. We'll see an example shortly.

Conditions in if statements can be formed by using the equality operators (= and !=), relational operators (<, >, >=) summarized in Fig. 3.21. The two equality operators (= and !=) have the same level of precedence, relational operators (>, <, >=) and the equality operators have lower precedence than the relational operators. They all associate from left to right.

# Common Programming Error 3.5

Confusing the equality operator, =, with the assignment operator, =, can cause a logic error or a syntax error. The equality operator should be read as "is equal to," and the assignment operator should be read as "gets" or "gets the value of." To avoid confusion, some programmers read the equality operator as "double equals" or "equals."

| Standard algebraic equality and relational operators | C# equality or relational operator | Sample C# condition | Meaning of C# condition |
|---|---|---|--|
| Relational operators | | | |
| > | | x > y | is greater than |
| < | | x < y | is less than |
| >= | | x >= y | is greater than equal to |
| <= | | x <= y | is less than equal to |
| Equality operators | | | |
| = | | x == y | is equal to |
| != | | x != y | is not equal to |

> Fig. 3.21 | Relational and equality operators.

Using the if Statement
3.22 uses if if statements to compare two integers entered by the user. If the condition in any of these if statements is true, the statement associated with that statement executes. The app uses Console to prompt and read two lines of text from the user, extracts the integers from text with int's Parse method, and stores them in variables number1 and number2. Then the app compares and displays the results of the comparisons that are true.

```
// Fig 3.22: Comparison.cs
// Comparing integers using if statements, equality operators
// and relational operators.
using System;
```

> Fig. 3.22 | Comparing integers using if statements, equality operators and relational operators. (Part 1 of 3).