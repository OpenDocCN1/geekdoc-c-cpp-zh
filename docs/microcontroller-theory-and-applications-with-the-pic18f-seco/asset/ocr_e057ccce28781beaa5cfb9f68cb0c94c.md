# SUBLW  Subtract W from Literal

+   Syntax:
SUBLW k
Operands:
0 ≤ k ≤ 255
Operation:
k → (W) → W
Status Affected:
N, OV, C, DC, Z

Encoding:
| 0000 | 1000 | kkkk | kkkk |
| ---- | ---- | ---- | ---- |

+   Description
W is subtracted from the eight-bit literal 'k'. The result is placed in W.
Words:
1
Cycles:
1
Q Cycle Activity:

| Q1 | Q2 | Q3 | Q4 |
| Decode | Read literal 'k' | Process Data | Write to W |
| ---- | ---- | ---- | ---- |

+   Example 1: SUBLW 02h
Before Instruction
W = 01h
C = ?
After Instruction
W = 01h
C = 1 ; result is positive
Z = 1
N = 0

+   Example 2: SUBLW 02h
Before Instruction
W = 02h
C = ?
After Instruction
W = 00h
C = 1 ; result is zero
Z = 1
N = 0

+   Example 3: SUBLW 02h
Before Instruction
W = 03h
C = ?
After Instruction
W = Fh ; (2's complement)
C = 0 ; result is negative
Z = 0
N = 1

# SUBWF  Subtract W from f

+   Syntax:
SUBWF f, {d, (a)}
Operands:
0 ≤ f ≤ 255
d = {0,1}
a = {0,1}
Operation:
(f) − (W) → dest
Status Affected:
N, OV, C, DC, Z

Encoding:
| 0101 | 11dd | ffff | ffff |
| ---- | ---- | ---- | ---- |

Description
Subtract W from register 'f' (2's complement method). If 'd' is '0', the result is stored in W. If 'd' is '1', the result is stored back in register 'f' (default).
If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default).
If 'a' is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever
f ≤ 95 (5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

+   Words:
1
Cycles:
1
Q Cycle Activity:

| Q1 | Q2 | Q3 | Q4 |
| Decode | Read register 'f' | Process Data | Write to destination |
| ---- | ---- | ---- | ---- |

+   Example 1: SUBWF REG, 1, 0
Before Instruction
REG = 3
W = 2
C = ?
After Instruction
REG = 1
W = 2
C = 1 ; result is positive
Z = 0
N = 0

+   Example 2: SUBWF REG, 0, 0
Before Instruction
REG = 2
W = 2
C = ?
After Instruction
REG = 2
W = 0
C = 1 ; result is zero
Z = 1
N = 0

+   Example 3: SUBWF REG, 1, 0
Before Instruction
REG = 1
W = 2
C = ?
After Instruction
REG = Fh ; (2's complement)
W = 2
C = 0 ; result is negative
Z = 0
N = 1