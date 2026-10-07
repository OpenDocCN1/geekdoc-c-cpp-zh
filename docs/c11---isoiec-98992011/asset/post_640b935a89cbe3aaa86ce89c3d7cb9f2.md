
© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

## K.2 Scope

- 1 This annex specifies a series of optional extensions that can be useful in the mitigation of security vulnerabilities in programs, and comprise new functions, macros, and types declared or defined in existing standard headers.
- 2 An implementation that defines __STDC_LIB_EXT1__ shall conform to the specifications in this annex.^{380}
- 3 Subclause K.3 should be read as if it were merged into the parallel structure of named subclauses of clause 7.

## K.3 Library

### K.3.1 Standard headers

- 1 The functions, macros, and types declared or defined in K.3 and its subclauses are declared or defined by their respective headers if __STDC_WANT_LIB_EXT1__ is defined as a macro which expands to the integer constant 0 in the source file where the appropriate header is first included.

- 2 The functions, macros, and types declared or defined in K.3 and its subclauses are declared or defined by their respective headers if __STDC_WANT_LIB_EXT1__ is defined as a macro which expands to the integer constant 1 at the point in the source file where the appropriate header is first included.^{381}

- 3 It is implementation-defined whether functions, macros, and types declared in K.3 and its subclauses are declared or defined by their respective headers if __STDC_WANT_LIB_EXT1__ is not defined as a macro at the point in the source file where the appropriate header is first included.^{382}

- 4 Within a preprocessing translation unit, __STDC_WANT_LIB_EXT1__ shall be defined identically for all inclusions of headers from subclause K.3. If __STDC_WANT_LIB_EXT1__ is defined differently for such inclusion, the implementation should issue a diagnostic as if a preprocessor error were used.

380 Implementations that do not define __STDC_LIB_EXT1__ are not required to conform to these specifications.

381 Future revisions of this International Standard may define meanings for other values of __STDC_WANT_LIB_EXT1__

382 Subclause 7.1 reserves certain names and patterns of names that an implementation may use in headers. All headers are not reserved, and a conforming implementation is not permitted to use them; While some of the names defined in K.3 and its subclauses are reserved, others are. If an unreserved name is defined in a header when __STDC_WANT_LIB_EXT1__ is defined as 0, the implementation is not conforming.

### K.3.1.1 Bounds-checking interfaces 583

### K.3.1.2 Reserved identifiers

- 1 Each name in any of the following subclauses is reserved for use as specified if it is defined by any of its associated headers when included; unless explicitly stated otherwise (see 7.1.4).

- 2 All identifiers with external linkage in any of the following subclauses are reserved for use as identifiers with external linkage if any of them are used by the program. None of them are reserved if none of them are used.

- 3 Each identifier with file scope listed in any of the following subclauses is reserved for use as a macro and an identifier with file scope in the same name as it is defined by any of its associated headers when included.

### K.3.1.3 Use of errno

- 1 An implementation may use errno for the functions defined in this annex, but is not required to.

### K.3.1.4 Runtime-constraint violations

- 1 Most functions in this annex include as part of their specification a list of runtime-constraints. These runtime-constraints are requirements on the program.³383)

- 2 Implementations shall verify that the runtime-constraints for a function are not violated by the program. If a runtime-constraint is violated, the implementation shall call the currently registered runtime-handler (see set_constraint_handler in <stdlib.h>). Multiple runtime-constraint violations in the same call to a library function result in only one call to the runtime handler. It is unspecified which runtime-constraint violations cause the handler to be called.

- 3 If the runtime-constraints for a function states an action to be performed when a runtime-constraint occurs, the function shall perform that action before calling the handler. If runtime-constraints lists actions that are prohibited when a runtime-constraint occurs, such actions are prohibited from the function before calling the handler and after the handler returns.

- 4 The runtime-constraint handler may not return. If the handler returns, the library function whose constraint was violated shall return some indication of failure as given by the returns section in the function's specification. Although runtime-constraints replace many cases of undefined behavior, undefined behavior still exists in this annex. implementations are free to detect any case of undefined behavior and treat it as a runtime-violation by calling the runtime-handler. This comes directly from the definition of undefined behavior.

© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

### K.3.2 Errors <errno.h>

- 1 The header <errno.h> defines a type.
- 2 The type is:
```
errno_t
```
which is type int.³384)

### K.3.3 Common definitions <stddef.h>

- 1 The header <stddef.h> defines a type.
- 2 The type is
```
size_t
```
which is type size_t.³385)

### K.3.4 Integer types <stdint.h>

- 1 The header <stdint.h> defines a macro.
- 2 The macro is
```
RSIZE_MAX
```
expands to a value ³386 of type size_t. Functions that have parameters of rsize_t consider it a runtime-constraint violation if the values of those parameters are greater than RSIZE_MAX

- 3 Extremely large objects frequently a sign that an object's size was calculated incorrectly. For example, negative numbers appear as very large numbers when converted to an unsigned type like size_t. Also, some implementations do not support objects as the maximum value that can be represented by type size_t.
-4 For these reasons, it is beneficial to restrict the range of object sizes to detect programming errors. For implementations targeting machines with large address spaces, it is recommended that RSIZE_MAX be defined as the smaller of the largest object supported or (SIZE_MAX >> 1), even if this is smaller than the size of some legitimate, yet large objects. implementations targeting machines with small address spaces may wish to define RSIZE_MAX as SIZE_MAX, which means that

384 As a matter of programming style, errno may be used as a type of something that only deals with the values that might be in errno. For example, a function which returns the value of errno be declared as having the return type errno_t.
385 See the description of the RSIZE_MAX macro in <stdint.h>.
386 The macro RSIZE_MAX need not expand to a constant expression.

### K.3.4 Bounds-checking interfaces is no object size that is considered a runtime-constraint violation.

### K.3.5 Input/output <stdio.h>

- 1 Header <stdio.h> defines several macros and two types.
- 2 The macros are
```
L_tmpnam_s
```
which expands to an integer constant that is the size needed for an array of char large enough to hold a temporary file name string generated by the tmpnam_s function;

```
TMP_MAX_S
```
which expands to an integer constant that is the maximum number of unique file names that can be generated by the tmpnam_s function.

- 3 The types are
```
errno_t
```
which is type int; and

```
rsize_t
```
which is the type size_t.

### K.3.5.1 Operations on files

### K.3.5.1.1 The tmpfile_s function

Synopsis

```
1 #define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
errno_t tmpfile_s(FILE * restrict * restrict streamptr);
```

Runtime-constraints

- 2 streamptr shall not be a null pointer.
- 3 If there is a runtime-constraint violation, tmpfile_s does not attempt to create a file.

Description

- 4 The tmpfile_s function creates a temporary binary file that differs from any other existing file and will automatically be removed when it is closed or at program termination. The program terminates normally, whether an open temporary file is removed implementation-defined. The file is opened for update with "wb+ mode meaning that mode has in the fopen function (including the effect of exclusive access and file permissions).
