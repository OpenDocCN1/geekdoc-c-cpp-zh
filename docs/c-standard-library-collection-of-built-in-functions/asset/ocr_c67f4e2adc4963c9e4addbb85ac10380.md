Let us compile and run the above program that will produce the following result because we are trying to open a file which does not exist:

```
Error: No such file or directory
```

# size_t strlen(const char *str)

# Description

The C library function size_t strlen(const char *str) computes the length of the string str up to, but not including the terminating null character.

# Declaration

Following is the declaration for strlen() function.

```
size_t strlen(const char *str)
```

# Parameters

+   - str -- This is the string whose length is to be found.

# Return Value

This function returns the length of string.

# Example

The following example shows the usage of strlen() function.

```
#include <stdio.h>
#include <string.h>

int main ()
{
    char str[50];
    int len;

    strcpy(str, "This is tutorialspoint.com");

    len = strlen(str);
    printf("Length of |%s| is |%d|\n", str, len);

    return(0);
}
```

Let us compile and run the above program that will produce the following result: