
if (!x) is equivalent to if (x == 0)

The position of the braces, not only in case of if, but also in the loop statements of Chapter 6, is a matter of personal preference. For example, many programmers prefer the K&R style:

```
if (x == 0) {
    printf("Yes\n");
}
```

The reason we don't prefer this style is because the left brace is not clearly shown. Our preference is to put each brace in a separate line, so that we can easily check that they match. You may choose the style you like more. However, the common practice, and this is what we strongly recommend, is to indent the inner statements in order to make clearer their grouping and the code easier to read. We use the same style for the loop statements in Chapter 6.

If the block of statements consists of a single statement, the braces can be omitted. For example, the previous code could be written like this:

```
if (x == 0)
    printf("Yes\n");
```

In general, the braces are used to group declarations and statements into a compound statement, or block, which is treated by the compiler as a single statement. As we'll see in Chapter 6, compound statements are also very common in loops.

## Common Errors

A common error is to add a semicolon (;) at the end of the if statement, as you usually do with most statements. The semicolon is handled as a statement that does nothing, that is, a null statement, and the compiler terminates the if. For example, in the following code:

```
int x = -3;
if (x > 0);
    printf("Yes\n");
```

the ; terminates the if statement, so the printf() call is not inside if. Therefore, this code outputs Yes regardless of the value of x.

A very popular error is to confuse the == equality operator with the = assignment operator. Remember that the == operator checks whether two expressions have the same value, while the = operator assigns a value to a variable. Also remember that the assignment of a nonzero value to a variable corresponds to a true expression, while the assignment of zero value corresponds to a false expression. For example, the following code:

```
int x = -10;
if (x = -20)
    printf("Yes\n");
```

If the condition is true, the first block of statements is executed, otherwise the second one. For example, the following code outputs Two, because x is less than 0.

```
int x = -3;
if(x > 0)
{
    printf("One\n");
}
else
{
    printf("Two\n");
}
```

And, since both blocks consist of a single statement, we could omit the braces:

```
int x = -3;
if(x > 0)
    printf("One\n");
else
    printf("Two\n");
```

## Nested if Statements

An if statement may contain other if and else statements, which in turn may contain others, and so on. For example, the following program contains two nested if statements:

```
#include <stdio.h>
int main(void)
{
    int a = 10, b = 20, c = 30;

    if(a > 5)
    {
        if(b == 20)
            printf("1 ");

        if(c == 40)
            printf("2 ");
        else
            printf("3 ");
    }
    else
        printf("4\n");

    return 0;
}
```

Since a is greater than 5, the program outputs: 1 3

Because the else part is optional, there is an ambiguity when an else is omitted from a nested if sequence. To match if and else statements, the rule is that an else is associated with the closest unmatched if inside the same group of statements. For example, can you apply the rule and tell us what does the following program output?

```
#include <stdio.h>
int main(void)
{
    int a = 5;
    if(a != 5)
        if(a-2 > 5)
            printf("One\n");
    else
        printf("Two\n");
    return 0;
}
```

According to this rule, the else statement is associated with the inner if. As a result, the program displays nothing because the first if condition is false and it has no else associated with.

Notice how the indenting can trick you into thinking that the else statement is associated with the first if statement. By aligning each else statement with the matching if, indenting the statements, and adding braces to if-else statements even if you don't have to, the program becomes easier to read. For example, here is how we could make the previous program more readable by aligning the correct if with the matching else:

```
#include <stdio.h>
int main(void)
{
    int a = 5;
    if(a != 5)
    {
        if(a-2 > 5)
            printf("One\n");
        else
            printf("Two\n");
    }
    return 0;
}
```

Although the braces of the first if are not needed, we add them to make the code more readable. If something else is desired, braces must be used to force the proper association. For example:

```
if(a != 5)
{
    if(a-2 > 5)
        printf("One\n");
}
else
    printf("Two\n");
```

To test a series of conditions, the typical choice is to use the following syntax:

```
if(condition_A)
{
    ... /* block of statements A */
}
else if(condition_B)
{
    ... /* block of statements B */
}
else if(condition_C)
{
    ... /* block of statements C */
}
.
.
.
else /* optional */
{
    ... /* block of statements N */
}
```

There can be any number of else if clauses between the first if and the last else. The conditions are evaluated in order starting from the top. Once a true condition is found, the corresponding block of statements is executed and the remaining else if conditions are not evaluated. The program continues with the execution of the next statement after the last else. For example, if condition_A is true, the first block of statements is executed; if not, condition_B is checked. If it is true, the second block of statements is executed; if not, condition_C is checked, and so on. If none condition is true and the last else is present, its block of statements will be executed. The following program reads an integer and displays a message according to the input value:

```
#include <stdio.h>
int main(void)
{
    int a;

    printf("Enter number: ");
    scanf("%d", &a);

    if(a == 1)
        printf("One\n");
    else if(a == 2)
        printf("Two\n");
    else
        printf("Other\n");

    printf("End\n");
    return 0;
}
```

### C.53 Write a program that reads two integers and displays their relationship without using an else statement.

```c
#include <stdio.h>
int main(void)
{
    int i, j;

    printf("Enter numbers: ");
    scanf("%d%d", &i, &j);

    if (i < j)
        printf("%d < %d\n", i, j);
    if (i > j)
        printf("%d > %d\n", i, j);
    if (i == j)
        printf("%d = %d\n", i, j);
    return 0;
}
```

### C.54 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int a = 4, b = 5, c = 3;

    if (a && a/b)
        printf("One\n");
    else
        printf("Two\n");

    if (++a == b++)
        printf("One\n");
    else
        printf("Two\n");

    if (a < b < c)
        printf("One\n");
    else
        printf("Two\n");
    return 0;
}
```

Answer: Since the / operator has higher precedence than the && operator, the division is performed first. The result of a/b is 0, not 0.8, because a and b are both integer variables. Therefore, the condition is false and the program displays Two. The == operator has lower precedence than the ++ operator applied in both forms. The prefix form first increases a and makes it 5. The postfix form increases b, after b is used in the comparison. Therefore, since b is 5, the program displays One and b becomes 6. According to the precedence rules, the < operator is left associative. Since a is 5 and b is 6, the expression a < b is true, so its value is 1. Therefore, the expression (a < b < c) is equivalent to (1 < c), which is true because c is 3. Therefore, the program displays One. Remember, if we want to compare b against a and c we would use the && operator and write: if(a < b && b < c)

### C.5.5 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    int i = 10, j = 20, k = 0;

    if(i = 40)
        printf("One ");
    if(j = 50)
        printf("Two ");
    if(k = 60)
        printf("Three ");
    if(k = 0)
        printf("Four ");
    printf("%d %d %d\n", i, j, k);
    return 0;
}
```

Answer: This is an example of how the wrong use of the = operator instead of the == operator can produce unexpected results. In particular, the if conditions don't test the variables for equality, but the variables are assigned with the respective values instead. As a result, i becomes 40, j becomes 50, while k first becomes 60, and then 0. Since the first three if conditions are true and the fourth is false (since 0 is assigned to k), the program displays One Two Three 40 50 0

### C.5.6 Write a program that reads two floats (e.g., a and b) and displays the solution of the equation a*x + b = 0, if any.

```
#include <stdio.h>
int main(void)
{
    double a, b;

    printf("Enter numbers: ");
    scanf("%lf%lf", &a, &b);

    if(a == 0)
    {
        if(b == 0)
            printf("Infinite solutions\n");
        else
            printf("There is no solution !!\n");
    }
    else
        printf("The solution is %f\n", -b/a);
    return 0;
}
```
