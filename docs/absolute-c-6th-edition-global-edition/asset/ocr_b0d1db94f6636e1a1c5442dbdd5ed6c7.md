# Old and New Header Files

In this book, we have used the header files for standard libraries that are part of the most recent ANSI/ISO C++ standard. If you have an older compiler, you may need to use the older header files. In the following, we list the new header file names that we have used in this book along with their corresponding older header file names. If the new header files do not work for you, then try the older header file names instead.

If your compiler requires the older header file names, then it also may not accommodate namespaces. In that case, you may have to eliminate all references to namespaces. If you have a compiler that requires the older header file names and/or does not support namespaces, you should consider obtaining a new compiler that comes closer to meeting the new standard.

| NEW HEADER FILE | CORRESPONDING OLDER HEADER FILE |
|---|---|
| cassert | assert.h |
| cctype | ctype.h |
| cstddef | stddef.h |
| cstdlib | stdlib.h |
| cmath | math.h |
| cstring | string.h |
| fstream | fstream.h |
| iomanip | iomanip.h |
| iostream | iostream.h |
| string | string or no corresponding library |