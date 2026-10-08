# ## Appendix D: PIC18F Instruction Set - Details

**LFSR**  
Load FSR

Syntax: LFSR f, k
Operands: 0 ≤ f ≤ 2
          0 ≤ k ≤ 4095
          k → FSRf
Operation:
Status Affected: None
Encoding:

| 1110 1110 00ff | k₁.kkk |
| 1111 0000 k.kkk |

Description: The 12-bit literal 'k' is loaded into the File Select Register pointed to by 'f'.
Words: 2
Cycles: 2

| Q Cycle Activity: | Q1 | Q2 | Q3 | Q4 |
|-------------------|----|----|----|----|
| Decode | Read literal 'k' MSB | Process Data | Write literal 'k' MSB to FSRlH |
| Decode | Read literal 'k' LSB | Process Data | Write literal 'k' to FSRlL |

Example: LFSR 2, 3ABh
After Instruction:
FSR2H = 03h
FSR2L = ABh

**MOVF**  
Move f

Syntax: MOVF f, d (d, a)
Operands: 0 ≤ f ≤ 255
          d ∈ {0, 1}
          a ∈ {0, 1}
          f → dest
Operation:
Status Affected: N, Z
Encoding:

| 0101 | 00aa | ffff | ffff |

Description: The contents of register 'f' are moved to a destination dependent upon the status of 'd'. If 'd' is '0', the result is placed in W. If 'd' is '1', the result is placed back in register 'f' (default). Location 'f' can be anywhere in the 256-byte bank.

If 'a' is '0', the Access Bank is selected.
If 'a' is '1', the BSR is used to select the GPR bank (default).
If 'a' is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 (5Fh). See *Section 24.2.3 “Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode”* for details.

Words: 1
Cycles: 1

| Q Cycle Activity: | Q1 | Q2 | Q3 | Q4 |
|-------------------|----|----|----|----|
| Decode | Read register 'f' | Process Data | Write W |

Example: MOVF REG, 0, 0
Before Instruction:
REG = 22h
W = FFh
After Instruction:
REG = 22h
W = 22h