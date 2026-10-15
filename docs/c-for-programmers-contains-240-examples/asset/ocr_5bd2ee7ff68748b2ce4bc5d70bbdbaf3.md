The following example includes a block in the else part of an if...else statement.

```
if ( studentGrade >= 60 )
    cout << "Passed.\n";
else
{
    cout << "Failed.\n";
    cout << "You must take this course again.\n";
}
```

In this case, if studentGrade is less than 60, the program executes both statements in the body of the else and prints

```
Failed.
You must take this course again.
```

Notice the braces surrounding the two statements in the else clause. These braces are important. Without the braces, the statement

```
cout << "You must take this course again.\n";
```

would be outside the body of the else part of the if and would execute regardless of whether the grade was less than 60.

# Common Programming Error 4.3

> Forgetting one or both of the braces that delimit a block can lead to syntax errors or logic errors in a program.

Just as a block can be placed anywhere a single statement can be placed, it is also possible to have no statement at all—called a null statement (or an empty statement). The null statement is represented by placing a semicolon (;) where a statement would normally be.

# Common Programming Error 4.4

> Placing a semicolon after the condition in an if statement leads to a logic error in single-selection if statements and a syntax error in double-selection if...else statements (when the if part contains an actual body statement).

# 4.5 while Repetition Statement

A repetition statement (also called a looping statement or a loop) allows you to specify that a program should repeat an action while some condition remains true.

As an example of C++’s while repetition statement, consider a program segment designed to find the first power of 3 larger than 100. Suppose the integer variable product has been initialized to 3. When the following while repetition statement finishes executing, product contains the result:

```
int product = 3;

while ( product <= 100 )
    product = 3 * product;
```

When the while statement begins execution, the value of product is 3. Each repetition of the while multiplies product by 3, so product takes on the values 9, 27, 81 and 243 suc-