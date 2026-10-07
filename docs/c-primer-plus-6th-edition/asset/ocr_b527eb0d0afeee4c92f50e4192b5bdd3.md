# Alternative Tokens

In addition to keywords, C++ has some alphabetic alternative representations of operators, termed alternative tokens.These too, are reserved.Table B.2 lists the alphabetic tokens and the operators they represent.

Table B.2 C++ Reserved Alternative Tokens and Their Meanings
| Token | Meaning |
| --- | --- |
| and | && |
| and_eq | &= |
| bitand | & |
| bitor | | |
| compl | ~ |
| not | ! |
| not_eq |= |
| or | || |
| or_eq |= |
| xor | ^ |
| xor_eq | ^= |

# C++ Library Reserved Names

The compiler won't let you use keywords and alternative tokens as names. There's another class of forbidden names for which the protection is not as absolutereserved names, which are names reserved for use by the C++ library. If you use one of these as an identifier, the effect is undefined. That is, it might generate a compiler error, or it might generate a warning, which might cause a program to run incorrectly, or it might cause no problems at all.

The C++ language reserves macro names used in a library header file. If a program includes a header file, you shouldn't use the names of macros defined in that header (or in headers included by header file, and so on) for other purposes. For example, if you use the header file <limits> directly or indirectly, you shouldn't use CHAR_BIT as an identifier that is already used as a macro in that header file.

The C++ language reserves names beginning with two underscores or a single underscore followed by an uppercase letter for any use, and it reserves names beginning with a single underscore for use as a global variable. So don't create names as __gink or __Lynx in any case and names as _lynx in the global namespace.