of resultant decimal string $D$ should satisfy $L \le D \le U$, with the extra stipulation that the error should have a correct sign for the current rounding direction.

# Returns

The `fprintf` function returns the number of characters transmitted, or a negative value if an output or encoding error occurred.

# Environmental limits

The number of characters that can be produced by any single conversion shall be at least 4095.

EXAMPLE 1 To print a date and time in the form "Sunday, July 3, 10:02" followed by $\pi$ to five decimal places:

```
```c
#include <stdio.h>
/* // pointers to strings
char *weekday, *month;
int day, hour, min;
fprintf(stdout, "%s, %s %02d:%02d\n", weekday, month, day, hour, min);
fprintf(stdout, "%pi = %.5f\n", 4 * atan(1.0));
```
```

EXAMPLE 2 In this example, multiple characters do not have a state-dependent encoding, and the members of the extended character set that contain more than one byte each of exactly two bytes, the first of which is denoted here by a Box and the second by an uppercase letter.

Given the following string with length seven,

```
```c
static char_t wstr[] = "L\BoxBoxYabc\BoxW";
```
```

```
```c
fprintf(stdout, "%1234567890123\n");
fprintf(stdout, "%%13s\n", wstr);
fprintf(stdout, "%%-13.9s\n", wstr);
fprintf(stdout, "%%13.10s\n", wstr);
fprintf(stdout, "%%13.11s\n", wstr);
fprintf(stdout, "%%13.15s\n", wstr[2]);
fprintf(stdout, "%%13c\n", (int_t) wstr[5]);
```
```

will print the following sequences:

```
```
|1234567890123|
|BoxBoxYabcBoxW|
|BoxYabcZ|
|BoxYabcBoxZ|
|BoxYabcBoxW|
|abcBoxW|
|Z|
```
```

Forward references: conversion state (7.29.6), the wctomb function (7.29.6.3).