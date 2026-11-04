
the loop body. In fact, this is executed only once, after the loop ends. Let's trace the iterations:

First iteration. Since i is 12, the condition i > 2 (12 > 2) is true and the program displays 12.

Second iteration. With the statement i-=5 (i = i-5), i becomes 7. Therefore, the condition i > 2 (7 > 2) is true and the program displays 7.

Third iteration. Now, i becomes 2. Therefore, the condition i > 2 (2 > 2) is false and the loop terminates.

Next, the second printf() displays the current value of i. Therefore, the program displays 12 7 End = 2

Here is the second trap. Since j is declared as unsigned, it will never become negative (e.g., -1). Therefore, the second loop is infinite and the program outputs Test forever.

### C.6.3 Write a program that reads an integer, and if it is within [10, 20], the program should display the word One a number of times equal to the input integer. Otherwise, the program should read 10 integers and display the negatives.

```c
#include <stdio.h>
int main(void)
{
    int i, num;

    printf("Enter number: ");
    scanf("%d", &num);

    if(num >= 10 && num <= 20)
    {
        for(i = 0; i < num; i++)
            printf("One\n");
    }
    else
    {
        for(i = 0; i < 10; i++)
        {
            printf("Enter number: ");
            scanf("%d", &num);
            if(num < 0)
                printf("%d\n", num);
        }
    }
    return 0;
}
```

Comments: The braces after the if and else statements are not needed because only the for statement is contained. The reason we are using them is for better readability.

## The break Statement

We have already discussed how a **break** statement terminates the execution of a **switch** statement. It can also be used to terminate a **for**, **while**, or **do-while** loop and transfer control out of the loop. For example:

```c
#include <stdio.h>
int main(void)
{
    int i;
    for(i = 1; i < 10; i++)
    {
        if(i == 5)
            break;
        printf("%d ", i);
    }
    printf("End = %d\n", i);
    return 0;
}
```

As long as i is not 5, the if condition is false and the program displays the values of i from 1 to 4. When i becomes 5, the **break** statement terminates the loop and the program continues with the execution of the outer printf(). Therefore, the program displays: 1 2 3 4 End = 5

Each **break** terminates the execution of the loop or the **switch** statement in which it is contained. For example, what is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int i;
    for(i = 1; i < 10; i++)
    {
        switch(i)
        {
            case 4:
                break;
            default:
                if(i == 3)
                    break;
                else
                    printf("%d", i);
                break;
        }
        if(i == 6)
            break;
    }
    return 0;
}
```

In the first two iterations, the default case outputs 1* and 2* and the break statement terminates the switch statement, not the for statement. Be careful now, in the third iteration, it is the break statement inside if that terminates switch and the program displays nothing. In the fourth iteration, it is the break statement in the first case that terminates switch and the program displays nothing. The fifth iteration outputs 5*, the next one 6* and the outer break terminates the loop. Therefore, the program outputs: 1* 2* 5* 6*.

And now that we remembered switch, here is a new challenge for you; can you tell us what does the following program output?

```c
#include <stdio.h>
int main(void)
{
    int i;

    for(i = 1; i < 12; i++)
    {
        switch(i)
        {
            case 1: i += 2;
            case 2: i += 3;
            default: i += 4;
        }
    }
    printf("%d", i);
    return 0;
}
```

As you guessed, we used that indenting in the switch statement on purpose to confuse you. In the first iteration, since i is 1, the program executes the statement of the first case and continues with the next ones, since break is missing. Therefore, i becomes 10. In the second iteration, because i is now 11, only the default case is executed and i becomes 15. Next, i becomes 16, the loop ends, and that is the output value.

## The continue Statement

The continue statement can be used only inside a for, while, or do-while loop. While the break statement ends the loop, the continue statement terminates the current iteration of the enclosing loop and causes the next iteration to begin. The rest of the loop body is skipped for the current iteration. For example, consider the following program:

```c
#include <stdio.h>
int main(void)
{
    int i;
    for(i = 1; i < 10; i++)
    {
        if(i < 5)
            continue;
        printf("%d ", i);
    }
    return 0;
}
```

As long as i is less than 5, the if condition is true and the continue statement terminates the current iteration. The rest of the loop body, that is, printf(), is skipped and the program continues with the i++ statement. When i becomes greater or equal to 5, the continue statement is not executed and the program displays the value of i. As a result, the program outputs: 5 6 7 8 9.

Notice that we can avoid the use of continue by testing the reverse condition. For example:

```
if(i >= 5)
    printf("%d ", i);
```

As a matter of style, our preference is to use the continue statement rather than reverse logic, in order to make clear to the reader which is the condition that triggers the next iteration. For example, it is clearer to write the following code rather than use reverse logic:

```
if(a >= 5 || b != 10 || c < -8)
    continue;
```

Unlike break, the continue statement does not apply to switch. A continue statement inside a switch, which is inside a loop, triggers the next loop iteration. Therefore, in

the second example of the previous section, what does the program output if we change the default case to:

```
default:
    if(i == 3)
        break;
    else
        continue;
printf("* ");
break;
```

Since the continue statement causes the next iteration to begin, the program displays nothing.

## Exercises

### C.6.4 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int i = 0, j = 5;
    for(i > j; i+j == 5; j < 2)
    {
        printf("One\n");
        i = 4;
        j = 2;
    }
    printf("%d %d\n", i, j);
    return 0;
}
```

Answer: The value of i > j is 0; however, this does not affect the execution of the loop. Let's trace the iterations:

First iteration. Since i is 0, the condition i+j == 5 (0+5 = 5 == 5) is true and the program outputs One. Next, i and j become 4 and 2, respectively.

Second iteration. The value of j < 2 is 0; however, this does not affect the execution. Since the condition i+j == 5 (4+2 = 6 == 5) becomes false, the loop ends.

The program displays the values of i and j, that is, 4 and 2, respectively.

### C.6.5 A test consists of 10 multiple choice questions, each of which has three possible answers. The first answer gets three points, the second one point, and the third two points. Write a program that uses the switch statement to read the test taker's 10 answers and display the final score.

```c
#include <stdio.h>
int main(void)
{
    int i, ans, points;

    points = 0;
    for(i = 0; i < 10; i++)
    {
        printf("Enter answer [1-3]: ");
        scanf("%d", &ans);

        switch(ans)
        {
            case 1:
                points += 3;
            break;

            case 2:
                points += 1;
            break;

            case 3:
                points += 2;
            break;

            default:
                printf("Error: Wrong answer ...\n");
            break;
        }
    }
    printf("Candidate gets %d points in total\n", points);
    return 0;
}
```

### C.6.6 What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int i, j;

    for(i = 10, j = 2; i != j; i-=2, j+=2)
        printf("%d %d\n", i, j);
    return 0;
}
```

Answer: The loop terminates when i equals j. That happens, after the second iteration, when both become 6. Therefore, the loop is executed twice and the program displays:

10 2
8 4
