| "r+" | Opens a file to update both reading and writing. The file must exist. |
| "w+" | Creates an empty file for both reading and writing. |
| "a+" | Opens a file for reading and appending. |

# Return Value

This function returns a FILE pointer. Otherwise, NULL is returned and the global variable errno is set to indicate the error.

# Example

The following example shows the usage of fopen() function.

```
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    FILE * fp;

    fp = fopen ("file.txt", "w+");
    fprintf(fp, "%s %s %s %d", "We", "are", "in", 2012);

    fclose(fp);

    return(0);
}
```
```

Let us compile and run the above program that will create a file file.txt with the following content:

We are in 2012

Now let us see the content of the above file using the following program:

```
```c
#include <stdio.h>

int main ()
{
    FILE *fp;
```
```