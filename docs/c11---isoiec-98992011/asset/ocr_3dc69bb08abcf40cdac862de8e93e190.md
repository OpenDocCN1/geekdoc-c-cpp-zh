# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.29.3.6 The getwc function

Synopsis

```
#include <stdio.h>
#include <wchar.h>
wint_t getwc(FILE *stream);
```

Description

The getwc function is equivalent to fgetwc, except if it is implemented as a macro, it may evaluate stream more than once, so the argument should never be an expression with side effects.

Returns

The getwc function returns the next character from the input stream pointed to by stream, or WOEOF.

# 7.29.3.7 The getwchar function

Synopsis

```
#include <wchar.h>
wint_t getwchar(void);
```

Description

The getwchar function is equivalent to getwc with the argument stdin.

Returns

The getwchar function returns the next character from the input stream pointed to by stdin, or WOEOF.

# 7.29.3.8 The putwc function

Synopsis

```
#include <stdio.h>
#include <wchar.h>
wint_t putwc(wchar_t c, FILE *stream);
```

Description

The putwc function is equivalent to fputwc, except if it is implemented as a macro, it may evaluate stream more than once, so that argument should never be an expression with side effects.

Returns

The putwc function returns the wide character written, or WOEOF.