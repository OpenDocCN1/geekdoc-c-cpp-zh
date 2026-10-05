C and C++ also use forward declarations. A forward declaration tells the compiler that a variable, function, struct or class is in some other header file.

# Effective Header Management

The problem with the C++ compilation model is as follows. We make tiny, innocuous change in a header file and then 200 implementation files that include this header file have to be recompiled. This consumes a lot of time. In addition, we can have circular dependencies in header files. Header A includes header B, which includes header C. Header C includes header A.

How can we effectively manage header files and header dependencies in order to make our build times quicker?

The first rule is that an implementation file should only include the header files that it actually needs.

# Forward Declarations

The second rule is to use forward declarations in preference to including header files whenever possible.

Forward declarations introduce an identifier to the compiler. In certain cases, an identifier is all that is required, we do not need to include the header file containing the declaration of the identifier. The compiler only needs to know that a specific identifier is declared in some other header file. Details about the how much memory it requires or what methods it has, are generally not relevant to the identifier is actually used in an implementation.

A forward declaration to an identifier will be sufficient when the include implementation file only uses a pointer to the identifier and this file does not need to