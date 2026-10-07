# LESSON 4 The Pieces of a C Program: Statements, Expressions, and Operators

# Output

Enter the year you were born: 1994
You were not born in a leap year!
You can vote this year!
It is illegal for you to drink alcohol!

# Analysis

The ageChecker.c program shows four statements in action (lines 15 through 27). Hopefully, with each new program in the book, key elements are becoming more familiar to you. Line 3 creates a CURRENTYEAR constant with use the #define directive, and line 4 includes the stdio.h file that is needed whenever you use the printf and scanf functions. Line 6 defines two integer variables that will be used by the if statements.

The first two if statements used to determine if the user was born in a leap year. This is the place where the modulus operator (%) proves useful. Leap year is divisible by 4, so testing whether the entered has a remainder equal to 0 (again, remember to use instead of == equality) means the year is a leap year. The second if statement uses the not equal (!= operator for all other years. This setup is far more efficient than testing whether the remainder is equal to 1, 2, or 3. Not equal is a great choice when you need to exclude one case.

The second pair of if statements test the user's current age against voting and drinking eligibility. The first, on line 24, greater than or equal to and tells eligible voters they should be good and do their civic duty. The second statement, on line 26, reminds users under the age of 21 that they cannot drink (legally).

Although most birth years entered can satisfy only one of those requirements, as the sample output demonstrates, there is a small section that has both.

> The statements within an if clause are indented. This is a common practice to aid readability.

# The else Clause

An if statement can optionally include an else clause. The else clause is included as follows:

```
if (expression)
    statement1;
else
    statement2;
```