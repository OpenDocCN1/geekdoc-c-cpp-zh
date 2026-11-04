Caught you sleeping? Is 30 your answer?
Who told you that the += is a compound operator? You were warned in Chapter 4 that
the = in a compound operator comes second, weren't you? Therefore, the statement
sum += 10; is equivalent to sum = sum +10;, which merely assigns 10 to sum, and that is the
output value.

Basically, the main purpose of this example is to show you that when reading code,
even if it is few lines, imagine the case of thousands, it is very easy to skip an easy bug.
Sometimes, the easier to insert a bug, the harder to find it. Just remember, when writing
code, you should be particularly concentrated, cautious, and in a good mood. Continue
with the exercises, watch out for the next traps though.

# Exercises

+   **C.6.26** Write a program that reads integers continuously and displays them until the user enters 0. The number 0 must not be displayed.

```
~~~c
#include <stdio.h>
int main(void)
{
    int i = 1; /* Initialize with a nonzero value, just to be sure
that the loop will be executed. */
    while(i != 0)
    {
        printf("Enter number: ");
        scanf("%d", &i);
        if(i != 0)
            printf("Num = %d\n", i);
    }
    return 0;
}
~~~
```

+   **C.6.27** Find the number of iterations in the following program.

```
~~~c
#include <stdio.h>
int main(void)
{
    int a = 256, b = 2;

    while(a != b)
    {
        b = b*b;
        a >>= 2;
    }
    return 0;
}
~~~
```