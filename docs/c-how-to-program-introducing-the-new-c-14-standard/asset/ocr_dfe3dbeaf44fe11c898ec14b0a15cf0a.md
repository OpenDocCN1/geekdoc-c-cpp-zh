# Fig. 22.7 Results of combining two bits with the bitwise AND operator (`&`).

| Bit 1 | Bit 2 | Bit 1 & Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 1 | 1 |

![](bbox=[0.118, 0.411, 0.188, 0.464])

# Common Programming Error 22.2

*Using the logical AND operator (`&&`) for the bitwise AND operator (`&`) and vice versa is a logic error.*

The program of **Fig. 22.8** demonstrates the *bitwise AND operator*, the *bitwise inclusive OR operator*, the *bitwise exclusive OR operator* and the *bitwise complement operator*. Function `displayBits` (lines 47–64) prints the `unsigned` integer values.