sscanf reads numeric values and words out of a formatted string allowing you to parse text from elsewhere. Remember that all the arguments to sscanf must be pointers

![](bbox=[0.038, 0.169, 0.912, 0.413])

# How long is a (piece of) string?

One final useful string function is strlen ('for string length'); as the name suggests, this tells you how many characters there are in a string, counting from the start to the terminating zero character.

```
#include <stdio.h>
#include <string.h>

void main (void)
{
    char str1[10] = "first"

    printf("The length of the string '%s' is %d\n", str1, strlen(str1));
}
```

All the operations we've looked at here are possible by manually manipulating pointers the string library just makes them easier and will make your code shorter. If you find yourself moving pointers around strings in a program, always check the string library to make sure you're not reinventing the wheel!