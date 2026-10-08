
## CLRF

Clear f

**Syntax:** CLRF f{,a}
**Operands:**
- 0 <= f <= 255
- a ∈ [0,1]

**Operation:**
- 000h → f
- 1 → Z

**Status Affected:** Z

**Encoding:**
```text
0110 101a ffff ffff
```

**Description:** Clears the contents of the specified register.
If 'a' is '0', the Access Bank is selected.
If 'a' is '1', the BSR is used to select the GPR bank (default).
If 'a' is '1' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f <= 95 (5Fh). See **Section 24.2.3 “Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode”** for details.

**Words:** 1
**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register 'f' | Process Data | Write register 'f' |

**Example:**
`CLRF FLAG_REG, 1`

Before Instruction: FLAG_REG = 5Ah
After Instruction: FLAG_REG = 00h

## CLRWDT

Clear Watchdog Timer

**Syntax:** CLRWDT
**Operands:** None

**Operation:**
- 000h → WDT,
- 000h → WDT postscaler,
- 1 → TO,
- 1 → PD

**Status Affected:** TO, PD

**Encoding:**
```text
0000 0000 0000 0100
```

**Description:** CLRWDT instruction resets the Watchdog Timer. It also resets the postscaler of the WDT. Status bits, TO and PD, are set.

**Words:** 1
**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | No operation | Process Data | No operation |

**Example:**
`CLRWDT`

Before Instruction:
WDT Counter = ?
After Instruction:
WDT Counter = 00h
WDT Postscaler = 0
TO = 1
PD = 1

## COMF

Complement f

**Syntax:**
`COMF f {d, a}`

**Operands:**
- 0 ≤ f ≤ 255
- d ∈ {0,1}
- a ∈ {0,1}
- (*f*) → *dest*

**Operation:**
(*f*) → *dest*

**Status Affected:** N, Z

**Encoding:**
| 0001 | 11da | efff | ffff |
| :--- | :--- | :--- | :--- |

**Description:** The contents of register *f* are complemented. If *d* is '0', the result is stored in W. If *d* is '1', the result is stored back in register *f* (default).
If *a* is '0', the Access Bank is selected.
If *a* is '1', the BSR is used to select the GPR bank (default).
If *a* is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever *f* ≤ 95 (5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

**Words:** 1
**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register *f* | Process Data | Write to destination |

**Example:**
`COMF REG, 0, 0`

Before Instruction:
REG = 13h
After Instruction:
REG = 13h
W = ECh

## CPFSEQ

Compare f with W, Skip if f = W

**Syntax:**
`CPFSEQ f (a)`

**Operands:**
- 0 ≤ f ≤ 255
- a ∈ {0,1}
- (f) - (W)
- skip if (f) = (W)
- (unsigned comparison)

**Operation:**
- (f) - (W)
- skip if (f) = (W)
- (unsigned comparison)

**Status Affected:** None

**Encoding:**
| 0110 | 001a | ffff | ffff |
| :--- | :--- | :--- | :--- |

**Description:** Compares the contents of data memory location *f* to the contents of W by performing an unsigned subtraction.
If *f* = W, then the fetched instruction is discarded and a NOP is executed instead, making this a two-cycle instruction.
If *a* is '0', the Access Bank is selected.
If *a* is '1', the BSR is used to select the GPR bank (default).
If *a* is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever *f* ≤ 95 (5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

**Words:** 1
**Cycles:** 1(2)
**Note:** 3 cycles if skip and followed by a 2-word instruction.

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| Decode | Read register *f* | Process Data | No operation |

If skip:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| | Q2 | Q4 | |
| | No operation | No operation | |
| | No operation | No operation | |

If skip and followed by 2-word instruction:

| Q1 | Q2 | Q3 | Q4 |
| :--- | :--- | :--- | :--- |
| No operation | No operation | No operation | No operation |
| No operation | No operation | No operation | No operation |

**Example:**
```text
HERE   CPFSEQ REG, 0
NEQUAL ;
EQUAL  ;
```

Before Instruction:
PC Address = HERE
W = ?
REG = ?
After Instruction:
If REG = W; PC = Address (EQUAL)
If REG ≠ W; PC = Address (NEQUAL)

## CPFSGT

Compare f with W, Skip if f > W

**Syntax:**
`CPFSGT f, a`

**Operands:**
- 0 ≤ f ≤ 255
- a ∈ [0,1]

**Operation:**
- (f) – (W),
- skip if (f) > (W)
- (unsigned comparison)

**Status Affected:** None

**Encoding:**
```text
0110 010a ffff ffff
```

**Description:** Compares the contents of data memory location 'f' to the contents of the W by performing an unsigned subtraction. If the contents of 'f' are greater than the contents of WREG, then the fetched instruction is discarded and a NOP is executed instead, making this a two-cycle instruction.

If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default).

If 'a' is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 ($5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

**Words:** 1
**Cycles:** 1(2)
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
| No operation | No operation | No operation | No operation |

**Example:**

```text
HERE     CPFSGT REG, 0
NGREATER :
GREATER  :
```

Before Instruction:
PC = Address (HERE)
W = ?

After Instruction:
If REG > W; PC = Address (NGREATER)
If REG ≤ W; PC = Address (GREATER)

## CPFSLT

Compare f with W, Skip if f < W

**Syntax:**
`CPFSLT f, a`

**Operands:**
- 0 ≤ f ≤ 255
- a ∈ [0,1]

**Operation:**
- (f) – (W),
- skip if (f) < (W)
- (unsigned comparison)

**Status Affected:** None

**Encoding:**
```text
0110 000a ffff ffff
```

**Description:** Compares the contents of data memory location 'f' to the contents of W by performing an unsigned subtraction. If the contents of 'f' are less than the contents of W, then the fetched instruction is discarded and a NOP is executed instead, making this a two-cycle instruction.

If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the GPR bank (default).

**Words:** 1
**Cycles:** 1(2)
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
| No operation | No operation | No operation | No operation |

**Example:**

```text
HERE   CPFSLT REG, 1
NLESS  :
LESS   :
```

Before Instruction:
PC = Address (HERE)
W = ?

After Instruction:
If REG < W; PC = Address (NLESS)
If REG ≥ W; PC = Address (NLESS)
