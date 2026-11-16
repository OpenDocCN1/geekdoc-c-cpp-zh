| C Source Code | Assembly Code |
|---|---|
| signed int a,b,c; | LDR R0, a ; is a > 0? |
| | CMP R0, #0 |
| if (a > 0) b = 1; | ITT GT ; controls 4 instructions |
| else c = 2; | LD RGT R0,=1 ; yes: b ← 1 |
| | ST RGT R0,b |
| | LD RLE R0,=2 ; no: c ← 2 |
| | ST RLE R0,c |

FIGURE 7-5 Speeding up an if-then-else statement with an IT block.

The first instruction in the IT block is enabled if the condition code given in the operand field of the IT instruction is true. The remaining instructions in the block are controlled by appending one to three letters to the IT mnemonic. If the letter is a “T” (“then”), the condition code enables the corresponding instruction; if the letter is an “E” (“else”), the opposite of the condition code enables the instruction. All instructions in the IT block must have their enabling condition code appended to their mnemonic.⁶

An instruction within an IT block may modify the flags, but has no effect on whether the remaining instructions in the block are enabled or disabled.

There are three fundamental restrictions regarding IT blocks:

+   1. An IT block may not contain an IT, CBZ, CBNZ, CPSID, or CPSIE instruction.⁷
+   2. Instructions that modify the PC may be used only as the last instruction of the block.
+   3. A branch to an instruction within an IT block is not allowed.

# 7.3 IMPLEMENTING LOOPS

Loops generally consist of four parts: initialization, test for completion (or continuation), update of the loop control variables, and the body of the loop (the code to be repeated). Sometimes the update is part of the body of the loop. Loops may be distinguished by whether their test for completion is placed before or after the body of the loop. For and while loops test for completion before each iteration and thus repeat zero or more times; do-while loops test after each iteration and always repeat at least once.

Some loops repeat for a fixed number of iterations, specified by either a constant or the value of a variable, such as finding the factorial of a number or computing the average of a set of values. Others repeat until some condition is satisfied that depends on values computed during the loop, such as finding the greatest common divisor (GCD) of two integers or the convergence test in a series approximation.

⁶ All ARM processors use a single unified assembly language (UAL). Unlike Thumb-2 instructions, appending a condition code to a regular ARM instruction makes its execution conditional without the need for an IT instruction. When assembled for a regular ARM processor, the IT instruction is ignored, and the seemingly redundant requirement for condition codes appended to instructions within the IT block allows the same source code to be used for regular ARM and Thumb-2 code.
⁷ CPSID is used to disable interrupts and CPSIE to enable them.