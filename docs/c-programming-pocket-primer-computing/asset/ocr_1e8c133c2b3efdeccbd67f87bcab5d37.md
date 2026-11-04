# WORKING WITH FOR LOOPS

Listing 3.1 displays the contents of ForLoop.c that shows you how to use a for loop in C.

```
**LISTING 3.1: ForLoop.c**

```
#include <stdio.h>

int main()
{
   int max=5;
   for(int i=0; i<max; i++)
   {
      printf("i : %d\n", i);
   }

   return 0;
}
```
```

Listing 3.1 is straightforward: a `main()` function that initializes the integer-valued variable max (its value is 5), followed by a for loop that prints the integers between 0 and max.

The output from launching the C program in Listing 3.1 is here:

```
```
i : 0
i : 1
i : 2
i : 3
i : 4
```
```

# WORKING WITH BREAK AND CONTINUE IN FOR LOOPS