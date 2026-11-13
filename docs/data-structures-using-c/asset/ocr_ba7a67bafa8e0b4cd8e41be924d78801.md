Tabel 3.4 (Continued)

(b) Stacking of the × operator

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| + | + | A |
| B | + | AB |
| × | +× | AB |
| C | +× | ABC |
| # (Pop all) | +× | ABC ×+ |

In addition, when the input is exhausted, we should output all remaining operators in the stack to get the postfix expression as ABC×+.

Let us consider one more example. The infix expression A × (B + C) × D, after conversion, should generate the postfix expression ABC + × D ×, and hence, the sequence of operations should be as shown in Table 3.5.

Table 3.5 Infix to postfix conversion of the expression A × (B + C) × D

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| × | × | A |
| ( | ×( | A |
| B | ×( | AB |
| + | ×(+ | AB |
| C | ×(+ | ABC |

(Continued)

At this point, unstack the corresponding left parenthesis and then delete the left and right parentheses; this should give the stack contents as follows:

Table 3.5 (Continued)

| Next character | Stack | Output |
|---|---|---|
| ) | × | ABC+ |
| × | × | ABC+× |
| D | × | ABC+× D |
| Done | Empty | ABC+× D× |

From these examples and discussion, we can say that the operators are popped out of the stack if their in-stack priority (ISP) is greater than the priority of the incoming operator that is to be added onto the stack.