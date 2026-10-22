
## break Statement

The break statement terminates the loop (`for`, `while`, and `do...while` loop) immediately when it is encountered. The break statement is used with decision-making statements such as `if...else`. In C programming, the break statement is also used with the `switch...case` statement.

### Syntax of break statement

```c
break;
```

### Flowchart of break statement

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_56_0.png)

### How break statement works?

```c
while (test Expression)
{
    // codes
    if (condition for break)
    {
        break;
    }
    // codes
}
```

```c
for (init, condition, update)
{
    // codes
    if (condition for break)
    {
        break;
    }
    // codes
}
```

### Example #1: break statement

```c
// Program to calculate the sum of maximum of 10 numbers
// Calculates sum until user enters positive number

#include <stdio.h>

void main()
{
    int i;
    double number, sum = 0.0;

    for(i = 1; i <= 10; ++i)
    {
        printf("Enter a n%d: ", i);
        scanf("%lf", &number);

        // If user enters negative number, loop is terminated
        if(number < 0.0)
        {
            break;
        }

        sum += number; // sum = sum + number;
    }

    printf("Sum = %.2lf", sum);
}
```

### Output

```text
Enter a n1: 2.4

Enter a n2: 4.5

Enter a n3: 3.4

Enter a n4: -3

Sum = 10.30
```

## Continue Statement

The continue statement skips some statements inside the loop. The continue statement is also used with decision-making statements such as `if...else`.

### Syntax of continue Statement

```c
continue;
```

### Flowchart of continue Statement

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_59_0.png)

### How continue statement works?

```c
while (test Expression)
{
    // codes
    if (condition for continue)
    {
        continue;
    }
    // codes
}
```

```c
for (init, condition, update)
{
    // codes
    if (condition for continue)
    {
        continue;
    }
    // codes
}
```

```c
// Program to calculate sum of maximum of 10 numbers
// Negative numbers are skipped from calculation

#include <stdio.h>

int main()
{
    int i;
    double number, sum = 0.0;

    for(i = 1; i <= 10; ++i)
    {
        printf("Enter a n%d: ", i);
        scanf("%lf", &number);

        // If user enters negative number, loop is terminated
        if(number < 0.0)
        {
            continue;
        }

        sum += number; // sum = sum + number;
    }

    printf("Sum = %.2lf", sum);

    return 0;
}
```

### Output

```text
Enter a n1: 1.1

Enter a n2: 2.2

Enter a n3: 5.5

Enter a n4: 4.4

Enter a n5: -3.4

Enter a n6: -45.5

Enter a n7: 34.5

Enter a n8: -4.2

Enter a n9: -1000

Enter a n10: 12

Sum = 59.70
```

In the program, when the user enters a positive number, the sum is calculated using `sum += number;` statement.

When the user enters a negative number, the `continue` statement is executed and skips the negative number from calculation.

## Branching & Looping

### Looping (repetition)

A set of statements may have to be repeatedly executed for a specified number of times or till a condition is satisfied. The statements that help us to execute a set of statements repeatedly are called looping or repetitive or iterative statements.

There are 3 types of loops in C:

- while loop
- for loop
- do-while loop

Any looping construct will have to perform 3 tasks, namely initialization, condition checking, and incrementation. The difference between the three looping control constructs is the order in which they perform the 3 tasks, i.e. (initialization, increment, condition checking).

### The while loop

It is a pretest or entry-controlled loop, and hence the condition is evaluated first and the body of the loop is executed only if the condition is true. It is also a condition-controlled or event-controlled loop.

#### Syntax

```c
initialization;

while(condition)
{
    Statement;
    updation;
}
Statement;
```

#### Working

1. Initialization of loop control variable is done.
2. Next condition is checked.
3. If the condition is evaluated to true, then control enters the body of the loop and executes the statements in the body.
4. Next updates the loop counter variable, after which control goes back to the condition check. If the condition is true, again the body is executed.
5. This process repeats as long as the condition evaluates to be true. Once the condition evaluates to be false, the control flows to the statement outside the body of the loop.

