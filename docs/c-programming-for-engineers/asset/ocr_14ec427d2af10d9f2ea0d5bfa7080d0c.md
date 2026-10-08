# 4.4. Printing Value Variables

Table 4.8: ASCII character set

| Bits 3-0 | 000 | 001 | 010 | 011 | 100 | 101 | @ | 110 | 111 |
|---|---|---|---|---|---|---|---|---|--|
| 0000 | NUL | DLE | | SP | | | | p |
| 0001 | SOH | DC1 | | 1 | A | Q | | q |
| 0010 | STX | DC2 | | 2 | B | R | | r |
| 0011 | ETX | DC3 | | # | C | S | | s |
| 0100 | EOT | DC4 | | $ | D | T | | t |
| 0101 | ENQ | NAK | | % | E | U | | u |
| 0110 | ACK | SYN | | 6 | F | V | | v |
| 0111 | BEL | ETB | | 7 | G | W | | w |
| 1000 | BS | CAN | ( | 8 | H | X | | x |
| 1001 | HT | EM | | 9 | I | Y | | y |
| 1010 | LF | SUB | | : | J | Z | | z |
| 1011 | VT | ESC | | ; | K | | k | | |
| 1100 | FF | FS | | < | L | | l | | |
| 1101 | CR | GS | | = | M | | m | } |
| 1111 | SI | US | | / | > | n | | n |

Declaring a string variable with an array size allocates enough space for the specified number of characters plus the null terminator. For example:

```
char myArray[15]; // Creates space for 14 characters + null terminator
```

To initialize strings, you can specify the array size or let the compiler determine it. C automatically adds the null terminator when necessary:

You can also initialize a string character by character:

```
char name[] = { 'J', 'a', 'n', 'e', '\0' }; // Explicit size (5 bytes)
```

Understanding the char data type and strings means you are now able to handle text in C.

# 4.4 Printing Value of Variables

Up to this, we've utilized printf primarily for fixed messages. The first parameter of printf is referred to as the format string. When printf encounters a format specifier in this string, it substitutes it with the corresponding argument from the argument list. In the example below: