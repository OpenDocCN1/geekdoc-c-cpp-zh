© ISO/IEC 2011 – All rights reserved

ISO/IEC 9899:2011 (E)

+   - Whether two string literals in subexpressions are evaluated (6.4.5).

+   - The order in which subexpressions are evaluated and the order in which side effects take place, except as specified for the function-call (), &&, ||, ?, and comma operators (6.5).

+   - The order in which the function designator, arguments, and subexpressions within the arguments are evaluated in a function call (6.5.2.2).

+   - The order of side effects among compound literal initialization expressions (6.5.2.5).

+   - The order in which the operands of an assignment operator are evaluated (6.5.16).

+   - The alignment of the addressable storage unit allocated to hold a bitfield (6.7.2.1).

+   - Whether a call to an inline function uses the inline definition or the external definition of the function (6.7.4).

+   - Whether or not a size expression is evaluated when it is part of the operand of `sizeof` operator and changing the value of the size expression would not affect the result of the operator (6.7.2).

+   - The order in which any side effects occur among the initialization list expressions in an initializer (6.7.9).

+   - The layout of storage for function parameters (6.9.1).

+   - When a fully expanded macro replacement list contains a function-like macro name as its first preprocessing token and the next preprocessing token from the source file is a (, the fully expanded replacement of the next macro ends with the name of the first macro and the next preprocessing token from the source file is a ), whether that is considered a nested replacement (6.10.3).

+   - The order in which # and ## operations are evaluated during macro substitution (6.10.2, 6.10.3).

+   - The state of the floating-point status flags when execution passes from a part of the program with `FENV_ACCESS` “off” to a part translated with `FENV_ACCESS` “on” (7.6.1).

+   - The order in which `feraisexcept` accepts floating-point exceptions, except as in F.8 (7.6.2.3).

+   - Whether `math_errhandling` is a macro or an identifier with external linkage (7.12).

+   - The results of the `frexp` function when the specified value is not a floating-point number (7.12.6.4).