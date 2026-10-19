# ISO/IEC 14882:2020(E)

Table 116: fmtflags effects  [tab:ios.fmtflags]

| Element | Effect(s) if set |
|---|---|
| boolalpha | insert and extract bool type in alphabetic format |
| dec | converts integer input or generates integer output in decimal base |
| fixed | generate floating-point output in fixed-point notation |
| hex | converts integer input or generates integer output in hexadecimal base |
| internal | adds fill characters at a designated internal point in certain generated output, or identical to right if no such point is designated |
| left | adds fill characters on the right (final positions) of certain generated output |
| oct | converts integer input or generates integer output in octal base |
| right | adds fill characters on the left (initial positions) of certain generated output |
| scientific | generates floating-point output in scientific notation |
| showbase | generates a prefix indicating the numeric base of generated integer output |
| showpoint | generates a decimal-point character unconditionally in generated floating-point output |
| showpos | generates a + sign in non-negative generated numeric output |
| skipws | skips leading whitespace before certain input operations |
| unitbuf | flushes output after each output operation |
| uppercase | replaces certain lowercase letters with their uppercase equivalents in generated output |

Table 117: fmtflags constants  [tab:ios.fmtflags.const]

| Constant | Allowable values |
|---|---|
| adjustfield | left | right | internal |
| basefield | dec | oct | hex |
| floatfield | scientific | fixed |

Table 118: iostate effects  [tab:ios.iostate]

| Element | Effect(s) if set |
|---|---|
| badbit | indicates a loss of integrity in an input or output sequence (such as an irrecoverable read error from a file); |
| eofbit | indicates that an input operation reached the end of an input sequence; |
| failbit | indicates that an input operation failed to read the expected characters, or that an output operation failed to generate the desired characters. |

Table 119: openmode effects  [tab:ios.openmode]

| Element | Effect(s) if set |
|---|---|
| app | seek to end before each write |
| ate | open and seek to end immediately after opening |
| binary | perform input and output in binary mode (as opposed to text mode) |
| in | open for input |
| out | open for output |
| trunc | truncate an existing stream when opening |

Table 120: seekdir effects  [tab:ios.seekdir]

| Element | Meaning |
|---|---|
| beg | request a seek (for subsequent input or output) relative to the beginning of the stream |
| cur | request a seek relative to the current position within the sequence |
| end | request a seek relative to the current end of the sequence |