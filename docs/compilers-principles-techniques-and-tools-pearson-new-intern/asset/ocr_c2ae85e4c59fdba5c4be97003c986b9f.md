| Block B | OUT[B]⁰ | IN[B]¹ | OUT[B]¹ | IN[B]² | OUT[B]² |
|---|---|---|---|---|---|
| B₁ | 000 0000 | 000 0000 | 111 0000 | 000 0000 | 111 0000 |
| B₂ | 000 0000 | 111 0000 | 001 1100 | 111 0111 | 001 1110 |
| B₃ | 000 0000 | 001 1100 | 000 1110 | 001 1110 | 000 1110 |
| B₄ | 000 0000 | 001 1100 | 001 0111 | 001 1110 | 001 0111 |
| EXIT | 000 0000 | 001 0111 | 001 0111 | 001 0111 | 001 0111 |

Figure 9.15: Computation of IN and OUT

we now know there is a change on the first round (and will proceed to a second round).

Then we consider *B = B₂* and compute

IN[B₂]¹ = OUT[B₁]¹ ∪ OUT[B₄]⁰
= 111 0000 + 000 0000 = 111 0000
OUT[B₂]¹ = gen<sub>B₂</sub> ∪ (IN[B₂]¹ − kill<sub>B₂</sub>)
= 000 1100 + (111 0000 − 110 0001) = 001 1100

This computation is summarized in Fig. 9.15. For instance, at the end of the first pass, OUT[B₂]¹ = 001 1100, reflecting the fact that d₄ and d₅ are generated in B₂, while d₃ reaches the beginning of B₂ and is not killed in B₂.
Notice that after the second round, OUT[B₂] has changed to reflect the fact that d₆ also reaches the beginning of B₂ and is not killed by B₂. We did not learn that fact on the first pass, because the path from d₆ to the end of B₂, which is B₃ → B₄ → B₂, is not traversed in that order by a single pass. That is, by the time we learn that d₆ reaches the end of B₄, we have already computed IN[B₂] and OUT[B₂] on the first pass.
There are no changes in any of the OUT sets after the second pass. Thus, after a third pass, the algorithm terminates, with the IN’s and OUT’s as in the final two columns of Fig. 9.15. □

# 9.2.5  Live-Variable Analysis

Some code-improving transformations depend on information computed in the direction opposite to the flow of control in a program; we shall examine one such example now. In *live-variable analysis* we wish to know for variable *x* and point *p* whether the value of *x* at *p* could be used along some path in the flow graph starting at *p*. If so, we say *x* is live at *p*; otherwise, *x* is dead at *p*.

An important use for live-variable information is register allocation for basic blocks. Aspects of this issue were introduced in Sections 8.6 and 8.8. After a value is computed in a register, and presumably used within a block, it is not