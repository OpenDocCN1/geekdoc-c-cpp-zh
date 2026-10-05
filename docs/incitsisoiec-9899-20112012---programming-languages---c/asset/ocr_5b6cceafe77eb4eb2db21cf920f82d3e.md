# 7.22.4.3 The at_quick_exit function

# Synopsis

```
#include <stdlib.h>
int at_quick_exit(void (*func)(void));
```

# Description

The at_quick_exit function registers the function pointed to by func, to be called without arguments should quick_exit be called.²298 It is unspecified whether a call to the at_quick_exit function that does not happen before the quick_exit function is called will succeed.

# Environmental limits

The implementation shall support the registration of at least 32 functions.

# Returns

The at_quick_exit function returns zero if the registration succeeds, nonzero if it fails.

Forward references: the quick_exit function (7.22.4.7).

# 7.22.4.4 The exit function

# Synopsis

```
#include <stdlib.h>
_Nturn void exit(int status);
```

# Description

The exit function causes program termination to occur. No functions registered by the at_quick_exit function are called. If a program calls the exit function more than once, or calls the quick_exit function in addition to the exit function, the behavior is undefined.

First, all functions registered by the atexit function are called, in the reverse order of their registration,²299 except that a function called after any previously registered functions had already been called at the time it was registered. During the call to any such function, a call to the longjmp function is made that would terminate the call to the registered function, the behavior is undefined.