# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

of the resultant string $D$ should satisfy $L \le D \le U$, with the extra stipulation that the error should have a correct sign for the current running direction.

# Returns

+   The `printf` function returns the number of characters transmitted, or a negative value if an output or encoding error occurred.

# Environmental limits

+   The number of characters that can be produced by any single conversion shall be at least 4095.

+   EXAMPLE 1 To print a date in the form "Sunday, July 3, 10:02" followed by $\pi$ to five decimal places:

```
#include <math.h>
#include <stdio.h>
/* */
char *weekday, *month; // pointers to strings
int day, hour;
printf(stdout, "%s, %s, %2d:%02d\n", weekday, month, day, hour);
printf(stdout, "%pi = %.5f\n", 4 * atan(1.0));
```

+   EXAMPLE 2 In this example, multiple characters do not have a state-dependent encoding, and the members of the extended character set that consist of more than one byte each consist of exactly two bytes, the first of which is denoted by $ackslash$ and by an uppercase letter.

+   Given a wide string with `wstr[] = "L\X\Yabc\ZW";

the calls

will print the following lines:

```
123456789012
XabcZW
XYabcZ
XYabcZW
XYabcZW
Z
```

Forward references: conversion state (7.29.6), the wctomb function (7.29.6.3).