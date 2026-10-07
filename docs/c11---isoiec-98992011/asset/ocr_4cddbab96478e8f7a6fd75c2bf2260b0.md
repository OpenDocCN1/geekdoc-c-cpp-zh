# ISO/IEC 9899:2011 (E)

universal character name specifying a short identifier of 00010000 or more considered 10 characters, and each extended source character is considered the same number of characters as the corresponding universal character name, if any)¹¹⁹

+   - 4095 external identifiers in one translation unit
- 511 identifiers with block scope declared in one block
- 4095 macros simultaneously defined in one preprocessing translation unit
- 127 parameters in one function call
- 127 arguments in one macro definition
- 127 arguments in one macro invocation
- 4095 characters in a logical source line
- 4095 characters in a string literal (after concatenation)
- 65535 bytes in an object (in a hosted environment only)
- 15 nesting levels for #included files

+   - 1023 case labels for a switch statement (excluding those for any nested switch statements)
- 1023 members in a single structure or union
- 1023 enumeration constants in a single enumeration
- 63 levels of nested structure or union definitions in a single struct-declaration-list

# 5.2.4.2 Numerical limits

An implementation is required to document all the limits specified in this clause, which are specified in the headers <limits.h> and <float.h>. Additional limits are specified in <stdint.h>

Forward references: integer types <stdint.h> (7.20).

# 5.2.4.1 Sizes of integer types <limits.h>

The values given below should be replaced by constant expressions suitable for use in #if preprocessing directives. Moreover, ever for CHAR_BIT and MB_LEN_MAX, the following should be replaced by expressions that have the same type as an expression that is an object of the type converted according to the integer promotions. Their implementation-defined values should be equal or greater in magnitude

19) See “future language directions” (6.11.3).