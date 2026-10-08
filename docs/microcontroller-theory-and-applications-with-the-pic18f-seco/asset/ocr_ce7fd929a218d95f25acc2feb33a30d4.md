# ADDWFC ADD W and CARRY bit to f

**Syntax:** ADDWFC f{,d (a)}

**Operands:**
0 ≤ f ≤ 255
d ∈ {0,1}
a ∈ {0,1}

**Operation:**
(W) + (f) + (C) → dest

**Status Affected:**
N, OV, C, DC, Z

**Encoding:**

| 0010 | 00da | ffff | ffff |
|---|---|---|---|
|  |  |  |  |

**Description:** Add W, the Carry flag and data memory location *f*. If *d* is '0', the result is placed in W. If *d* is '1', the result is placed in data memory location *f*.
If *a* is '0', the Access Bank is selected. If *a* is '1', the BSR is used to select the GPR bank (default).
If *a* is '0' and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f ≤ 95 (5Fh). See Section 24.2.3 "Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode" for details.

**Words:**
1

**Cycles:**
1

**Q Cycle Activity:**

|  | Q1 | Q2 | Q3 | Q4 |
|---|---|---|---|---|
|  | Decode | Read register *f* | Process Data | Write to destination |

```
**Example:** ADDWFC REG, 0, 1
```

```
Before Instruction
Carry bit = 1
REG = 02h
W = 4Dh
After Instruction
Carry bit = 0
REG = 02h
W = 50h
```

# ANDLW AND Literal with W

**Syntax:** ANDLW k

**Operands:** 0 ≤ k ≤ 255

**Operation:** (W) .AND. k → W

**Status Affected:** N, Z

**Encoding:**

| 0000 | 1011 | kkkk | kkkk |

**Description:** The contents of W are ANDed with the 8-bit literal 'k'. The result is placed in W.

**Words:** 1

**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
|---|---|---|---|
| Decode | Read literal 'k' | Process Data | Write to W |

```
**Example:** ANDLW 05Fh
```

```
Before Instruction
W = A3h
After Instruction
W = 03h
```