#### Example

```c
/* program to display numbers from 1-10 */

#include<stdio.h>

void main()
{
    int i;

    i = 0;              /* initialization */
    while(i <= 10)      /* condition checking */
    {
        printf("%d\n", i);
        i++;            /* updation */
    }
    getch();
}
```

**Note:** Study corresponding lab programs and the programs given in theory class.

### for loop

Using this we can execute a set of statements repeatedly for a specified number of times. So it is also called a counter-controlled loop. It is a pretest or top-testing loop.

#### Syntax

```c
for(initialization; condition check; updation)
{
    Statements
}
```

#### Working

1. Here initialization, condition check, and updation are done in the same statement.
2. Initialization of the loop counter is performed.
3. Condition is checked. If the condition evaluates to be true, then the control enters the body of the loop. The statements in the body are executed.
4. Updation of the loop counter is performed. After which again the control goes back to condition check. If the condition is true, again the body is executed.
5. This process repeats as long as the condition evaluates to be true. Once the condition evaluates to be false, the control flows to the statement outside the body of the loop.

#### Example

```c
/* program to display numbers from 1-10 */

#include<stdio.h>

void main()
{
    int i;

    for(i = 0; i <= 10; i++)
    {
        printf("%d\n", i);
    }

    getch();
}
```

**Note:** Study corresponding lab programs and the programs given in theory class.

### Do-while

It is a post-test or bottom-test loop, and hence the body of the loop is executed first and then the condition is checked.

#### Syntax

```c
Initialization;

do
{
    statement;
    updation;
} while(condition);  /* note: there is a semi-colon at the end of while */

statements
```

#### Working

1. Initialization is performed first.
2. Then the statements inside the body of the loop are executed one after another.
3. Updation is performed at the end of the body, and then the condition is checked.
4. If the condition is evaluated to be true, then the control re-enters the body and executes the statements within the body.
5. This process repeats as long as the condition evaluates to be true.
6. When the condition becomes false, the control comes out of the loop body.

#### Example

```c
#include<stdio.h>

void main()
{
    int i;

    i = 0;                  /* initialization */
    do
    {
        printf("%d\n", i);
        i++;                /* updation */
    } while(i <= 10);       /* condition checking */

    getch();
}
```

**Note:** Study corresponding lab programs and the programs given in theory class.

### Difference between while-loop and do-while loop

|  | While loop | Do-while loop |
|---|---|---|
| **1** | **Syntax**<br><br><code>initialization;</code><br><br><code>while(condition)</code><br><br><code>{</code><br><br><code>Statement;</code><br><br><code>updation;</code><br><br><code>}</code><br><br><code>Statement;</code> | **Syntax:**<br><br><code>Initialization;</code><br><br><code>do</code><br><br><code>{</code><br><br><code>statement;</code><br><br><code>updation;</code><br><br><code>} while(condition);</code><br><br><code>Statement;</code> |
| **2** | It is a top-testing or entry-control loop since the condition is checked in the beginning itself. | It is a bottom-testing or exit-control loop since the condition is checked at the bottom of the loop. |
| **3** | It is a pre-test loop, and if the expression is evaluated to false in the beginning itself, then the statements within the body of the loop will not be executed even once. | It is a post-test loop, and the body of the loop will be executed at least once even if the condition is false. |
| **4** | Example | Example |

### Example

```c
sum = 0;
i = 0;
top: sum = sum + i;
i++;
if(i <= n) goto top;
```

#### Disadvantage

- It is an unstructured programming style.
- Very difficult to read and understand.
- Very difficult to debug the programs.

### The break statement

It is a jump statement which can be used in switch statement and loops.

#### Working

1. In switch statement, it causes control to terminate the switch statement, and the statement following the switch statement will be executed.
2. If break is executed in a loop (for, while, do-while), the control comes out of the loop, and the statement following the loop will be executed.

**Note:** If break appears in the inner loop of a nested loop, control only comes out of the inner loop.

```c
for(............)
{
    for(............)
    {
        ................
        if(error)
            break;
```
