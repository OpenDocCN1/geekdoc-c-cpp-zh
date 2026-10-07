ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# Returns

+   3 The thrd_detach function returns thrd_success on success or thrd_error if the request could not be honored.

# 7.26.5.4 The thrd_equal function

# Synopsis

```
#include <threads.h>
int thrd_equal(thrd_t thr0, thrd_t thr1);
```

# Description

+   2 The thrd_equal function will determine whether the thread identified by thr0 refers to the thread identified by thr1.

# Returns

+   3 The thrd_equal function returns zero if the thread thr0 and the thread thr1 refer to different threads. Otherwise the thrd_equal function returns a nonzero value.

# 7.26.5.5 The thrd_exit function

# Synopsis

```
#include <threads.h>
_Noreturn void thrd_exit(int res);
```

# Description

+   2 The thrd_exit function terminates execution of the calling thread and sets its result code to res.

+   3 The program terminates normally after the last thread has been terminated. The behavior shall be as if the program called the exit function with the status EXIT_SUCCESS at termination time.

# Returns

+   4 The thrd_exit function returns no value.

# 7.26.5.6 The thrd_join function

# Synopsis

```
#include <threads.h>
int thrd_join(thrd_t thr, int *res);
```

# Description

+   2 The thrd_join joins the thread identified by thr by blocking until the thread has terminated. If the parameter res is not a pointer, it stores the thread's result code in the integer pointed to by res. Termination of the