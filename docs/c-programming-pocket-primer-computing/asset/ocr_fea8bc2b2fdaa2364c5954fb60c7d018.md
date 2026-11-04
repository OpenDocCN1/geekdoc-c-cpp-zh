Listing 2.12 declares a character array name that contains 4 elements (currently uninitialized). Next, a main() function initializes each element of the name array with the characters "a", "b", and "c". The final position is null-terminated with '\0'.

# The strcpy() Function

String constants consist of text enclosed in double quotes (“”), as shown here:

```
char str[] = "abcd";
```

Although other languages (such as Java) allow you to assign one string to another string, the following statement is illegal in C:

```
str = "another string"; // illegal in C
```

As you saw in an previous code sample, C provides the built-in strcpy() function to copy a string into a another location. Listing 2.13 displays the contents of CopyString.c that illustrates how to use the strcpy() function.

# LISTING 2.13: CopyString.c

```
```c
#include <string.h>

char str[4];

int main()
{
    strcpy(str, "abc");
    return (0);
}
```
```

Listing 2.13 is minimalistic: after declaring the character string str that consists of 4 elements, the main()