+   4. In the case where the input value of a variable m(v) is used on the right-hand-side of a symbolic map in region R_i and m(v) = NAA upon entry to the region, we introduce a new reference variable t, add assignment τ = v to the beginning of region R_i, and all references of m(v) are replaced by t. If we did not introduce a reference variable at this point, the NAA value held by v would penetrate into inner loops.

f_{R3,j,IN[B3]} = f_{B3}^{j-1}
f_{R5,j,OUT[B3]} = f_{B3}^{j}

f_{R5,IN[B2]} = I
f_{R5,IN[R3]} = f_{B2}
f_{R5,OUT[B4]} = I ∘ f_{R5,10,OUT[B3]} ∘ f_{B2}

f_{R7,i,IN[R6]} = f_{R6,OUT[B4]}^{-1}
f_{R7,i,OUT[B4]} = f_{R6,OUT[B4]}

f_{R8,IN[B1]} = I
f_{R8,IN[R7]} = f_{B1}
f_{R8,OUT[B4]} = f_{R7,100,OUT[B4]} ∘ f_{B1}

Figure 9.62: Transfer function relations in the bottom-up pass for Example 9.58.

**Example 9.64 :** For Example 9.58, we show how the transfer functions for the program are computed in the bottom-up pass in Fig. 9.62. Region R5 is the inner loop, with body B5. The transfer function representing the path from the entry of region R5 to the beginning of the jth iteration, j ≥ 1, is f_{B5}^{j-1}. The transfer function representing the path to the end of the jth iteration, j ≥ 1, is f_{B5}^{j}.

Region R6 consists of blocks B2 and B4, with loop region R5 in the middle. The transfer functions from the entry of B2 and R5 can be computed in the same way as in the original algorithm. Transfer function f_{R6,OUT[B3]} represents the composition of block B2 and the entire execution of the inner loop, since f_{B4} is the identity function. Since the inner loop is known to iterate 10 times, we can replace j by 10 to summarize the effect of the inner loop precisely. The