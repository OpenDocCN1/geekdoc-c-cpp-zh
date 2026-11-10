```
```c
free(p);
p = NULL;
```
```

*p becomes a dangling pointer*  
*p is now a null pointer*

Because this memory—partially or totally—may have already been allocated, a subsequent attempt to access it using p could produce erroneous results or even cause the program to crash. Setting p to NULL solves the problem easily.

# 16.5.2 Memory Leaks

A different problem arises when p is made to point to another block without freeing the existing one. The previous block can’t then be freed (except by program termination) because its pointer is lost. A block without its pointer creates a *memory leak* which can turn serious when **malloc** is repeatedly used in a loop.

What happens when **malloc** is used in a function where the pointer to the block is declared as a local variable? Repeated invocation of the function will progressively deplete the heap unless arrangements are made to free the blocks outside the function. Figure 16.2 shows the improved version of the **my_strcpy** function (13.8.3) shown with the **main** section.

```
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

char *my_strcpy2(const char *src);

int main(void){
    char stg[80], *p;

    printf("Enter string: ");
    scanf("%[^\n]", stg);

    p = my_strcpy2(stg);
    printf("Copied string: %s\n", p);

    free(p);                         /* Frees memory created in the function */
    return 0;
}

char *my_strcpy2(const char *src)
{
    char *dest;
    short length;

    length = strlen(src) + 1;        /* One extra slot for NUL character */
    dest = malloc(length);

    strcpy(dest, src);
    return dest;                     /* Pointer to block now available in main */
}
```
```

**FIGURE 16.2**  Freeing Memory Created in a Function