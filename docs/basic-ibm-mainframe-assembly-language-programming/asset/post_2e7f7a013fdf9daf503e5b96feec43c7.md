
## 17. Decimal Arithmetic

The decimal instruction set consists of those instructions that operate on or support packed decimal (also known as BCD or binary coded decimal) data.

### 17.1 Zoned and Packed Decimal

Arithmetic on an IBM mainframe can be carried out in fixed point binary integer, packed decimal and floating point modes.

Initially, when numbers are read as character (EBCDIC) input (when using the z390 emulator, ASCII input is automatically converted to EBCDIC by the emulator), they are in what is called zoned decimal format where the high order 4 bits of each byte contain a hexadecimal F₁₆ called the zone and the low order 4 bits (called the digit) are the value of the character number in binary (0 through 9). For example, the internal hexadecimal EBCDIC for the printable number 1234 is:

```
F1 F2 F3 F4
```

Arithmetic may not be performed on character representations of numbers. Instead, they must be converted to one of the numeric types: packed decimal, fixed point binary or floating point. Of these, conversion to packed decimal is the easiest.

A packed decimal number is a string of one or more bytes containing, in each half byte, a value (in binary) from 0 to 9 except for the last half byte. The last half byte contains the sign of the number. The hex codes C,A,F, and E mean the number is positive (CAFE) and the codes D and B mean it's negative (DB). Thus, the zoned decimal number 1234 (F1 F2 F3 F4) in packed format would be:

```
01 23 4F
```

In this format the zones have been eliminated and a sign appended. All packed decimal numbers occupy an integral number of bytes in memory. A leading zero is prepended as necessary.

Packed decimal numbers can be up to 16 bytes long and, therefore, can represent numbers up to 31 digits (2 digits per byte except for the last byte which has one digit and the sign). Packed decimal is especially useful for business applications where many digits of accuracy are required.

### 17.2 The PACK Instruction

The PACK instruction is used to convert from printable, zoned decimal character strings to packed decimal. As noted above, all zoned numeric characters have the same value of F₁₆ for their zone (the high order 4 bits of each character). The low order portion of all zoned numeric characters (called the numeric part of a byte) is a 4 bit binary number whose value is between zero and nine. The PACK instruction, when applied to a string of zoned numbers, removes the zones from all bytes except the last and packs two numerics per byte. In the last byte (possibly the only byte), it swaps the numeric and zoned fields. The result is padded with leading zeros as needed to make an integral number of bytes. This is illustrated in Figure 57.

![](img/4b7e9c58cac527296b19b501116daeb1_155_0.png)

Figure 57 1234 in Zoned & Packed

In a PACK instruction, both operands are located in memory. The operands are processed one byte at a time from left to right. The second operand is the source and the result replaces the first operand. The Condition Code is unchanged.

Bytes from left to right of the source are read, the zone is removed and the digit portion stored in the next available half byte moving to the right in the target. The source and target may be of different lengths but the target must be long enough to hold the answer. If the source field is short and the target field long, the target will be padded to the left with leading zeros as needed.

The final byte of the source, however, is treated differently. In this case, the zone and digit parts of the source byte are reversed and placed in the last (rightmost) byte of the target. This always results in an F₁₆ code in the sign position. Since F₁₆ is one of the positive sign indicators in packed format, all numbers are initially positive until altered by the program. The positive sign can be changed to negative by executing an AND Immediate instruction on the low order (rightmost) byte of the packed result with an immediate byte (mask) of X'F0'. This will preserve the high order four bits and alter the low order F₁₆ to D₁₆ thus making the number negative.

Once a number is in packed format, you may do arithmetic on it. While packed or decimal arithmetic is slower than binary arithmetic, it can handle more digits of accuracy and it does not need any further conversion.

### 17.3 Converting Packed Decimal to Binary

To convert a number from zoned decimal to fixed point binary you first must pack the number (PACK is very fast), then perform a Convert to Binary instruction. In the original architecture, this was performed by the CVB instruction which converts a packed number to a 32 bit signed fixed point binary integer leaving the result in a register.

More recently, the similar CVBY instruction has been added which differs from the CVB in that it uses signed long displacements. Also added is the CVBG which likewise uses signed long displacements but the result occupies 64 bits. For the CVB and CVBY instructions, the second operand is an 8 byte packed decimal field, while, for the CVBG, the second operand is a 16 byte packed decimal field.

