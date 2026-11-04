
## Exercises

### C.5.15 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int a = 10, b = !a;

    a = b ? 50 : 200;
    printf("Val = %d\n", a);
    return 0;
}
```

Answer: The statement a = b ? 50 : 200; is equivalent to: a = (b != 0) ? 50 : 200; Since b is 0, a becomes 200 and the program displays: Val = 200.

### C.5.16 Write a program that reads a student's grade and stores it in a variable only if the input grade is within [5,10]. Otherwise, the variable should be set to -1. Use the conditional operator.

```c
#include <stdio.h>
int main(void)
{
    float i, grd;

    printf("Enter grade: ");
    scanf("%f", &grd);

    i = (grd >= 5 && grd <= 10) ? grd : -1;
    printf("%f\n", i);
    return 0;
}
```

### C.5.17 Write a program that reads an integer and displays a message to indicate whether it is positive or negative. If it is 0, the program should display Zero. Use the conditional operator.

```c
#include <stdio.h>
int main(void)
{
    int num;

    printf("Enter number: ");
    scanf("%d", &num);

    num > 0 ? printf("Pos\n") : (num < 0) ? printf("Neg\n") : printf("Zero\n");
    return 0;
}
```

Comments: Alternatively, we could write:

```
printf("%s\n", num > 0 ? "Pos" : num < 0 ? "Neg" : "Zero");
```

### C.5.18 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int a = -10;
    if(((a < 0) ? -a : a) <= 10)
        printf("One %d\n", -a);
    else
        printf("Two %d\n", -a);
    return 0;
}
```

Answer: Since a is -10, the result of the conditional expression is -a, that is, 10. Notice that the value of a does not change, it remains equal to -10. Therefore, since the if condition is true, the program displays: One 10

### C.5.19 The following program reads the prices of three products and displays the highest price. Use the conditional operator to replace the if-else statements and a single printf() to display the highest price.

```c
#include <stdio.h>
int main(void)
{
    float i, j, k;
    printf("Enter prices: ");
    scanf("%f%f%f", &i, &j, &k);
    if(i >= j && i >= k)
        printf("Max = %f\n", i);
    else if(j > i && j > k)
        printf("Max = %f\n", j);
    else
        printf("Max = %f\n", k);
    return 0;
}
```

Answer: printf("Max = %f\n", (i >= j && i >= k) ? i : (j > i && j > k) ? j : k); To display the lowest price change > to <.

### C.5.20 Write a program that reads a student's grade and uses the conditional operator to display a corresponding message according to the next scale:

- a. If grade is within [7.5–10], the program outputs: A
- b. If grade is within [5–7.5), the program outputs: B

As a matter of style, there are several ways to write the switch statement. The most popular is to put the statements under the case label and the break statement some space(s) inner or aligned with the statements. Our preference is to align each break with the case label and leave a space between each case and the preceding break.

The expression must be an integer variable or expression in parentheses, and the values of all constant_1, constant_2,..., constant_n must be integer constant expressions (e.g., 30 is a constant expression, and 30+40 as well) with different values. The order of the cases does not matter. When the switch statement is executed, the value of the expression is compared with each case constant. If a match is found, the group of statements of the respective case will be executed and the remaining cases will not be tested. If no match is found and a default case is present, its group of statements will be executed. The break statement terminates the execution of the switch and the program continues with the next statement after the switch. We'll discuss more about the break statement in Chapter 6. switch statements may be nested, and a case or default clause is associated with the enclosing switch.

For example, the following program reads an integer, and if it is 1, it outputs One; if it is 2, it outputs Two; otherwise, it outputs Other. In any case, the break statement terminates the switch and the program outputs End.

~~~c
#include <stdio.h>
int main(void)
{
    int a;

    printf("Enter number: ");
    scanf("%d", &a);

    switch(a)
    {
        case 1:
            printf("One\n");
            break;

        case 2:
            printf("Two\n");
            break;

        default:
            printf("Other\n");
            break;
    }
    printf("End\n");
    return 0;
}
~~~

Notice that the default case is optional; it may also appear anywhere in the list of cases, and will be executed if there is no match. If it is present, our suggestion is to put it always at the end to make it clear. If it is missing and there is no matching case, no action takes place.

Let's make a parenthesis for the default case. Typically, it is used to report an "impossible" condition. One time, I've chosen to output the message Panic: Wish you weren't here paraphrasing the classical song of Pink Floyd. As you may guess, this wrong situation had never occurred during the testing phase. Can you imagine when it occurred? After

```
case 3:
    printf("Three\n");
    break;
default:
    printf("Other\n");
    break;
}
printf("End\n");
return 0;
}
```

Since a is 1, the first case outputs One. However, since there is no break, the switch statement is not terminated and the execution falls through to the next cases, until the break is met. Therefore, the program outputs Two and Three. The break statement terminates the switch and the program displays End. If that break was missing, the program would also output Other. The last break can be omitted, since the right brace } terminates the switch anyway. Our preference is to put it, not only to keep a uniform style, but to have it as a safe guard if some day another case is added there.

![](img/b8da5dcf9ba7f1fad5213c453d095246_115_0.png)

> Typically, the absence of break is a cause of a potential bug. If you deliberately omit it, add a comment to state it explicitly, so that someone who reads your code or even you after a while won't wonder.

If we want to execute the same block of statements in more than one case, we can merge them together. For example:

```
case constant_1:
case constant_2:
case constant_3:
/* block of statements that will be executed if the value of the expression matches any of constant_1 or constant_2 or constant_3. */
break;
```

In another example, the following program reads an integer that represents a month (1 for January, 12 for December) and displays the season in which the month belongs to.

```c
#include <stdio.h>
int main(void)
{
    int month;

    printf("Enter month [1-12]: ");
    scanf("%d", &month);

    switch(month)
    {
        case 12:
        case 1:
        case 2:
            printf("Winter\n"); /* If the input value is 1, 2 or 12, the program outputs Winter. */
            break;

        case 3:
        case 4:
        case 5:
            printf("Spring\n");
            break;

        case 6:
        case 7:
        case 8:
            printf("Summer\n");
            break;

        case 9:
        case 10:
        case 11:
            printf("Autumn\n");
            break;

        default:
            printf("Error: Wrong month\n");
            break;
    }
    return 0;
}
```

## switch versus if

The main disadvantage of the switch statement is that we can make tests only for equality, that is, to test whether the value of an expression matches one of the case constants. In contrast, we can use if to test any kind of condition. Moreover, the case constants are restricted to integers and the expression must be an integer variable or expression only. Because characters are treated as small integers they may be used, but floating-point numbers and strings are not permitted. On the other hand, the use of the switch statement in place of cascaded if-else-if statements may make the program easier to read in some situations. For example, a typical use of the switch statement is to handle user choices in a menu of commands.

## Exercises

### C.5.21 Write a program that simulates a physical calculator. The program should read the symbol of an arithmetic operation and two integers and display the result of the arithmetic operation.

```c
#include <stdio.h>
int main(void)
```
