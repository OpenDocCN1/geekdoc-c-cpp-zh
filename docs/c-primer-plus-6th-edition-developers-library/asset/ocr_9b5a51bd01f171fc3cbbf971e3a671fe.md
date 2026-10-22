| Prototype | Description |
|---|---|
| int vsnprintf(char * restrict, size_t n); const char * restrict, va_list); | Like snprintf(), except uses a single list- argument of type va_list initialized by va_start instead of a variable argument list |
| int vsprintf(char * restrict, const char * restrict, va_list); | Like sprintf(), except uses a single list-argument of type va_list initialized by va_start instead of a variable argument list |
| int vscanf(const char * restrict, va list); | Like scanf(), except uses a single list-argument of type va_list initialized by va_start instead of a variable argument list |
| int vsscanf(const char * restrict,* restrict, va_list); | Like sscanf(), except const char uses a single list-argument of type va_list initialized by va_start instead of a variable argument list |

# General Utilities: stdlib.h

The ANSI C standard library includes a variety of utility functions defined in stdlib.h. The header file defines the types shown in Table RS.V.34.

# Table RS.V.34 Types Declared in stdlib.h

| Type | Description |
|---|---|
| size_t | The integer type returned by the sizeof operator. |
| wchar_t | The integer type used to represent wide characters. |
| div_t | The structure type returned by div(); it has a quot and a rem member, both of type int. |
| ldiv_t | The structure type returned by ldiv(); it has a quot and a rem member, both of type long. |
| lldiv_t | The structure type returned by lldiv(); it has a quot and a rem member, both of type long long. (C99) |

The header file defines the constants listed in Table RS.V.35.