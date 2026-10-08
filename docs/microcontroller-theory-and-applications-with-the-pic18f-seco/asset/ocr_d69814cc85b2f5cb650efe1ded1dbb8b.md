# IORLW Inclusive OR Literal with W

**Syntax:** IORLW k

**Operands:** 0 ≤ k ≤ 255

**Operation:** (W).OR. k → W

**Status Affected:** N, Z

**Encoding:** | 0000 | 1001 | kkkk | kkkk |
| --- | --- | --- | --- |


**Description:** The contents of W are ORed with the eight-bit literal ‘k’. The result is placed in W.

**Words:** 1
**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
|---|---|---|---|
| Decode | Read literal ‘k’ | Process Data | Write to W |


**Example:** IORLW 35h

Before Instruction W = 9Ah
After Instruction W = BFh

# IORWF Inclusive OR W with f

**Syntax:** IORWF f {d, (a)}

**Operands:** 0 ≤ f ≤ 255, d ∈ {0,1}, a ∈ {0,1}

**Operation:** (W).OR. (f) → dest

**Status Affected:** N, Z

**Encoding:** | 0001 | 00da | ffff | ffff |
| --- | --- | --- | --- |


**Description:** Inclusive OR W with register f. If ‘d’ is ‘0’, the result is placed in W. If ‘d’ is ‘1’, the result is placed back in register ‘f’ (default). If ‘a’ is ‘0’, the Access Bank is selected. If ‘a’ is ‘1’, the BSR is used to select the GPR bank (default). If ‘a’ is ‘0’ and the extended instruction set is enabled, this instruction operates in Indexed Literal Offset Addressing mode whenever f= 05 (5Fh). See **Section 24.2.3 “Byte-Oriented and Bit-Oriented Instructions in Indexed Literal Offset Mode”** for details.

**Words:** 1
**Cycles:** 1

**Q Cycle Activity:**

| Q1 | Q2 | Q3 | Q4 |
|---|---|---|---|
| Decode | Read register f | Process Data | Write to destination |


**Example:** IORWF RESULT, 0, 1

Before Instruction RESULT = 13h, W = 91h
After Instruction RESULT = 13h, W = 93h