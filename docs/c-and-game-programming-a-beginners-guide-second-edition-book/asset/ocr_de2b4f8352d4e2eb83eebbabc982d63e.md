| Data Types: | Prefixes |
|---|---|
| Boolean | b |
| BYTE (unsigned char) | by |
| Character (for types char, WCHAR, and TCHAR) | c |
| Integer used as x, y lengths (c stands for count). | cx, cy |
| Double WORD (unsigned long integer) | dw |
| Function | Fn |
| Handle | H |
| Integers | i |
| Integer used as x, y coordinates | x, y |
| f stands for "flags" | f |
| Long Integers | l |
| String | S |
| String terminated by 0 character | Sz |
| Pointer | p |
| Short Integers | n |
| WORD (unsigned short integer) | w |

Table 1.6. Prefixes for various data types.

# Troubleshooting

Before going through the steps involved in the process of troubleshooting, let’s make sure that we understand the four basic types of errors. The first type, known as a *syntax error*, is what might be described as a grammatical error. The compiler, acting as a spell-checker, looks through our programs trying to find any and all misspelled commands and/or forgotten punctuation marks. If it finds any errors, the compiler immediately sends notification and directs us to the problem. Programs with this type of error cannot be "built", and thus no linkable objects are produced.

The second type of error is known as a *runtime error*. *Runtime errors* usually involve asking the computer to do something it can’t, such as dividing by zero or storing a