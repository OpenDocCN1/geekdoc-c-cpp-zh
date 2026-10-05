# 7.18 Boolean type and values <stdbool.h>

The header <stdbool.h> defines four macros.

The macro
```nbool
```
ands to _Bool.

The remaining three macros are suitable for use in #if preprocessing directives. They are
```true
```
which expands to the integer constant 1,
```false
```
which expands to the integer constant 0, and
```__bool_true_false_are_defined
```
which expands to the integer constant 1.

Notwithstanding the provisions of 7.1.3, a program may undefine and perhaps then redefine the macros bool, true, and false.²59)