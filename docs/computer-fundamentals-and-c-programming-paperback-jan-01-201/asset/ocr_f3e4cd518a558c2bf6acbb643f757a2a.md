# 16.3.1  `malloc.c`: An Introductory Program

Before discussing the other features related to `malloc`, let’s consider Program 16.1 which invokes `malloc` three times to return pointers of three different data types. The program doesn’t use the `free` function to deallocate the blocks because it is not required here. The annotations make further discussions on this program unnecessary.

```
```c
/* malloc.c: Uses malloc without error checking. */

#include <stdio.h>
#include <stdlib.h>              /* Needed by malloc, calloc, realloc and free */

int main(void)
{
    short *p1;
    int *p2;
    float *p3;

    p1 = malloc(2);                       /* Non-portable; not recommended */
    p2 = malloc(sizeof(int));             /* The right way */
    p3 = malloc(sizeof(float));           /* Ditto */

    *p1 = 256; *p3 = 123.456;
    printf("*p1 = %hd\n", *p1);
    printf("*p2 = %d\n", *p2);           /* Prints uninitialized value */
    printf("*p3 = %f\n", *p3);

    exit(0);                              /* Frees all allocated blocks */
}
```
```

PROGRAM 16.1: `malloc.c`

```
```text
*p1 = 256
*p2 = 0
*p3 = 123.456001
```
```

> Uninitialized value; may not be 0

PROGRAM OUTPUT:  `malloc.c`

# 16.3.2  Error-Checking in `malloc`

The preceding program assumed that `malloc` always succeeds in allocating memory, which may not be the case. The function fails when there is not enough contiguous memory available for allocation in the heap. We must, therefore, check the pointer returned by `malloc` for NULL before using it. If `malloc` fails, it may not make sense to continue with program execution:

```
```c
long *p = malloc(sizeof(long));
if (p == NULL) {
    fputs("Memory allocation failed\n", stderr);
    exit(1);
}
```
```