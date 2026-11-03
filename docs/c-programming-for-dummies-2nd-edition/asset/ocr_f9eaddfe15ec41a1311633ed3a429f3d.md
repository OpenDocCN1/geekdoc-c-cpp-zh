# Listing 11-1: Counting Up and Down

```
```c
#include <stdio.h>

int main()
{
    int c;
    for(c=-5;c<5;c++)
    printf("%d ",c);
    for(;c=-5;c--)
    printf("%d ",c);
    putchar('\n');
    return(0);
}
```
```

The crux of what I want you to see happens at Line 9 in Listing 11-1, but it also plays heavily off the first for statement at Line 7. You might suspect that a loop counting from -5 to 5 would have the value 5 as its stop condition, as in

```
for(c=-5;c<5;c++)
```

The problem with this approach is that the value of c is incremented to trigger the end of the loop, which means that c equals 6 when the first for loop is done. If c remains less than 5, as is done at Line 7, then c is automatically set to 5 when the second loop starts. Therefore, in Line 9, no initialization of variable x in the for statement is necessary.

Exercise 11-4: Construct a program that displays values from -10 to 10 then back down to -10. Step in increments of 1, as was done in Listing 11-1, but use two while loops to display the values.

# Prefixing the ++ and -- operators

The ++ operator always increments a variable’s value, and the -- operator always decrements. Knowing that, consider this statement:

```
a=b++;
```

If the value of variable b is 16, you know that its value will be 17 after the ++ operation. So what’s the value of variable a — 16 or 17?