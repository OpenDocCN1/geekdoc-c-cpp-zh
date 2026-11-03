# The Joy of Hex

Face it: No one wants to count bits in a binary number. No one. Perhaps some nerd somewhere can tell you that 10110001 is really the value 177 (I had to look it up), but most programmers can't. What a good programmer can do, however, is translate binary into hex.

Hex has nothing to do with Harry Potter. It’s short for hexadecimal, which is the base 16 counting system. This concept isn’t as obtuse as it sounds, because it’s easy to translate between base 16 (hex) and binary.

For example, the value 10110001 translates into B1 hexadecimal. I can see that at once because I’ve been using hex for a while. It also means that I accept a hexadecimal numbers include the letters A through F, representing decimal values 10 through 15, respectively. A B in hex is the decimal value 11. Letters are used because they occupy a single character position.

Table 17-4 shows the 16 hexadecimal values 0 through F and how they relate to four bits of data.

| Hex | Binary | Decimal | Hex | Binary | Decimal |
|-----|--------|---------|-----|---------|---------|
| 0x0 | 0000 | 0 | 0x8 | 1000 | 8 |
| 0x1 | 0001 | 1 | 0x9 | 1001 | 9 |
| 0x2 | 0010 | 2 | 0xA | 1010 | 10 |
| 0x3 | 0011 | 3 | 0xB | 1011 | 11 |
| 0x4 | 0100 | 4 | 0xC | 1100 | 12 |
| 0x5 | 0101 | 5 | 0xD | 1101 | 13 |
| 0x6 | 0110 | 6 | 0xE | 1110 | 14 |
| 0x7 | 0111 | 7 | 0xF | 1111 | 15 |

The hexadecimal values shown in Table 17-4 are prefixed with 0x. This prefix is used in C, though other programming languages may use different prefixes or a postfix.

The next hexadecimal value after 0xF is 0x10. Don’t read it as the number ten, but rather as “one zero hex.” It’s the value 16 in decimal (base 10). After that, hex keeps counting with 0x11, 0x12, up and through 0xFF and beyond.