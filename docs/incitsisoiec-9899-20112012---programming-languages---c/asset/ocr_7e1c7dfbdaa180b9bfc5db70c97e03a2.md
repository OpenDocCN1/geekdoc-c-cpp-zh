The fscanf macros for signed integers:

| SCdN | SCNDLEAST | SCNDFAST | SCNDMAX | SCNDPTR |
| SCiN | SCNILEAST | SCNIFAST | SCNIMAX | SCNIPTR |

The fscanf macros for unsigned integers:

| SCNoN | SCNoLEAST | SCNoFAST | SCNoMAX | SCNoPTR |
| SCuNx | SCNuLEAST | SCNuFAST | SCNuMAX | SCuNPTR |

For each type the implementation provides in <stdint.h>, the corresponding fprintf shall be defined and the corresponding fscanf macros shall be defined unless the implementation does not have a suitable fscanf length modifier for the type.

```
EXAMPLE
```c
#include <inttypes.h>
#include <wchar.h>
int main(void) {
    uintmax_t i = UINTMAX_MAX; // this type always exists
    printf("The largest integer value is %020\n", PRIxmax "\n", i);
    return 0;
}
``````
```

# 7.8.2 Functions for greatest-width integer types

# 7.8.2.1 The imabs function

Synopsis

```
#include <inttypes.h>
intmax_t imabs(intmax_t j);
```

Description

The imabs function computes the absolute value of an integer j. If the result cannot be represented, the behavior is undefined.221)

Returns

The imabs function returns the absolute value.

> 221) The absolute value of the most negative number cannot be represented in two's complement.