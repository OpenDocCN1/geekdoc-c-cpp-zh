# ISO/IEC 14882:2017(E)

Table 107 — fmtflags effects

| Element | Effect(s) if set |
| --- | --- |
| boolalpha | insert and extract bool type in alphabetical format |
| dec | converts integer input or generates output in decimal base |
| fixed | generates floating-point output in fixed-point notation |
| hex | converts integer input or generates integer output in hexadecimal base |
| internal | adds fill characters to designated integer point in certain output, or identical to right if no such is designated |
| left | adds fill characters on the right (final positions) of certain generated output |
| oct | converts integer input or generates output in octal base |
| right | adds fill characters on the left (initial positions) of certain generated output |
| scientific | generates floating-point output in scientific notation |
| showbase | generates a prefix indicating the numeric base of generated output |
| showpoint | generates a decimal-point character unconditionally in generated floatingpoint output |
| showpos | generates a sign in non-negative numeric output |
| skipws keeps leading whitespace before before operation |
| unitbuf | flushes output after each output operation |
| uppercase | replaces lowercase letters with their uppercase equivalents in generated output |

Table 108 — fmtflags constants

| Constant | Allowable values |
| --- | --- |
| adjustfield | left | right | internal |
| basefield | dec | oct | hex |
| floatfield | scientific | fixed |

Table 109 — iostate effects

| Element | Effect(s) if set |
| --- | --- |
| badbit | indicates a loss of integrity in an input or output sequence (such as an error read from a file); |
| eofbit | indicates that an input operation reached the end of an input sequence; |
| failbit | indicates that an input operation failed to read the expected characters, or that an output operation failed to generate the desired characters. |

Table 110 — openmode effects

| Element | Effect(s) if set |
| --- | --- |
| app | seek to end before each read |
| ate | open and seek to end immediately after opening |
| binary | perform input and output in binary mode (as opposed to text mode) |
| in | open for input |
| out | open for output |
| trunc | truncate an existing stream when opening |

©ISO/IEC 2017 – All rights reserved