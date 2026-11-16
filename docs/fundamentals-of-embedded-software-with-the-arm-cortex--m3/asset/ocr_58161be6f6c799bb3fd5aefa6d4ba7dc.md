instructions that are the then clause. Instead, a more efficient solution is to use the BNE instruction to eliminate the unconditional branch:

| C Source Code | Inefficient Assembly | Efficient Assembly |
|---|---|---|
| int32_t a, b ; | LDR R0, a | LDR R0, a |
| if (a == 0) b = 1 ; | CMP R0, #0 | CMP R0, #0 |
| | BEQ Then | BNE EndIf |
| | B EndIf | Then: LDR R0, =1 |
| | Then: LDR R0, =1 | STR R0, b |
| | STR R0, b | EndIf: ... |
| | EndIf: ... | |

FIGURE 7-2 Converting an if-then statement to assembly.

It is important to realize that when a decision is made in assembly, the only possible action is to branch. In other words, to get closer to what is actually done in assembly, we should imagine that the if statement has been rearranged so that the action controlled by the if statement is a goto, which then requires that we reverse the sense of the comparison:

if (a != 0) goto L1 ;
b = 1 ;
L1:

When coding a relative magnitude comparison, it is important to remember that the opposite of “less than” is NOT “greater than.” If a condition includes the equality case, then the opposite condition must not, and vice versa!

Figure 7-3 illustrates how an else-if statement is translated into assembly. When an else is added, an unconditional branch must always be included. As shown in Figure 7-4, the unconditional branch must immediately follow the then clause (b = 1;) in order to skip over the else (c = 2;) so that only one of the two will be executed. If omitted, the code simply will not work as intended.

| C Source Code | Incorrect Assembly | Correct Assembly |
|---|---|---|
| int32_t a, b ; | LDR R0, a | LDR R0, a |
| if (a < 100) b = 1 ; | CMP R0, #100 | CMP R0, #100 |
| | BGT L1; #NO! | BGE L1 |
| | LDR R0, =1 | LDR R0, =1 |
| | STR R0, b | STR R0, b |
| | L1: ... | L1: ... |

FIGURE 7-3 Correctly choosing the opposite condition code.