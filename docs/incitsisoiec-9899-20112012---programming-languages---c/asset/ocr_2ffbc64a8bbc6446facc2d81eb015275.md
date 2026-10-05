An attempt is made to copy an object to an overlapping object by use of a library function, other than as explicitly allowed (e.g., memmove) (clause 7).

A file with the same name as one of the standard headers, not provided as part of the implementation, is placed in any of the standard places that are searched for included source files (7.1.2).

A header is included within an external declaration or definition (7.1.2).

A function, object, type, or macro that is specified as being declared or defined by some standard header is used before any header that declares or defines it is included (7.1.2).

A standard header is included while a macro is defined with the same name as a keyword (7.1.2).

The program attempts to declare a library function itself, rather than via a standard header, but the declaration does not have external linkage (7.1.2).

The program declares or defines a reserved identifier, other than as allowed by 7.1.4 (7.1.3).

The program removes the definition of a macro whose name begins with underscore and either an uppercase letter or another underscore (7.1.3).

An argument to a library function has an invalid value or a type not expected by a function with variable number of arguments (7.1.4).

The pointer passed to a library function array parameter does not have a value such that all address computations and object accesses are valid (7.1.4).

The macro definition of assert is suppressed in order to access any actual function (7.2).

The argument to a macro does not have a scalar type (7.2).

The CX_LIMITED_RANGE, FENV_ACCESS, or FP_CONTRACT pragma is used in any context other than outside all external declarations or preceding all explicit declarations and statements inside a compound statement (7.3.4, 7.6.1, 7.1.2).

The value of an argument to a character handling function is neither equal to the value of EOF nor representable as an unsigned char (7.4).

A macro definition of errno is suppressed in order to access any actual object, or the program defines an identifier with the name errno (7.5).

Part of the program tests floating-point status flags, sets floating-point control modes, or runs under non-default mode settings, but was translated with the state for FENV_ACCESS pragma “off” (7.6.1).