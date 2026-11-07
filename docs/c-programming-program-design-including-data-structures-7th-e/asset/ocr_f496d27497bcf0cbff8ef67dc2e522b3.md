# ### EXAMPLE 4-1

| Expression | Meaning | Value |
|---|---|---|
| 8 < 15 | 8 is less than 15 | `true` |
| 6 != 6 | 6 is not equal to 6 | `false` |
| 2.5 > 5.8 | 2.5 is greater than 5.8 | `false` |
| 5.9 <= 7.5 | 5.9 is less than or equal to 7.5 | `true` |
| 7 <= 10.4 | 7 is less than or equal to 10.4 | `true` |

# ## Comparing Characters

For char values, whether an expression using relational operators evaluates to `true` or `false` depends on a machine's collating sequence. The collating sequence of some of the characters is:

| ASCII Value | Char | ASCII Value | Char | ASCII Value | Char | ASCII Value | Char |
|---|---|---|---|---|---|---|---|
| 32 | ' ' | 61 | = | 81 | Q | 105 | i |
| 33 | ! | 62 | > | 82 | R | 106 | j |
| 34 | " | 65 | A | 83 | S | 107 | k |
| 42 | * | 66 | B | 84 | T | 108 | l |
| 43 | + | 67 | C | 85 | U | 109 | m |
| 45 | - | 68 | D | 86 | V | 110 | n |
| 47 | / | 69 | E | 87 | W | 111 | o |
| 48 | 0 | 70 | F | 88 | X | 112 | p |
| 49 | 1 | 71 | G | 89 | Y | 113 | q |
| 50 | 2 | 72 | H | 90 | Z | 114 | r |
| 51 | 3 | 73 | I | 97 | a | 115 | s |
| 52 | 4 | 74 | J | 98 | b | 116 | t |
| 53 | 5 | 75 | K | 99 | c | 117 | u |
| 54 | 6 | 76 | L | 100 | d | 118 | v |
| 55 | 7 | 77 | M | 101 | e | 119 | w |
| 56 | 8 | 78 | N | 102 | f | 120 | x |
| 57 | 9 | 79 | O | 103 | g | 121 | y |
| 60 | < | 80 | P | 104 | h | 122 | z |

The ASCII character set is described in Appendix C.

Now, because 32 < 97, and the ASCII value of ' ' is 32 and the ASCII value of 'a' is 97, it follows that ' ' < 'a' is `true`. Similarly, using the previous ASCII values: