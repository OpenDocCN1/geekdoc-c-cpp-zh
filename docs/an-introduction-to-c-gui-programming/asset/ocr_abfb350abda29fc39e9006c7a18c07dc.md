# Chapter 4

# More advanced
flow control

For loops and case statements - more advanced
ways of controlling the flow of a program

The if statement and while loop described in the previous chapter are fairly simple control structures. In this chapter, we're going to look at a few more complex structures that can help to make your code shorter and reduce the amount of typing you need to do.

Although the while loop we saw in the previous article is very useful the for loop tends to be favoured by many programmers, as it puts all the logic controlling the loop in one place Here's an example:

```
#include <stdio.h>

void main (void)
{
    int a;

    for (a = 0; a < 5; a++) {
        printf("a is equal to %d\n", a);
    }
    printf("a is equal to %d and I've finished\n", a);
}
```

This isn't all that different from a while loop, but all of the control for the loop lives in the round brackets after the for keyword This contains three statements, separated by semicolons; in order, these are the initial condition, the test, and the increment.
a = 0 is the initial condition, the variable a is initialised to 0 at the start of the loop.
a < 5 is the test, just like in a while loop. This is checked on each iteration of the loop, the loop code is only executed if the test evaluates to true; as soon as the test is false, execution continues after the curly bracket at the end of the loop code.