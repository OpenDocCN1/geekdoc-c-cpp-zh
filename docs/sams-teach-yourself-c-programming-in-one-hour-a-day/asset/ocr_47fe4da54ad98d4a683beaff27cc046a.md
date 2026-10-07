# Programming with Multiple Source-Code Files

```
12:   printf("\nThe square of %d is %ld.\\n", x, sqr(x));
13:   return(0);
14: }
```

# Input

LISTING 22.2 calc.c: The Secondary functions.

```
1:   /* Module containing calculation functions. */
2:
3:   #include "calc.h"
4:
5:   long sqr(int x)
6:   {
7:     return ((long)x * x);
8:   }
```

# Input

LISTING 22.3 calc.h: The Header File for calc.c

```
1:   /* calc.h-header file for calc.c. */
2:
3:   long sqr(int x);
4:
5:   /* / end of calc.h */
```

# Output

Enter an integer value: 100

The square of 100 is 10000.

# Analysis

Now at the components of these three files in greater detail. The header file, calc.h, contains the prototype for the sqr() function in calc.c. Any module that uses sqr() needs to know sqr()'s prototype, the module must include calc.h.

The secondary module file, calc.c, contains the definition of the sqr() function. The #include directive is used to include the header file, calc.h. Note that the header filename is enclosed in quotation marks rather than brackets. (You learn the reason for later in this lesson.)

The main module, list2201.c, contains the main() function. This module also includes the header file, calc.h.