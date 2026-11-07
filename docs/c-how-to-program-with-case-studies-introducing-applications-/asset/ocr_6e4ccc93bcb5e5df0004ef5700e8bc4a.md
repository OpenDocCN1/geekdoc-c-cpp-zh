a multicore system can run those threads in parallel—that is, simultaneously. Section C.9 first demonstrates two long-running calculations performed in sequence. Then we separate those calculations into two threads to demonstrate the significant performance improvement of running the threads in parallel on multiple cores.

# C.2 Headers Added in C99

The following table lists the standard-library headers added in C99—these remain available in C11/C18. We’ll discuss the new C11/C18 headers in Section C.8.1.

| Header | Explanation |
|---|---|
| `<complex.h>` | Contains support for complex numbers (see Section C.5). |
| `<fenv.h>` | Provides information about the C implementation’s floating-point environment and capabilities. |
| `<inttypes.h>` | Defines portable integral types and provides format specifiers for them. |
| `<stdbool.h>` | Contains macros defining bool, true and false, used for boolean variables (see Section C.4). |
| `<stdint.h>` | Defines extended integer types and related macros. |
| `<tgmath.h>` | Provides type-generic macros that allow functions from <math.h> to be used with a variety of parameter types (see Section C.7). |

# C.3 Designated Initializers and Compound Literals

[This section can be read after Section 10.3.] Designated initializers allow you to initialize array elements by subscript and union or struct members by name. Figure C.1 shows that we can use designated initializers to initialize specific array elements.

```
```c
// fig_C01.c
// Initializing specific array elements with designated initializers.
#include <stdio.h>

int main(void) {
    int values[5] = {
        [0] = 123, // initialize element 0
        [4] = 456  // initialize element 4
    }; // semicolon is required

    // output array contents
    printf("values: ");

    for (size_t i = 0; i < 5; ++i) {
        printf("%d ", values[i]);
    }
}
```
```

Fig. C.1 | Initializing specific array elements with designated initializers. (Part 1 of 2.)