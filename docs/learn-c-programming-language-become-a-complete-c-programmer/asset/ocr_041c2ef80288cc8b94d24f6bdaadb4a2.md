A C++ implementation can be either *hosted* or *freestanding*(§iso.17.6.1.3). A hosted implementation includes all the standard-library facilities as described in the standard (§30.2) and in this book. A freestanding implementation may provide fewer standard-library facilities, as long as the following are provided:

# Freestanding Implementation Headers

+   Types
+   Implementation properties
+   Integer types
+   Start and termination
+   Dynamic memory management
+   Type identification
+   Exception handling
+   Initializer lists
+   Other run-time support
+   Type traits
+   Atomics

<cstddef> §10.3.1 <cfloat> <limits> <climits> §40.2 <cstdint> §43.7 <cstdlib> §43.7 <new> §11.2.3 <typeinfo> §22.5 <exception> §30.4.1.1 <initializer_list> §30.3.1 <cstdalign> <cstdarg> <cstdbool> §12.2.4, §44.3.4 <type_traits> §35.4.1 <atomic> §41.3

Freestanding implementations are meant for code running with only the most minimal operating system support. Many implementations also provide a (non-standard) option for not using exceptions for really minimal, close-to-the-hardware, programs.

# 6.1.2 The Basic Source Character Set

The C++ standard and the examples in this book are written using the *basic source character set* consisting of the letters, digits, graphical characters, and whitespace characters from the U.S. variant of the international 7-bit character set ISO 646-1983 called ASCII (ANSI3.4-1968). This can cause problems for people who use C++ in an environment with a different character set:

+   - ASCII contains punctuation characters and operator symbols (such as ], {, and !) that are not available in some character sets.
+   - We need a notation for characters that do not have a convenient character representation (such as newline and “the character with value 17”).
+   - ASCII doesn’t contain characters (such as ñ, þ, and Æ) that are used for writing languages other than English.

To use an extended character set for source code, a programming environment can map the extended character set into the basic source character set in one of several ways, for example, by using universal character names (§6.2.3.2).

# 6.2 Types

Consider: