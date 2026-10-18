```
```c
statement(s);
}
statement(s);
}
```
```

The syntax for a **nested do...while loop** statement in C programming language is as follows:

```
```c
do
{
    statement(s);
    do
    {
        statement(s);
    }while( condition );
}while( condition );
```
```

A final note on loop nesting is that you can put any type of loop inside any other type of loop. For example, a ‘for’ loop can be inside a ‘while’ loop or vice versa.

# Example

The following program uses a nested for loop to find the prime numbers from 2 to 100:

```
```c
#include <stdio.h>

int main ()
{
    /* local variable definition */
    int i, j;

    for(i=2; i<100; i++) {
        for (j=2; j <= (i/j); j++)
            if(!(i%j)) break;          // if factor found, not prime
        if(j > (i/j)) printf("%d is prime\n", i);
    }
}
```
```