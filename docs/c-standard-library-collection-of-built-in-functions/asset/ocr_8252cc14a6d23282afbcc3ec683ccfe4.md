| 41 | void perror(const char *str) |
|    | Prints a descriptive error message to stderr. First the string str is printed followed by a colon and then a space. |

# int fclose(FILE *stream)

# Description

The C library function int fclose(FILE *stream) closes the stream. All buffers are flushed.

# Declaration

Following is the declaration for fclose() function.

```
```c
int fclose(FILE *stream)
```
```

# Parameters

+   - stream -- This is the pointer to a FILE object that specifies the stream to be closed.

# Return Value

This method returns zero if the stream is successfully closed. On failure, EOF is returned.

# Example

The following example shows the usage of fclose() function.

```
```c
#include <stdio.h>

int main()
{
    FILE *fp;

    fp = fopen("file.txt", "w");

    fprintf(fp, "%s", "This is tutorialspoint.com");
    fclose(fp);

    return(0);
}
```
```