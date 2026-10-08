# **CPFSGT**

Compare f with W, Skip if f > W

Syntax:    **CPFSGT   {a}
Operands:  0 ≤ f ≤ 255
           a ∈ [0,1]
Operation: (f) – (W),
           skip if (f) > (W)
           (unsigned comparison)
Status Affected:  None
Encoding:    0110  010a  ffff ffff

Description: Compares the contents of data memory location 'f' to the contents of the W by performing an unsigned subtraction. If the contents of 'f' are greater than the contents of WREG, then the fetched instruction is discarded and a NOP is executed instead, making this a two-cycle instruction.

If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default).

If 'a' is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 ($5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

Words: 1
Cycles: 1(2)
**Note:** 3 cycles if skip and followed by a 2-word instruction.

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | No operation |

**If skip:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |

**If skip and followed by 2-word instruction:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| No operation | No operation | No operation | No operation

**Example:**

    HERE        CPFSGT REG, 0
    NGREATER    :
    GREATER     :

    Before Instruction
    PC   = Address (HERE)
    W    = ?

    After Instruction
    If REG > W;
    PC   = Address (NGREATER)
    If REG ≤ W;
    PC   = Address (GREATER)

# **CPFSLT**

Compare f with W, Skip if f < W

Syntax:    **CPFSLT   {a}
Operands:  0 ≤ f ≤ 255
           a ∈ [0,1]
Operation: (f) – (W),
           skip if (f) < (W)
           (unsigned comparison)
Status Affected:  None
Encoding:    0110  000a  ffff ffff

Description: Compares the contents of data memory location 'f' to the contents of W by performing an unsigned subtraction. If the contents of 'f' are less than the contents of W, then the fetched instruction is discarded and a NOP is executed instead, making this a two-cycle instruction.

If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default).

Words: 1
Cycles: 1(2)
**Note:** 3 cycles if skip and followed by a 2-word instruction.

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | No operation |

**If skip:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |

**If skip and followed by 2-word instruction:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| No operation | No operation | No operation | No operation

**Example:**

    HERE        CPFSLT REG, 1
    NLESS       :
    LESS        :

    Before Instruction
    PC   = Address (HERE)
    W    = ?

    After Instruction
    If REG < W;
    PC   = Address (NLESS)
    If REG ≥ W;
    PC   = Address (NLESS)