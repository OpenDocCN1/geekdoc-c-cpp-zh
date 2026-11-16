TABLE 7-2 ARM Condition Codes

| Code | Meaning | Requirements |
|---|---|---|
| EQ | **E**qual | Z = 1 |
| NE | **N**ot Equal | Z = 0 |
| HS | Unsigned ≥ (“Higher or Same”) | C = 1 |
| LO | Unsigned < (“LOwer”) | C = 0 |
| HI | Unsigned > (“HIgher”) | C = 1 && Z = 0 |
| LS | Unsigned ≤ (“Lower or Same”) | C = 0 || Z = 1 |
| GE | Signed ≥ (“Greater than or Equal”) | N = V |
| LT | Signed < (“Less Than”) | N ≠ V |
| GT | Signed > (“Greater Than”) | Z = 0 && N = V |
| LE | Signed ≤ (“Less than or Equal”) | Z = 1 || N ≠ V |
| CS | Carry Set (synonym for HS) | C = 1 |
| CC | Carry Clear (synonym for LO) | C = 0 |
| MI | MIus negative | N = 1 |
| PL | PLus –positive or zero (non-negative) | N = 0 |
| VS | oVerflow Set | V = 1 |
| VC | oVerflow Clear | V = 0 |
| AL | **AL**ways (unconditional) | (Rarely used) |

continues sequentially with whatever instruction immediately follows the BEQ. The “EQ” in BEQ is called a condition code; there are 15 possible condition codes as summarized in Table 7-2.

Eight of the condition codes are used much more frequently than others and are indicated in bold in the table. EQ and NE are used for equality and inequality tests. The codes for relative magnitude tests depend on whether the operands are signed or unsigned; condition codes GE, LT, GT, and LE are used with signed operands, while HS, LO, HI and LS are used with unsigned operands.

If you are not sure why two separate sets of condition codes for relative magnitude comparisons are necessary, then ask yourself which is greater: 11012 or 01112. As 4-bit unsigned values, they represent decimal 13 and 7 so that 11012 > 01112; however, as 4-bit signed 2’s-complement values, they represent –3 and +7 so that 11012 < 01112.

# 7.2.2 If-Then and If-Then-Else Statements

Consider the following simple C if-then statement shown in Figure 7-2. Since the C code uses an equality comparison (==), you may be tempted to use a BEQ instruction in assembly. If you do, you will have to add an unconditional branch around the two