The calculation of answer will correctly evaluate to 100000000. However, the assignment of the long result to a short produces a value that is too large to be held in the short and the short will therefore hold an incorrect value.

Note that the integer ranges in the tables above aren't mandated by the C standard and may vary from one compiler to another. One way to determine the range of integer types for a particular implementation is to check the <limits.h> header file, which is part of the standard C library. This header defines macros that represent the smallest and largest values of each integer type.

```
// limit.c
#include <stdio.h>
#include <limits.h>

int main (void) {
    printf("Data-Type\t\t\t\t\t\t\t\t Min Value\t\t\t\t Max Value\n");
    printf("Short Int\t\t\t\t\t\t\t %ld\t\t\t\t\t%20d\n", sizeof(short), SHRT_MIN, SHRT_MAX);
    printf("Unsigned Short Int\t\t\t\t %ld\t\t\t\t\t%20u\n", sizeof(unsigned short), 0, USHRT_MAX);
    printf("Int\t\t\t\t\t\t\t\t %ld\t\t\t\t\t%20d\n", sizeof(int), INT_MIN, INT_MAX);
    printf("Unsigned Int\t\t\t\t\t\t %ld\t\t\t\t\t%20u\n", sizeof(unsigned int), 0, UINT_MAX);
    printf("Long Int\t\t\t\t\t\t\t %ld\t\t\t\t\t%20ld\n", sizeof(long int), LONG_MIN, LONG_MAX);
    printf("Unsigned Long Int\t\t\t\t %ld\t\t\t\t\t%20lu\n", sizeof(unsigned long int), 0, ULONG_MAX);
    printf("Long Long Int\t\t\t\t\t %ld\t\t\t\t\t%20lld\n", sizeof(long long int), LLONG_MIN, LLONG_MAX);
    printf("Unsigned Long Long Int\t\t\t %ld\t\t\t\t\t%20llu\n", sizeof(unsigned long long int), 0, ULLONG_MAX);

    return 0;
}
```