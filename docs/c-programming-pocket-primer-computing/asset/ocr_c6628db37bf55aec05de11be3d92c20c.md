Next, a `main()` function initializes the character arrays `source` and `destination` to hard-coded strings. A `printf()` statement displays the contents of `destination`, followed by an invocation of the `strcpy()` method that copies the contents of `source` to the variable `destination`, after which another `printf()` statement displays the new contents of `destination`. The output from launching `Listing 2.11` is here:

Before: The target string
After: The initial string

# # STRINGS AND STRING-RELATED FUNCTIONS

A string in C consists of a sequence of characters. Unlike languages such as Java, C does not provide a built-in string type. C uses a character array to represent a string, which is always terminated with `\0`.

`Listing 2.12` displays the contents of `CharArray.c` that illustrates how to initialize an array of characters.

# ### **LISTING 2.12: CharArray.c**

```
```c
#include <stdio.h>

char name[4];

int main()
{
  name[0] = 'a';
  name= 'b';
  name= 'c';
  name= '\0';

  return (0);
}
```
```