```
while ((status = scanf("%d", &code)) != 1 ||
    (code < 1 || code > 5))
```

This code fragment uses C’s guarantee that logical expressions are evaluated from left to right and that evaluation ceases the moment the statement is clearly false. In this instance, the values of code are checked only after it is determined that scanf() succeeded in reading an integer value.

Assigning separate tasks to separate functions encourages this sort of refinement. A first pass at menu() or getnights() might use a simple scanf() without the data-verification features that have been added. Then, after the basic version works, you can begin improving each module.

# Finding Addresses: The & Operator

One of the most important C concepts (and sometimes one of the most perplexing) is the pointer, which is a variable used to store an address. You’ve already seen that scanf() uses addresses for arguments. More generally, any C function that modifies a value in the calling function without using a return value uses addresses. We’ll cover functions using addresses next, beginning with the unary & operator. (The next chapter continues the exploration and exploitation of pointers.)

The unary & operator gives you the address where a variable is stored. If pooh is the name of a variable, &pooh is the address of the variable. You can think of the address as a location in memory. Suppose you have the following statement:

```
pooh = 24;
```

Suppose that the address where pooh is stored is 0B76. (PC addresses often are given as hexadecimal values.) Then the statement

```
printf("%d %p\n", pooh, &pooh);
```

would produce this (%p is the specifier for addresses):

```
24 0B76
```

Listing 9.12 uses this operator to see where variables of the same name—but in different functions—are kept.

# Listing 9.12 The loccheck.c Program

```
/* loccheck.c -- checks to see where variables are stored */
#include <stdio.h>
void mikado(int);          /* declare function */
int main(void)
{
    int pooh = 2, bah = 5;     /* local to main() */
```