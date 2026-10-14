explain about a preprocessor
include Files in the source program
explain and implement Macro definition and substitution
use parentheses in macro definitions

# 11.2 File Inclusion

A line of the form

```
#include <filename.h>
```

or

```
#include "filename.h"
```

causes the contents of the file filename.h to be read, parsed, and compiled at that point. (After filename.h is processed, compilation continues on the line following the #include line.) For example, suppose you got tired of retyping external function prototypes such as

```
extern int getline(char [], int);
```

at the top of each source file. You could instead place the prototype in a header file, perhaps getline.h, and then simply place

```
#include "getline.h"
```

at the top of each source file where you called getline. (You might not find it worthwhile to create an entire header file for a single function, but if you had a package of several related function, it might be very useful to place all of their declarations in one header file.) As we may have mentioned, that's exactly what the Standard header files such as