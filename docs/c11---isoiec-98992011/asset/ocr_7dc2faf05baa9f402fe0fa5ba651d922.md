ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.26.6 Thread-specific storage functions

# 7.26.6.1 The tss_create storage function

Synopsis

```
#include <threads.h>
 tss_create(tss_t *key, tss_dtor_t dtor);
```

Description

The tss_create function creates a thread-specific storage pointer with destructor dtor, which may be null.

Returns

If the tss_create function is successful, it sets the thread-specific storage pointed to by key to a value that uniquely identifies the newly created pointer and returns thrd_success; otherwise, thrd_error is returned and the thread-specific storage pointed to by key is set to an undefined value.

# 7.26.6.2 The tss_delete function

Synopsis

```
#include <threads.h>
void tss_delete(tss_t key);
```

Description

The tss_delete function releases any resources used by the thread-specific storage identified by key.

Returns

The tss_delete function returns no value.

# 7.26.6.3 The tss_get function

Synopsis

```
#include <threads.h>
void *tss_get(tss_t key);
```

Description

The tss_get function returns the value for the current thread held in the thread-specific storage identified by key.

Returns

The tss_get function returns the value for the current thread if successful, or zero if unsuccessful.