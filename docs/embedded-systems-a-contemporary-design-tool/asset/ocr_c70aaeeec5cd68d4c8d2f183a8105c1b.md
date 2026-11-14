| Operator | Operation |
| :--- | :--- |
| ← | Transfer from right-hand side to left-hand side |
| → | If-then operation |
| [index] | Select word from memory at index |
| <index> | Select bit or bits from register at index or range |
| i,j | Index range |
| := | Text substitution |
| # | Concatenation |
| : | Separator for parallel operations |
| . | Separator for sequential operations |
| @ | Replication |
| { } | Information about operation |
| ( ) | Grouping |
| = ≤ < ≥ > | Comparison operators |
| + − × ÷ | Arithmetic operators |
| ∧ ∨ ¬ ⊕ ≡ | Logical operators |

Table 1.4 illustrates how representative operations from the ISA level can be expressed using RTN.

| Type | Instruction | ISA level | Register transfer level |
| :--- | :--- | :--- | :--- |
| Data transfer | Move register | MOVE R1, R2 | R1 ← R2 |
| | Move from memory | MOVE R1, memax | R1 ← (memax) |
| | Move to memory | MOVE memax, R1 | (memax) ← R1 |
| | Move immediate | MOVE R1, #DEAD | R1 ← #DEAD |
| Control flow | Unconditional branch | BR $1 | PC ← $1 |
| | Conditional branch | BNE $1 | cond (PC ← $1) if(cond) PC ← $1 |
| Logic | Complement accumulator | CMA | A ← ~A |
| | AND register | AND R1, R2 | R1 ← R1 ∧ R2 |
| | OR register | OR R1, R2 | R1 ← R1 ∨ R2 |
| | Shift register | SHL R1, #3 | R1 < 31-n..0>n@(0) Contents of R1 get replaced by bits in range of 31-n..0, where n is number of bits to shift and n 0s get extended on right |
| Arithmetic | ADD register with carry | ADDC R1, R2 | R1 ← R1 + R2 + C |
| | Clear carry | CLRC | C ← 0 |
| Program control | Don't execute an instruction | NOP | PC ← (PC + 1) |
| | Stop executing instructions | HALT | PC ← PC |