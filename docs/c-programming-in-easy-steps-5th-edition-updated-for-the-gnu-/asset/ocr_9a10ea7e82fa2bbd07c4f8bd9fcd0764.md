use the smallest amount of memory possible. For example, where a variable will only ever contain positive integer values below 65,535 it is preferable to use an unsigned short int variable that reserves just 2 bytes of memory rather than a long int variable that reserves 4 bytes of memory.

![](bbox=[0.35, 0.21, 0.65, 0.29])

Constants are always named entirely in uppercase to distinguish them from variables.

![](bbox=[0.35, 0.4, 0.65, 0.48])

The memory space allocated to an int variable of unspecified size is system-dependent but will often be treated as a long int by default.

1. Begin a new program with a preprocessor instruction to include the standard input/output functions and constants

```
```c
#include <stdio.h>
#include <limits.h>
```
```

![](bbox=[0.35, 0.74, 0.65, 0.82])

2. Add a main function that contains statements to output the size and range of the short int data type

```
```c
int main()
{
    printf("short int... size: %d bytes\n", sizeof(short int));
    printf("%d to %d\n", SHRT_MAX, SHRT_MIN);
}
```
```

3. Next, insert statements to output the size and range of the long int data type