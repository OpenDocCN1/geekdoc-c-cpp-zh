# 7.26.6.4 The tss_set function

Synopsis

```
#include <threads.h>
int tss_set(tss_t key, void *val);
```

Description

+   1 The tss_set function sets the value for the current thread held in the thread-specific storage identified by key to val.

2 Returns

+   3 The tss_set function returns thrd_success on success or thrd_error if the request could not be honored.

# §7.26.6.4