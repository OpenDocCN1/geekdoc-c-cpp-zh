# 6.4.4 Constants

Syntax

+   1 constant:
integer-constant
floating-constant
enenumeration-constant
character-constant

# Constraints

+   2 Each constant shall have a type and the value of a constant shall be in the range of representable values for its type.

# Semantics

+   3 Each constant has a type, determined by its form and value, as detailed later.

# 6.4.4.1 Integer constants

Syntax

+   1 integer-constant:
decimal-constant integer-suffix_{opt}
octal-constant integer-suffix_{opt}
hexadecimal-constant integer-suffix_{opt}

+   decimal-constant:
nonzero-digit
decimal-constant digit

+   octal-constant:
0
octal-constant octal-digit

+   hexadecimal-constant:
hexadecimal-prefix hexadecimal-digit
hexadecimal-constant hexadecimal-digit

+   hexadecimal-prefix: one of
0x 0X

+   nonzero-digit: one of
1 2 3 4 5 6 7 8 9

+   octal-digit: one of
0 1 2 3 4 5 6 7