```
c = getchar();
```

The first statement declares that c is a character-type variable. The second statement causes a single character to be entered from the keyboard and then assign to c.

A companion function is **putchar()**, which writes one character to the “standard output.” (The standard output is usually the user's screen).

The syntax of the **putchar()** function is written as

```
*putchar(character variable)*
```

where *character variable* refers to some previously declared character variable.

Example:

```
char c;

...

putchar(c);
```

The first statement declares that c is a character-type variable. The second statement causes the current value of c to be transmitted to the user monitor where it will be displayed.

Using these two functions, we can write a very basic program to copy the input, a character at a time, to the output:

# Program 3.6: Program to copy the input, a character at a time, to the output

```
#include <stdio.h>

/* copy input to output */
main()
{

```