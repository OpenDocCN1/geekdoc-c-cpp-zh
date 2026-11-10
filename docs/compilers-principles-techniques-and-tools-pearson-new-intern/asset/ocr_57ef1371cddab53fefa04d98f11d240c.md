# 9.8. SYMBOLIC ANALYSIS

+   4. In the case where the input value of a variable $m(v)$ is used on the right-hand-side of a symbolic map in region $R_i$ and $m(v) = NAA$ upon entry to the region, we introduce a new reference variable $t$, add assignment $τ = v$ to the beginning of region $R_i$, and all references of $m(v)$ are replaced by $t$. If we did not introduce a reference variable at this point, the NAA value held by $v$ would penetrate into inner loops.

```
f_{R_5,j,IN[B_3]} = f_{B_3}^{j-1}
f_{R_5,j,OUT[B_3]} = f_{B_3}^{j}

f_{R_5,IN[B_2]} = I
f_{R_5,IN[R_3]} = f_{B_2}
f_{R_5,OUT[B_4]} = I ∘ f_{R_5,10,OUT[B_3]} ∘ f_{B_2}

f_{R_7,i,IN[R_6]} = f_{R_6,OUT[B_4]}^{-1}
f_{R_7,i,OUT[B_4]} = f_{R_6,OUT[B_4]}

f_{R_8,IN[B_1]} = I
f_{R_8,IN[R_7]} = f_{B_1}
f_{R_8,OUT[B_4]} = f_{R_7,100,OUT[B_4]} ∘ f_{B_1}
```

Figure 9.62: Transfer function relations in the bottom-up pass for Example 9.58.

**Example 9.64:** For Example 9.58, we show how the transfer functions for the program are computed in the bottom-up pass in Fig. 9.62. Region $R_5$ is the inner loop, with body $B_3$. The transfer function representing the path from the entry of region $R_5$ to the beginning of the $j$th iteration, $j ≥ 1$, is $f_{B_3}^{j-1}$. The transfer function representing the path to the end of the $j$th iteration, $j ≥ 1$, is $f_{B_3}^{j}$.
    Region $R_6$ consists of blocks $B_2$ and $B_1$, with loop region $R_5$ in the middle. The transfer functions from the entry of $B_2$ and $R_5$ can be computed in the same way as in the original algorithm. Transfer function $f_{R_6,OUT[B_3]}$ represents the composition of block $B_2$ and the entire execution of the inner loop, since $f_{B_4}$ is the identity function. Since the inner loop is known to iterate 10 times, we can replace $j$ by 10 to summarize the effect of the inner loop precisely. The