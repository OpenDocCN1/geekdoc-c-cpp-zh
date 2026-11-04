# Parameters

+   - str -- This is the pointer to an array of chars where the proposed temp name will be stored as a C string.

# Return Value

+   - Return value is a pointer to the C string containing the proposed name for a temporary file. If str was a null pointer, this points to an internal buffer that will be overwritten the next time this function is called.
+   - If str was not a null pointer, str is returned. If the function fails to create a suitable filename, it returns a null pointer.

# Example

The following example shows the usage of tmpnam() function.

```
#include <stdio.h>

int main()
{
    char buffer[_L_tmpnam];
    char *ptr;

    tmpnam(buffer);
    printf("Temporary name 1: %s\n", buffer);

    ptr = tmpnam(NULL);
    printf("Temporary name 2: %s\n", ptr);

    return(0);
}
```

Let us compile and run the above program to produce the following result:

```
Temporary name 1: /tmp/filebaalTb
Temporary name 2: /tmp/filedCIbb0
```

# int fprintf(FILE *stream, const char *format, ...)

# Description