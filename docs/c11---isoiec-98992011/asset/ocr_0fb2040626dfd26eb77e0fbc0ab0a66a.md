# 7.26.4.2 The mtx_init function

Synopsis

```
#include <threads.h>
int mtx_init (mtx_t *mtx, int type);
```

Description

The mtx_init function creates a mutex object with properties indicated by type,
must have one of the six values:
mtx_plain for a non-recursive-mutex,
mtx_timed for a non-recursive mutex that supports timeout,
mtx_plain | mtx_recursive for a simple recursive mutex, or
mtx_timed | mtx_recursive for a recursive mutex that supports timeout.

If the mtx_init function succeeds, it sets the mutex pointed to by mtx to a value that
uniquely identifies the newly created mutex.

Returns

The mtx_init function returns thrd_success on success, or thrd_error if the
request could not be honored.

# 7.26.4.3 The mtx_lock function

Synopsis

```
#include <threads.h>
int mtx_lock (mtx_t *mtx);
```

Description

The mtx_lock function blocks until the mutex pointed to by mtx. If the mutex
is non-recursive, it shall not be locked by the calling thread. Prior calls to mtx_unlock
on the same mutex shall synchronize with this operation.

Returns

The mtx_lock function returns thrd_success on success, or thrd_error if the
request could not be honored.

# 7.26.4.4 The mtx_timedlock function

Synopsis

```
#include <threads.h>
int mtx_timedlock (mtx_t *restrict mtx,
const struct timespec *restrict ts);
```