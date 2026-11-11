When a continue statement is executed inside for loop, the control is transferred to the increment/decrement part of the for loop after which the main looping condition is checked to determine whether there are any more iterations needed. When continue is executed with while loop or a do while loop, the control is transferred to the condition part of the while/do...while syntax. Hence, when using while or do...while loop it is the programmers responsibility to do necessary increments or decrements required for the next iteration (if any) before the execution of continue statement, because anything written after continue statement will be skipped once the continue statement is executed.

Let us consider the following example to understand the execution of break and continue statements.

```
```c
#include<stdio.h>
void main()
{
    int k;
        for(k=1; k<=10; k++)
        {
                if(k>=3 && k<=5)
                {
                        printf("Going to next step of loop\n");
                        continue;
                }
                if(k>=7)
                {
                printf("Going out of loop\n");
                break;
                }
        printf("Default loop execution\n");
        }
    printf("Good Bye\n");
}
```
```

# Output

```
```
Default loop execution
Default loop execution
Going to next step of loop
Going to next step of loop
Going to next step of loop
Default loop execution
Going out of loop
Good Bye
```
```

The above program has a loop that runs from k=1 to 10 as its default behaviour.