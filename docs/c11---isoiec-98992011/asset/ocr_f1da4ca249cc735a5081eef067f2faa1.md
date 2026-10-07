# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 5. Environment

An implementation translates C source files and executes C programs in two data-processing-system environments, which will be called the translation environment and the execution environment in this International Standard. Their characteristics define and constrain the results of conforming C programs constructed according to the syntactic and semantic rules for conforming implementations.

Forward references: In this clause, only a few of many possible forward references have been noted.

# 5.1 Conceptual models

# 5.1.1 Translation environment

# 5.1.1 Translation structure

A program need not be translated at the same time. The text of the program is kept in units called source (or preprocessing files) in this International Standard. A source file together with all the headers and source files included via the preprocessing directive #include is known as a preprocessing unit. After preprocessing, a preprocessing translation unit is called a translation unit. Previously translated units may be preserved independently or in libraries. The separate translation units of a program communicate (for example) calls to functions whose identifiers have external linkage, manipulation of objects whose identifiers have external linkage, or manipulation of data files. Translation units may be separately translated and then later linked to produce an executable program.

Forward references: linkages of identifiers (6.2.2), external definitions (6.9), preprocessing directives (6.10).

# 5.1.1.2 Translation phases

The precedence among the syntax rules of translation is specified by the following phases⁶

+   1. Physical source file multibyte characters are mapped, in an implementation-defined manner, to the source file (introducing new-line characters for end-of-line indicators) if necessary. Trigraph sequences are replaced by corresponding single-character internal representations.

> 6 Implementations shall behave as if these separate phases occur, even though many are folded folded together practice. Source files, translations, and translated units need not necessarily be stored as files, nor need there be any one-to-one correspondence between these entities and an external representation. The description is conceptual only, and does not specify any