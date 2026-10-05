# 3. Terms, definitions, and symbols

For the purposes of this document, the following terms and definitions apply. Other terms are defined where they appear in *italic* type or on the left side of a syntax rule. Terms explicitly defined in this International Standard are not to be presumed implicitly to similar terms defined elsewhere. Terms not defined in this International Standard are to be interpreted according to ISO/IEC 2382–1. Mathematical symbols are to be interpreted according to ISO 80000-2.

# 3.1 access

(execution-time action) to read or modify the value of an object

NOTE 1 Where only one of these actions is meant, “read” or “modify” is used.

NOTE 2 “Modify” only includes the case where the new value stored is the same as the previous value.

NOTE 3 Expressions that are not evaluated do not access objects.

# 3.2 alignment

requirement that objects of a particular type are located on storage boundaries with addresses that are particular multiples of a byte address

# 3.3 argument

actual argument
actual parameter (deprecated)

expression in the comma-separated list bounded by the parentheses in a function call expression, or a sequence of preprocessing tokens in the comma-separated list bounded by the parentheses in a function-like macro invocation

# 3.4 behavior

external appearance or action

# 3.4.1 implementation-defined behavior

unspecified behavior where each implementation documents how the choice is made

EXAMPLE An example of implementation-defined behavior is the propagation of the high-order bit when a signed integer is shifted right.

# 3.4.2 locale-specific behavior

behavior depends on local conventions of nationality, culture, and language that each implementation documents