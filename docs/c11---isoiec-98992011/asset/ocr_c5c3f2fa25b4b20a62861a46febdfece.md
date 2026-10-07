# ISO/IEC 9899:2011 (E)

# Description

The **isgreaterequal** macro determines whether its first argument is greater than equal to its second. The value of **isgreaterequal(x, y)** is always equal to **(x) >= (y)**; however, unlike **(x) >= (y)**, **isgreaterequal(x, y)** does not raise the “invalid” floating-point exception when **x** and **y** are unordered.

# Returns

The **isgreaterequal** macro returns the value of **(x) >= (y).**

# 7.12.14.3 The isless macro

# Synopsis

```
#include <math.h>
int isless(real-floating x, real-floating y);
```

# Description

The **isless** macro determines whether its first argument is less than its second argument. The value of **isless(x, y)** is always equal to **(x) < (y)**; however, unlike **(x) < (y)**, **isless(x, y)** does not raise the “invalid” floating-point exception when **x** and **y** are unordered.

# Returns

The **isless** macro returns the value of **(x) < (y).**

# 7.12.14.4 The islesqual macro

# Synopsis

```
#include <math.h>
int islesqual(real-floating x, real-floating y);
```

# Description

The **islesqual** macro determines whether its first argument is less or equal to its second argument. The value of **islesqual(x, y)** is always equal to **(x) <= (y)**; however, unlike **(x) <= (y)**, **islesqual(x, y)** does not raise the “invalid” floating-point exception when **x** and **y** are unordered.

# Returns

The **islesqual** macro returns the value of **(x) <= (y).**