The reverse, converting binary to packed, is done by the Convert to Decimal CVD instruction which uses a signed 32 bit source register. Also available are the CVDY and CVDG instructions which use long signed displacements and, in the case of the CVDG, the source is a 64 bit register. The instructions write either an 8 or 16 byte signed packed decimal number to memory for 32 and 64 bit register source operands respectively.

### 17.4 Decimal Instruction Set

The basic set of packed decimal arithmetic instructions are shown in Figure 58.

| Code | Description |
|------|-------------|
| AP | Add Packed |
| CP | Compare Packed |
| DP | Divide Packed |
| ED | Edit |
| EDMK | Edit and Mark |
| MP | Multiply Packed |
| SP | Subtract Packed |
| SRP | Shift and Round Packed |
| TP | Test Packed |
| ZAP | Zero and Add Packed |

Figure 58 Decimal Instructions

The example in Figure 59 illustrates some basic packed arithmetic operations. It reads in a set of numbers in zoned

```asm
 1      PRINT     NOGEN
 2  SUM SUBENTRY
 4  LOOP XREAD     IN,L'IN
 5       BC        B'0100',ATEND
 6       XPRNT     IN,L'IN
 7       PACK      NBR,IN+1(7)       * PACK THE NUMBER
 8       CLI       IN,C'+'
 9       BE        ADD
10       CLI       IN,C'-'
11       BNE       ERR1
12       NI        NBR+7,X'FD'       * make negative
13  ADD  TP        NBR
14       BNE       ERR2
15       AP        ACC,NBR           * ADD TO TOTAL
16       B         LOOP              * READ ANOTHER RECORD
18       * EOF - BRANCH HERE WHEN OUT OF RECORDS
20  ERR1 XPRNT     ERRM1,L'ERRM1
21       B         EXIT
23  ERR2 XPRNT     ERRM2,L'ERRM2
24       B         EXIT
26  ATEND ED        RSLT,ACC          * UNPACK AND FORMAT RESULT
27       XPRNT     RSLT,L'RSLT
28  EXIT SUBEXIT
30  IN   DS        CL8
31  NBR  DS        PL8
32  ACC  DC        PL4'0'
33  ERRM1 DC        C'SIGN ERROR'
34  ERRM2 DC        C'NUMBER ERROR'
36  RSLT DC        X'40202020202120' * EDIT PATTERN
38  END  ADD
```

Sample input data:

1
1234
-1234
2

Figure 59 Decimal Arithmetic Example

### 17.6 Multiply Packed (MP)

In the MP instruction, the multiplier (the second operand) is multiplied by the multiplicand (first operand) and the result is placed in the first operand. The multiplier may not be longer than 15 digits and must be shorter in length than the multiplicand. In order to prevent an overflow from occurring, the multiplicand must include at least as many leading bytes of zeros as the number of bytes in the multiplier. If this is not the case, a data exception occurs. The Condition Code is unchanged.

### 17.7 Divide Packed (DP)

In the DP instruction, the first operand is the dividend and the second operand is the divisor. The results are a quotient and a remainder which will replace the dividend. The divisor may not be longer than 15 digits.

The quotient occupies the leftmost bytes of the result. Its length is equal to the difference between the length of the dividend (L1) and the divisor (L2). The remainder occupies the remaining bytes of the first operand. A Decimal Divide exception occurs in the case of divide by zero or a quotient too large to fit in the digits available. The Condition Code is unchanged.

### 17.8 EDIT (ED)

Although there is an Unpack instruction (UNPK), the ED instruction is the preferred way to convert packed decimal number to a zoned decimal, printable string. The first operand is a set of pattern codes that control the formatting process and the second operand is the packed number to be converted. The result replaces the first operand.

The first byte of the first operand pattern is called the fill byte. It will be placed in the leading bytes of the result in place of non-significant leading zeros.

Following the fill byte are a collection of pattern bytes and message bytes.

When the instruction begins the significance indicator is off. It stays off until a significant digit (i.e., non-zero) is encountered or turned on by a pattern byte. When the significance indicator is off, zeros in the source are replaced by the fill byte. If the significance indicator is on, the source digit appears in the result even if it is zero.

There are two main pattern bytes: 20₁₆ and 21₁₆. The first is called the digit selector. If encountered in the format, the next digit in the source field is selected. If the source digit is zero and the significance indicator is off, the fill byte replaces the digit
