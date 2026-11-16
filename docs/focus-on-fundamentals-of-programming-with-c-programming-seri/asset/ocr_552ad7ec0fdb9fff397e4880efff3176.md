Sometimes a header file will include angle brackets, <>.

```
#include <stdio.h>
```

The angle brackets tell the C preprocessor that the included file is a C Standard Library header file (sometimes called a system file.) The standard input/output library file, stdio.h, contains the declarations (definitions) of all the standard names needed to do input and output in our programs. It must be included, for example, to use the printf() and scanf_s() standard input/output functions.

Note that the C Standard Library (the header and implementation files) come with the C compiler software. There are about 18 such libraries, including stdio.h for input/output, library files for string manipulation functions, math functions, character manipulation functions, etc. Note that you don't have to know where system header files are located, as the C pre-processor knows where to find them.

# User-Defined Header Files

User defined header files are header files that you create that may define information specific to your program.

Assume the following statement:

```
#include "myheader.h"
```

The double quotes, "", tell the C preprocessor that the included file is a user-defined header file as opposed to a C Standard Library header file. The C preprocessor assumes that the file myheader.h is located in the same directory where the program is compiled. If the user defined header file is not located in the same directory where you compile the program, then the information inside the double quotes must contain the path information for the user defined header file. Otherwise, the C preprocessor will not know where to find user defined header files.