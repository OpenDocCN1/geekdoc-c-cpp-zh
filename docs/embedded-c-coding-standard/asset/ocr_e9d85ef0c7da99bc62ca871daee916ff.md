Embedded C Coding Standard

**Reasoning:** Owing to differences across processor families and loose definitions in the ISO C language standards, there is a tremendous amount of implementation-defined behavior in the area of structures and unions. Bit-fields, in particular, suffer from severe portability problems, including the lack of a standard bit ordering and no official support for the fixed-width integer types they so often call out to be used with. The methods available to check the layout of such data structures include static assertions or other compile-time checks as well as the use of preprocessor directives, e.g., to select one of two competing struct layouts based on the compiler.

**Enforcement:** These rules shall be enforced during code reviews.