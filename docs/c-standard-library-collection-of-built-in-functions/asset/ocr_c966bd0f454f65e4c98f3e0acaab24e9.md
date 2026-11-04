```
return(0);
}
```

Let us compile and run the above program to produce the following result:

```
tutorialspoint
compileonline
```

# int ungetc(int char, FILE *stream)

# Description

The C library function int ungetc(int char, FILE *stream) pushes the character char (an unsigned char) onto the specified stream so that the this is available for the next read operation.

# Declaration

Following is the declaration for ungetc() function.

```
int ungetc(int char, FILE *stream)
```

# Parameters

+   - char -- This is the character to be put back. This is passed as its int promotion.
+   - stream -- This is the pointer to a FILE object that identifies an input stream.

# Return Value

If successful, it returns the character that was pushed back otherwise, EOF is returned and the stream remains unchanged.

# Example

The following example shows the usage of ungetc() function.

```
#include <stdio.h>

int main ()
{
    FILE *fp;
    int c;
    char buffer [256];
```