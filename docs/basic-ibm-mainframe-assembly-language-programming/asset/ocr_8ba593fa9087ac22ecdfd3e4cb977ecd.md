# 13. Character Instructions

# 13.1 Basic Character Instructions

The original architecture had instructions to manipulate strings of character data up to 256 bytes in length. In later versions of the architecture, these were extended to handle larger strings but we begin with the most basic.

# 13.1.1 Moving Characters (MVC)

```
MVC D1(L,B1),D2(B2)
```

The basic character move instruction is the MVC instruction. It is an SS instruction and copies up to 256 bytes beginning at the address given as the second operand to the address given as the first operand. The addresses may overlap.

In the machine language coding of an MVC (as is also the case with other SS character instructions), the length is expressed as an 8 bit field whose coded value is one less than the actual length to be moved. Thus, in the machine language format, a length value of 0 means move 1 byte and a length value of 255 means move 256 bytes, and so on. In the assembly language source code, however, the actual length is coded (one will be subtracted from this value by the assembler in constructing the machine language translation).

```
1  MVC L1,L2      * 20 bytes from L2 copied to L1
2  MVC L1(10),L2   * 10 bytes from L2 copied to L1
3
4  LA  R2,L1
5  LA  R3,L2
6
7  MVC 0(20,R2),0(R3) * 20 bytes from L2 copied to L1
8  MVC 10(10,R2),0(R3) * 10 bytes from L2 copied to L1
9  *              * beginning at position 10
10
11 MVC L1(1),=C' '  * blank copied to 1st byte.
12 MVC L1+1(19),L1  * overlapped move; L1 is made
13 *              * all blanks
14
15 L1 DS  CL20
16 L2 DC  C'ABCDEFGHIJKLMNOPQRST'
```

Figure 51 MVC Examples

In the case where no length is supplied, the implied length attribute of the first operand is used. The operands are specified