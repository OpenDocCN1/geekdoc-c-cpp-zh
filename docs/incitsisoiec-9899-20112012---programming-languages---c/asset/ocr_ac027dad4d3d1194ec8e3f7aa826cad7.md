# 7.29.3.9 The putwchar function

Synopsis

```
#include <wchar.h>
wint_t putwchar(wchar_t c);
```

Description

The putwchar function is equivalent to putwc with the second argument stdout.

Returns

The putwchar function returns the character written, or WOEF.

# 7.29.3.10 The ungetwc

Synopsis

```
#include <stdio.h>
#include <wchar.h>
wint_t ungetwc(w_t c, FILE *stream);
```

Description

The ungetwc function pushes the wide character specified by c back onto the input stream pointed to by stream. Pushed-back characters will be returned by subsequent reads on that stream in the reverse order of their pushing. A successful intervening call (with the stream pointed to by stream) to a file positioning function (fseek, fsetpos, or rewind) discards any pushed-back wide characters for the stream. The external stream corresponding to the stream is unchanged.

One wide character of pushback is guaranteed, even if the call to the ungetwc follows just after a call to a formatted wide character function fwscanf, vfwscanf, vwcanf, or wscanf. If the ungetwc is called many times on the same stream without an intervening read or file positioning operation on that, the operation may fail.

If the value of c equals that of the macro WOEF, the operation fails and the input stream is unchanged.

A successful call to the ungetwc clears the end-of-file indicator for the stream. The value of the file position indicator for the stream after reading or discarding any pushed-back wide characters is the same as it was before the wide characters were pushed back. For a text or binary stream, the value of its file position indicator after a successful call to the ungetwc function is unspecified until all pushed-back characters are read or discarded.