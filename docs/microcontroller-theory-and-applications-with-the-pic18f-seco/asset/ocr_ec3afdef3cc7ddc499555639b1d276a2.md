# **SUBWF** Subtract W from f with Borrow

Syntax:
SUBWF f,{d,a}
Operands:
0 <= f <= 255
d a [0,1]
a a [0,1]
Operation:
(f) - (W) - (<G>) -> dest
Status Affected:
N, OV, C, DC, Z

Encoding:
0101 10da ffff ffff
Description:
Subtract W and the Carry flag (borrow) from register 'f' (2's complement method). If 'd' is '0', the result is stored in W. If 'd' is '1', the result is stored back in register 'f' (default).
If 'a' is '0', the Access Bank is selected.
If 'a' is '1', the BSR is used to select the GPR bank (default).
If 'a' is '1' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f <= 95 (5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

Words: 1
Cycles: 1

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | Write to destination |

```
Example 1: SUBWF REG, 1, 0
Before Instruction
REG = 19h (0001 1001)
W = 1
C = 1
After Instruction
REG = 0Ch (0000 1101)
W = 1
C = 1
Z = 0
N = 0 ; result is positive
```

```
Example 2: SUBWF REG, 0, 0
Before Instruction
REG = 1Bh (0001 1011)
W = 1Ah (0001 1010)
C = 0
After Instruction
REG = 1Bh (0001 1011)
W = 0h
C = 1
Z = 1
N = 0 ; result is zero
```

```
Example 3: SUBWF REG, 1, 0
Before Instruction
REG = 03h (0000 0011)
W = 0Eh (0000 1101)
C = 1
After Instruction
REG = F5h (1111 0100) ; (2's comp.)
C = 0
Z = 0
N = 1 ; result is negative
```

# **SWAPF** Swap f

Syntax:
SWAPF f,{d,a}
Operands:
0 <= f <= 255
d a [0,1]
a a [0,1]
Operation:
(<3:0>) -> dest<7:4>,
(<7:4>) -> dest<3:0>
Status Affected:
None

Encoding:
0011 10da ffff ffff
Description:
The upper and lower nibbles of register 'f' are exchanged. If 'd' is '0', the result is placed in W. If 'd' is '1', the result is placed in register 'f' (default).
If 'a' is '0', the Access Bank is selected.
If 'a' is '1', the BSR is used to select the GPR bank (default).
If 'a' is '1' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f <= 95 (5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

Words: 1
Cycles: 1

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | Write to destination |

```
Example: SWAPF REG, 1, 0
Before Instruction
REG = 53h
After Instruction
REG = 35h
```