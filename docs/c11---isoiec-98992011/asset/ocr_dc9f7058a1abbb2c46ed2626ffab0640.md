© ISO/IEC 2011 – All rights reserved

ISO/IEC 9899:2011 (E)

# 7.21.5.4 The freopen function

Synopsis

```
#include <stdio.h>
FILE *freopen(const char * restrict filename,
const char * restrict mode,
FILE * restrict stream);
```

Description

The freopen function opens the file whose name is the string pointed to by filename and associates the stream pointed to by stream with it. The mode argument is used just as in the freopen function.²

If filename is a null pointer, the freopen function changes the mode of the stream to that specified by mode, as if the name of the file currently associated with the stream had been used. It is implementation-defined which of modes are permitted (if any), and under what circumstances

The freopen function first attempts to close any file that is associated with the specified stream. Failure to close the file is ignored. The error and end-of-file indicators for the stream are cleared.

Returns

The freopen function returns a null pointer if the open operation fails. Otherwise, freopen returns the value of stream.

# 7.21.5.5 The setbuf function

Synopsis

```
#include <stdio.h>
void setbuf(FILE * restrict stream,
char * restrict buf);
```

Description

Except that it returns no value, the setbuf function is equivalent to the setbuf function invoked with the values _IOFBF for mode and BUFSZ for size, or (if buf is a null pointer), with the value _IONBF for mode.

> ²The primary use of the freopen function is to change the file associated with a standard text stream (stderr, stdin, and stdout), as these identifiers are not modifiable values to which the value returned by the freopen function may be assigned.

§7.21.5.5

Library

307