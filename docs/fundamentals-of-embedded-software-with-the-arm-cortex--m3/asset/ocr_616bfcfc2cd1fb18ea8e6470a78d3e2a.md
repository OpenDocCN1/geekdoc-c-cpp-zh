| Constant | Hex | Character | Constant | Hex | Character |
|---|---|---|---|---|---|
| '\a' | 07 | alert (e.g., bell) | '\v' | 0B | vertical tab |
| '\b' | 08 | backspace | '\\' | 5C | Backslash |
| '\f' | 0C | form feed | '\'' | 27 | single quote |
| '\n' | 0A | newline | '"' | 22 | double quote |
| '\r' | 0D | carriage return | '\?' | 3F | question mark |
| '\t' | 09 | horizontal tab | | | |

Programming languages (both high-level languages, such as C, and assembly languages) do not require the programmer to memorize the ASCII code. Rather than writing a binary or hex constant, the 7-bit pattern containing the ASCII code of a character can be produced by simply using a literal character constant. For example, suppose you want to store the ASCII code for the letter A in a byte of memory. Rather than writing the hex constant 0x41 (in C) or 41h (in assembly), both languages allow surrounding the letter by a pair of apostrophes (as in 'A') to achieve the same purpose. Some of the more frequently used of the first 32 ASCII control codes can be represented in C using character escapes, as shown in Table 2-3. A character escape consists of a backslash followed by a letter; surrounding the combination with apostrophes produces an ASCII code that has no corresponding graphic image. In general, the use of character literals instead of the numeric codes produces source code that is much more readable, and it helps avoid what are known as “magic constants” whose intended purpose becomes obscured over time.

Words, sentences, and paragraphs are examples of character strings. In addition to the string’s content, somehow the length of the string must also be indicated. Otherwise, we would not know when to stop trying to interpret the contents of memory as ASCII codes!

The length of a character string is specified either by a character count (stored at the front of the string) or by a special sentinel byte that marks the end of the string. In C, a sentinel byte consisting of all zeroes (called a NULL) is used to mark the end of a string. Thus, a string constant such as “Hello” occupies a total of six bytes of memory: five for the letters of the word and a sixth byte for the terminating byte of all zeroes (Figure 2-10).

| 'H' | 'e' | 'l' | 'l' | 'o' | NUL |
|---|---|---|---|---|---|
| 01001000 | 01100101 | 01101100 | 01101100 | 01101111 | 00000000 |
| 48 | 65 | 6C | 6C | 6F | 00 |