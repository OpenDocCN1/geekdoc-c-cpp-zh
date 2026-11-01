Once a number is in packed format, you may do arithmetic on it. While packed or decimal arithmetic is slower than binary arithmetic, it can handle more digits of accuracy and it does not need any further conversion.

# 17.3 Converting Packed Decimal to Binary

To convert a number from zoned decimal to fixed point binary you first must pack the number (PACK is very fast), then perform a Convert to Binary instruction. In the original architecture, this was performed by the CVB instruction which converts a packed number to a 32 bit signed fixed point binary integer leaving the result in a register.

More recently, the similar CVBY instruction has been added which differs from the CVB in that it uses signed long displacements. Also added is the CVBG which likewise uses signed long displacements but the result occupies 64 bits. For the CVB and CVBY instructions, the second operand is an 8 byte packed decimal field, while, for the CVBG, the second operand is a 16 byte packed decimal field.

The reverse, converting binary to packed, is done by the Convert to Decimal CVD instruction which uses a signed 32 bit source register. Also available are the CVDY and CVDG instructions which use long signed displacements and, in the case of the CVDG, the source is a 64 bit register. The instructions write either an 8 or 16 byte signed packed decimal number to memory for 32 and 64 bit register source operands respectively.

# 17.4 Decimal Instruction Set

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