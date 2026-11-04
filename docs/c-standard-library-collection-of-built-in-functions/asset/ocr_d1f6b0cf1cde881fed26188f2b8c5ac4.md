```
/* Print 5 random numbers from 0 to 49 */
for( i = 0 ; i < n ; i++ ) {
    printf("%d\n", rand() % 50);
}

return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
38
45
29
29
47
```

# void srand(unsigned int seed)

# Description

The C library function void srand(unsigned int seed) seeds the random number generator used by the function rand.

# Declaration

Following is the declaration for srand() function.

```
void srand(unsigned int seed)
```

# Parameters

+   - seed -- This is an integer value to be used as seed by the pseudo-random number generator algorithm.

# Return Value

This function does not return any value.

# Example

The following example shows the usage of srand() function.

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
```