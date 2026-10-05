Trailing whitespace (including new-line characters) is left un unless matched by a directive. The success of literal matches and suppressed assignments is not directly determinable other than via the %n directive.

# Returns

The fscanf function returns the value of the macro EOF if an input failure occurs before the first conversion (any) has completed. Otherwise, the function returns the number of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

EXAMPLE 1 The call:

```
#include <stdio.h>
/* ... */
int n, i; float x; char name[50];
n = fscanf(stdin, "%d%f%s", &i, &x, name);
```

with the input:

```
25 54.32-E1 thompson
```

will assign to n the value 3, to the i value 25, to x the value 5.432, and to name the sequence thompson\0.

EXAMPLE 2 The call:

```
#include <stdio.h>
/* ... */
int i; float x; char name[50];
fscanf(stdin, "%d%f*d %[0123456789]", &i, &x, name);
```

with input:

```
56789 0123 56a72
```

will assign to i the value 56 and to x the value 789.0, and will assign to name the sequence 56\0. The next character read from the input stream will be a.

EXAMPLE 3 To repeatedly read from stdin a quantity, a unit of measure, and an item name:

```
#include <stdio.h>
/* ... */
int count; float quant; char units[21], item[21];
d {
    count = fscanf(stdin, "%d%20s of %20s", &count, units, item);
    fscanf(stdin, "%*[^\n]");
} (!feof(stdin) && !ferror(stdin));
```

If the stdin stream contains the following lines:

+   2 quarts of oil
-12.8degrees Celsius
lots of luck
10.0LBS of
dirt
100ergs of energy