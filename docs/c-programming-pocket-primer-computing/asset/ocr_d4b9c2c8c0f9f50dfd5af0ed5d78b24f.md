The preceding code block is true in the first else statement, so the remaining portions of the compound if expression involving x are not executed. However, all the expressions involving y are false, which means that nothing is executed in the nested if expression involving the variable y. If necessary, read this example again until it's clear to you that nothing is printed.

# RANKING NUMBERS WITH IF-ELSE STATEMENTS

**Listing 2.5** displays the contents of OrderedValues.c that illustrates how to use if-else logic in a C program to display three numbers in descending order.

**LISTING 2.5:** OrderedValues.c

```
```c
#include <stdio.h>

int main()
{
    int a1=3, a2=8, a3=6, temp;

    printf("ORIGINAL a1: %d a2: %d a3: %d\n", a1, a2, a3);

    if( a1 < a2 )
    {
        temp = a1;
        a1 = a2;
        a2 = temp;
    }

    if( a2 < a3 )
    {
        temp = a2;
        a2 = a3;
```
```