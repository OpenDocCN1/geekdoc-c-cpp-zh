# Turing-Completeness ■ 103

```
READ ar MEM[ar] LOADED FROM INPUT
READ @ar MEM[MEM[ar]] := INPUT
WRITE ar MEM[ar] MOVED TO OUTPUT
ADD ar1, ar2, ar3 MEM[ar3] := MEM[ar1]+MEM[ar2]
ADD @ar1, ar2, @ar3 MEM[MEM[ar3]] =
MEM[MEM[ar1]]+MEM[ar2]
MEM[ar3] := MEM[ar1]/2
SHFT ar MEM[ar1] = MEM[ar1] * 2
JMP C PC = C
JPOS ar C IF MEM[ar] > 0, PC = C
```

The Turing machine to emulate this computer will have several tapes:

+   - Tape 1: PC (holds one address, which can be arbitrarily long)
- Tape 2: Address tape, used for fetching operands (holds up to three addresses)
- Tape 3: Memory, stored in the form of (address, contents) (unlimited number of pairs)
- Tape 4: Input tape (holds whatever the standard input device would contain (unlimited))
- Tape 5: Output tape (TM writes all output to this tape) (unlimited)
- Tape 6: Scratch work tape, if desired (unlimited)

Example: ADD 23, @45, 96

+   - 1. Write 23 onto tape 2, the address tape.
- 2. Scan the memory tape until the number 23 is found; replace 23 with contents onto tape 2.
- 3. Write @45 onto tape 2 (following the number written in step 2).
- 4. Scan memory tape until 45 is found; copy its contents onto tape 2 (replace the 45).
- 5. Find this cell on the memory tape; replace address address its contents.
- 6. Add these two numbers, using the scratch tape if desired.
- 7. Find cell 96 on the memory tape.
- 8. Replace its contents by the sum from tape 2 (perhaps moving tape over to make room).