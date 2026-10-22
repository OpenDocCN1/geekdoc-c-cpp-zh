This function does change the string, so the function header doesn’t use const in declaring the formal parameter string.

Try the fit() function in the test program of Listing 11.17. Note that the code uses C’s string literal concatenation feature.

# Listing 11.17 The test_fit.c Program

```
/* test_fit.c -- try the string-shrinking function */
#include <stdio.h>
#include <string.h> /* contains string function prototypes */
void fit(char *, unsigned int);

int main(void)
{
    char mesg[] = "Things should be as simple as possible," " but not simpler.";

    puts(mesg);
    fit(mesg,38);
    puts(mesg);
    puts("Let’s look at some more of the string.");
    puts(mesg + 39);

    return 0;
}

void fit(char *string, unsigned int size)
{
    if (strlen(string) > size)
        string[size] = '\0';
}
```

The output is this:

```
Things should be as simple as possible, but not simpler.
Things should be as simple as possible
Let’s look at some more of the string.
    but not simpler.
```

The fit() function placed a '\0' character in the 39th element of the array, replacing a comma. The puts() function stops at the first null character and ignores the rest of the array. However, the rest of the array is still there, as shown by the following call:

```
puts(mesg + 8);
```