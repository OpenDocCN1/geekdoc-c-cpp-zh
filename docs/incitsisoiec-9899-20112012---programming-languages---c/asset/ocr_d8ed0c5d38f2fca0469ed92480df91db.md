The implementation shall behave as if no library function calls the getenv function.

The getenv function returns a pointer to a string associated with the matched list member. The string pointed to shall not be modified by the program, but may be overwritten by a subsequent call to the getenv function. If the specified name cannot be found, a null pointer is returned.

# 7.22.4.7 The quick_exit function

Synopsis

```
#include <stdlib.h>
Noreturn void quick_exit(int status);
```

Description

The quick_exit function causes normal program termination to occur. No functions registered by the atexit signal handlers registered by the signal function are called. If a program calls the quick_exit function more than once, or calls the exit function in addition to the quick_exit function, the behavior is undefined. If a signal is raised while the quick_exit function is executing, the behavior is undefined.

The quick_exit function first calls all functions registered by the at_quick_exit function, in the reverse order of their registration^{301)} except that a function is called after any previously registered functions that had already been called at the time it was registered. If, during the call to any such function, a call to the longjmp function is made that would terminate the call to the registered function, the behavior is undefined.

Then control is returned to the host environment by means of the function call _Exit(status).

Returns

The quick_exit function cannot return to its caller.

# 7.22.4.8 The system function

Synopsis

```
#include <stdlib.h>
int system(const char *string);
```

Description

If string is a null pointer, the system function determines whether the host environment has a command processor. If string is not a null pointer, the system-

> 301) Each function is called as many times as it was registered, and in the correct order with respect to other registered functions.