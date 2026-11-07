# 3.6.2 Blocks

The if statement expects only one statement in its body. To include several statements in an if’s or else’s body, enclose the statements in braces. It’s good practice always to use braces. Statements in a pair of braces (such as a control statement’s or function’s body) form a block. A block can be placed anywhere in a function where a single statement can be placed.

The following example includes a block of multiple statements in an if...else statement’s else part:

```
```cpp
if (studentGrade >= 60) {
    cout << "Passed";
}
else {
    cout << "Failed\n";
    cout << "You must retake this course.";
}
```
```

If studentGrade is less than 60, the program executes both statements in the body of the else and prints

```
```text
Failed
You must retake this course.
```
```

Without the braces surrounding the two statements in the else clause, the statement

```
```cpp
cout << "You must retake this course.";
```
```

would be outside the body of the else part of the if...else statement and would execute regardless of whether the studentGrade was less than 60—a logic error.

# Syntax and Logic Errors

The compiler catches syntax errors, such as when one brace in a block is left out of the program. A logic error, such as an incorrect calculation, has its effect at execution time. A fatal logic error causes a program to fail and terminate prematurely. A nonfatal logic error allows a program to continue executing but causes it to produce incorrect results.

# Empty Statement

Just as a block can be placed anywhere a single statement can be placed, it’s also possible to have an empty statement, which is simply a semicolon (;) where a statement typically would be. An empty statement has no effect.

Placing a semicolon after the parenthesized condition in an if or if...else statement leads to a logic error in single-selection if statements and a syntax error in double-selection if...else statements (when the if-part contains a body statement).

# 3.6.3 Conditional Operator (?:)

C++ provides the conditional operator (?:), which can be used in place of an if...else statement. This can make your code shorter and clearer. The conditional operator is C++’s only ternary operator (i.e., an operator that takes three operands). Together, the operands and the ?: symbol form a conditional expression. For example, the following statement prints the conditional expression’s value:

```
```cpp
cout << (studentGrade >= 60 ? "Passed" : "Failed");
```
```