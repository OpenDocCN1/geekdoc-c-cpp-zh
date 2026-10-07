© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

+   - The contents of the error message strings set up by the strerror function (7.24.6.2).

+   - The formats for time and date (7.27.3.5, 7.29.5.1).

+   - Character mappings that are supported by the towctrans function (7.30.1).

+   - Character classifications that are supported by the isctype function (7.30.1).

# J.5 Common extensions

The following extensions are widely used in many systems, but are not portable to all implementations. The inclusion of any extension that may cause a strictly conforming program to become invalid renders an implementation nonconforming. Examples of such extensions are new keywords, extra library functions declared in standard headers, or predefined macros that do not begin with an underscore.

# J.5.1 Environment arguments

In a hosted environment, the main function receives a third argument, char *envp[], that points to a null-terminated array of pointers to char, each of which points to a string that provides information about the environment for this execution of the program (5.1.2.2).

# J.5.2 Specialized identifiers

Characters other than the underscore _ letters, and digits, are not part of the source character set (such as the dollar sign $, or characters in national character sets) may appear in an identifier (6.4.2).

# J.5.3 Lengths and case of identifiers

All characters in identifiers (with or without external linkage) are significant (6.4.2).

# J.5.4 Scopes of identifiers

A function, or the identifier of an object the declaration of which contains the keyword extern, has file scope (6.2.1).

# J.5.5 Writable string literals

String literals are modifiable (in which case, identical string literals should denote distinct objects) (6.4.5).