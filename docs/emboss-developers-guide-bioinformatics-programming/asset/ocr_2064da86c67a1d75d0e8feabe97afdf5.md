# ## 5.1.2.2 Other AJAX types

For convenience ajdefine.h also defines a few datatypes given in the table below:

| Type | Description |
| :--- | :--- |
| AjBool | Boolean |
| AjStatus | Status code |
| AjIntArray | Integer array (int*) |
| AjFloatArray | Float array (float*) |

**AjBool** Used to store true (ajTrue, AJTRUE) and false (ajFalse, AJFALSE) values. On output, the conversion code %b writes Y or N while conversion code %B writes Yes or No.
There is also a macro for testing boolean values:

```
```c
#define AJBOOL(b) (b ? "TRUE" : "FALSE")
```
```

**AjStatus** Intended as a general return code for functions, but currently unused because AjBool is enough. Has a constant value to indicate success (ajStatusOK), message (ajStatusInfo), warning (ajStatusWarn), error (ajStatusError) and fatal error (ajStatusFatal).

**AjIntArray** A simple C-type array of integers:

```
```c
typedef int* AjIntArray;
```
```

**AjFloatArray** A simple C-type array of floats:

```
```c
typedef float* AjFloatArray;
```
```

To use these AJAX datatypes you must include the files ajdefine.h and ajarch.h in your code. All applications must include at the start of the code the preprocessor directive #include "emboss.h" (see Chapter 2, Your first EMBOSS application).
emboss.h is the master include file and imports the entire EMBOSS interface: it includes all the header files in the AJAX and NUCLEUS C programming libraries making all the code available to you. If you inspect the file you'll see that ajax.h is included:

```
```c
% more nucleus/emboss.h

#ifndef emboss_h
#define emboss_h

#include "ajax.h"
#include "ajgraph.h"
.
.
```
```