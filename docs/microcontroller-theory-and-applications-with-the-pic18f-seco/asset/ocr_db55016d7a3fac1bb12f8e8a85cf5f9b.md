# Appendix D: PIC18F Instruction Set - Details

# INCFSZ Increment f, Skip if 0

Syntax: INCFSZ f(d , a)
Operands: 0 ≤ f ≤ 255
d ∈ [0,1]
a ∈ [0,1]

Operation: (f) + 1 → dest,
skip if result = 0

Status Affected: None

Encoding:
0011 1ida eeee eeee

Description: The contents of register 'f' are incremented. If 'd' is '0', the result is placed back in register 'f' (default). If 'd' is '1', the next instruction, which is already fetched, is discarded and a NOP is executed instead, making it a two-cycle instruction.
If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default). If 'a' is '1' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 (5Fh). See **Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode"** for details.

Words: 1
Cycles: 1(2)
Note: 3 cycles if skip and followed by a 2-word instruction.

Q Cycle Activity:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | Write to destination |

If skip:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |

If skip and followed by 2-word instruction:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| No operation | No operation | No operation | No operation |

```
Example:
HERE INCFSZ CNT, 1, 0
NZERO :
:
Before Instruction
PC = Address (HERE)
After Instruction
PC = CNT + 1
If CNT = 0,
PC = Address (ZERO)
If CNT ≠ 0;
PC = Address (NZERO)
```

# INFSGZ Increment f, Skip if Not 0

Syntax: INFSNZ f(d , a)
Operands: 0 ≤ f ≤ 255
d ∈ [0,1]
a ∈ [0,1]

Operation: (f) + 1 → dest,
skip if result ≠ 0

Status Affected: None

Encoding:
0100 10da eeee eeee

Description: The contents of register 'f' are incremented. If 'd' is '0', the result is placed back in register 'f' (default). If 'd' is '1', the next instruction, which is already fetched, is discarded and a NOP is executed instead, making it a two-cycle instruction.
If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default). If 'a' is '1' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 (5Fh). See **Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode"** for details.

Words: 1
Cycles: 1(2)
Note: 3 cycles if skip and followed by a 2-word instruction.

Q Cycle Activity:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | Write to destination |

If skip:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |

If skip and followed by 2-word instruction:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| No operation | No operation | No operation | No operation |

```
Example:
HERE INFSNZ REG, 1, 0
NZERO :
:
Before Instruction
PC = Address (HERE)
After Instruction
REG = REG + 1
If REG = 0,
PC = Address (ZERO)
If REG ≠ 0;
PC = Address (ZERO)
```

411