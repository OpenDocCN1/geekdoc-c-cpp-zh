longer will you put off going to the dentist? The computer is no different, albeit the comparisons it makes use values, not abstracts, as illustrated in Listing 8-1.

# Listing 8-1: A Simple Comparison

```
#include <stdio.h>
int main()
{
    int a,b;
    a = 6;
    b = a - 2;
    if (a > b)
    {
        printf("%d is greater than %d\n",a,b);
    }
    return(0);
}
```

# Exercise 8-1

Create a new program using the source code shown in Listing 8-1. Build and run. Here's the output you should see:

> 6 is greater than 4

Fast and obedient, that's what a computer is. Here's how the code works:

Line 5 declares two integer variables: a and b. The variables are assigned values in Lines 7 and 8; the value of variable b is assigned to the value of variable a minus 2.

Line 10 makes a comparison:

> if (a > b)

Programmers read this line as, “If a is greater than b.” Or when they're teaching the C language, they say, “If variable a is greater than variable b.” And, no, they don’t announce the parentheses.

Lines 11 through 13 form a block that belongs to the if statement. The meat in the sandwich is Line 12; the curly brackets don’t play a decision-making role, other than hugging the statement at Line 12. When the if expression at Line 10 is true, the statement in Line 12 is executed. Otherwise, all statements in the block are skipped.