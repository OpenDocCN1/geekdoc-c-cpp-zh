# Declaration

Following is the declaration for exit() function.

```
```c
void exit(int status)
```
```

# Parameters

+   - **status** -- This is the status value returned to the parent process.

# Return Value

This function does not return any value.

# Example

The following example shows the usage of exit() function.

```
```c
#include <stdio.h>
#include <stdlib.h>

int main ()
{
    printf("Start of the program....\n");
    printf("Exiting the program....\n");
    exit(0);
    printf("End of the program....\n");
    return(0);
}
```
```

Let us compile and run the above program that will produce the following result:

```
Start of the program....
Exiting the program....
```

# char *getenv(const char *name)

# Description

The C library function char *getenv(const char *name) searches for the environment string pointed to, by name and returns the associated value to the string.