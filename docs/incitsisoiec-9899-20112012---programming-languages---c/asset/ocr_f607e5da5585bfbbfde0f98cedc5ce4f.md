FILE pointed to by streamptr will be set to a null pointer.

# Returns

The opens_s function returns zero if it opened the file. If it did not open the file or if there was a runtime-constraint violation, fopen_s returns a nonzero value.

# K.3.5.2.2 The freopen_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
erno_t freopen_s(FILE * restrict * restrict newstreamptr,
const char * restrict filename,
const char * restrict mode,
FILE * restrict stream);
```

# Runtime-constraints

None of newstreamptr, mode, and stream shall be a null pointer.

If there is a runtime-constraint violation, fopen_s neither attempts to close any file associated with stream nor opens to any file. Furthermore, if newstreamptr is not a null pointer, fopen_s sets *newstreamptr to the null pointer.

# Description

The fopen_s function opens the file whose name is the string pointed to by filename and associates the stream pointed to with stream. The mode argument has the same meaning as in the fopen_s function (including the mode's effect on exclusive access and file permissions).

If filename is a null pointer, the fopen_s function attempts to change the mode of the stream to that specified by mode, as if the name of the file currently associated with the stream has been used. It is implementation-defined which changes of mode are permitted (if any), and under what circumstances.

The fopen_s function first attempts to close any file that is associated with stream. Failure to close the file is ignored. The error and end-of-file indicators for the stream are cleared.

If the file was opened successfully, then the pointer to FILE pointed by newstreamptr will be set to the value of stream. Otherwise, the pointer to FILE pointed to by newstreamptr will be set to a null pointer.

# Returns

The fopen_s function returns zero if it opened the file. If it did not open the file or there was a runtime-constraint violation, fopen_s returns a nonzero value.