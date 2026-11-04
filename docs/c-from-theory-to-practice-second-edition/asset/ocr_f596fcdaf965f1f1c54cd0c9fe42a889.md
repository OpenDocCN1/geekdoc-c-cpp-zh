# ## The break Statement

We have already discussed how a **break** statement terminates the execution of a **switch** statement. It can also be used to terminate a **for**, **while**, or **do-while** loop and transfer control out of the loop. For example:

```
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
```

As long as i is not 5, the if condition is false and the program displays the values of i from 1 to 4. When i becomes 5, the **break** statement terminates the loop and the program continues with the execution of the outer printf(). Therefore, the program displays: 1 2 3 4 End = 5

Each **break** terminates the execution of the loop or the **switch** statement in which it is contained. For example, what is the output of the following program?

```
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
```