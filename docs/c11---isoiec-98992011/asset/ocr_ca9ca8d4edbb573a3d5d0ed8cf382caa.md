# ISO/IEC 9899:2011 (E)

# K.3.5.3.2 The fscanf_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int fscanf_s(FILE * restrict stream,
            const char * restrict format, ...);
```

Runtime-constraints

Neither stream nor format be a null pointer. Any argument indirect though in order to store converted input should not be a null pointer.

If there is a runtime-constraint violation,392 the fscanf_s function does not attempt to perform further input, and it is unspecified to what extent fscanf_s performed input before discovering the runtime-constraint violation.

Description

The fscanf_s function is equivalent to fscanf except that the c, s, and [ conversion qualifiers are suppressed by an asterisk (*). The first of these arguments is the same as fscanf. Argument is immediately followed in the list by the second argument, which has size_t and gives the number of elements in the array pointed to by the first argument if the first argument is a scalar object, it is considered to be an array of one element.393

A matching failure occurs if the number of elements in a receiving object is insufficient to hold the converted input (including any trailing null character).

Returns

The fscanf_s function returns the value of EOF if an input failure occurs before any conversion or if there is a runtime-constraint violation. Otherwise, the

> 392) Because an implementation may treat any undefined behavior as a runtime-constraint violation, an implementation may treat any unsupported sequences in the string pointed to by format as a runtime-constraint violation.

> 393) If the format is known at translation time, an implementation may issue a diagnostic for any argument used to store the result from a c, s, or i conversion if that argument is not followed by an argument of type compatible with size_t. A limited amount of checking may be done if the format is not known at translation time. For example, an implementation may issue a diagnostic for each argument after format that has pointer to char, signed char, unsigned char, or void that is not followed by an argument of type compatible with size_t. The diagnostic could warn that unless the pointer is being used with a converter specifying the hh modifier, a length must follow the pointer argument. Another diagnostic could flag any non-pointer argument format that did not have a type compatible with

# Bounds-checking interfaces

# §K.3.5.3.2