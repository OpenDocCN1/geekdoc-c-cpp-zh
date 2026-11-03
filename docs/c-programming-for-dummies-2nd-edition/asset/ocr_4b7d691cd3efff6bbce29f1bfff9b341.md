# LISTING 20-3: Show Me the Garbage

```
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    unsigned char *junk;
    int x;

    /* allocate memory */
    junk = malloc(64);
    if( junk==NULL )
    {
        puts("Unable to allocate memory");
        exit(1);
    }

    /* output the buffer */
    for(x=0;x<64;x++)
    {
        printf("%02X ",*(junk+x));
        if( (x+1) % 8 == 0 )
            putchar('\n');
    }

    return(0);
}
```
```

**Exercise 20-6:** Copy the source code from Listing 20-3 in your editor. Save, build, and run.

The output from Exercise 20-6 shows the 64 bytes allocated as 2-digit hexadecimal values. The values are unpredictable. Memory could contain all zeros or any other values. The point is that the information is raw and uninitialized, and shouldn’t be trusted.

When you must ensure that memory is allocated and initialized, use the *calloc()* function instead of *malloc()*. Its format requires two arguments:

```
p = calloc(size,type);
```