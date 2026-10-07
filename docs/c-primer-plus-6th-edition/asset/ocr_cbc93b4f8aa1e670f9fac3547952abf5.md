# The ASCII Character Set

Computers store characters using numeric codes. The ASCII (American Standard Code for Information Interchange) code is the most commonly used in the United States. It's also a subset (a very small subset) of Unicode. C++ lets you represent most characters by including the character in single quotation marks, as in '^A' for the A character. You can also represent a single character by using the octal or hex code preceded by backslash, for example, '\012' and '\xa' both represent the linefed (LF) character. Such escape sequences can also be part of a string, as in "Hello,\012 dear". Table C.1 shows the ASCII character set in various representations. When used as a prefix, the ^ character denotes the Ctrl key.

Table C.1 ASCII Character Set Representations

| Decimal | Octal | Hex | Binary | Character | ASCII Name |
| --- | --- | --- | --- | --- | --- |
| 0 | 0 | 0 | 0000000 | ^@ | NUL |
| 1 | 01 | 0x1 | 0000001 | ^A | SOH |
| 2 | 02 | 0x2 | 0000010 | ^B | STX |
| 3 | 03 | 0x3 | 0000011 | ^C | ETX |
| 4 | 04 | 0x4 | 0000100 | ^D | EOT |
| 5 | 05 | 0x5 | 0000101 | ^E | ENQ |
| 6 | 06 | 0x6 | 0000110 | ^F | ACK |
| 7 | 07 | 0x7 | 0000111 | ^G | BEL |
| 8 | 08 | 0x8 | 0001000 | ^H | BS |
| 9 | 011 | 0x9 | 0001001 | ^I, Tab | HT |
| 10 | 012 | 0xa | 0001010 | ^J | LF |
| 11 | 013 | 0xb | 0001011 | ^K | VT |
| 12 | 014 | 0xc | 0001100 | ^L | FF |
| 13 | 015 | 0xd | 0001101 | ^M | CR |