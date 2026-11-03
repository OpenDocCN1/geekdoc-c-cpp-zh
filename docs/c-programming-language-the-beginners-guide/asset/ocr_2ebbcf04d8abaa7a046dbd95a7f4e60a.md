# The While Loop

The C language offers several ways of looping. In this section we will discuss the *while* type of loop. You’ll learn how to setup the loop, determine when to stop looping, and how to break out of a loop before it is done.

A loop is a repetitive way to control program execution. You must specify a condition that makes the loop repeat, a set of statements that repeat, and a way for the loop to stop. In the code below, a *while* loop counts from 1 to

```
```c
#include 2

int main()
{
    int x;

    x = 1;
    while(x <= 10)
    {
        printf("%d\n",x);
        x++;
    }

    return(0);
}
```
```