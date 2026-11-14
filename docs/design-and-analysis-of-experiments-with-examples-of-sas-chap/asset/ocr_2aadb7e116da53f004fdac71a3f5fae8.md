tests on all other effects and interactions in the model is the mean square for the split-plot error term.

| Source | df | Type III Expected Mean Square |
| :--- | :--- | :--- |
| Block | 1 | \(\sigma^2 + 4\sigma_W^2 + 16\sigma_B^2\) |
| A | 1 | \(\sigma^2 + 4\sigma_W^2 + Q(A, AB, AC, AD, ABC, ABD, ACD, ABCD)\) |
| B | 1 | \(\sigma^2 + 4\sigma_W^2 + Q(B, AB, BC, BD, ABC, ABD, BCD, ABCD)\) |
| AB | 1 | \(\sigma^2 + 4\sigma_W^2 + Q(AB, ABC, ABD, ABCD)\) |
| Whole Plot | 3 | \(\sigma^2 + 4\sigma_W^2\) |
| Error | | |
| C | 1 | \(\sigma^2 + Q(C, CD, AC, BC, ABC, ACD, BCD, ABCD)\) |
| D | 1 | \(\sigma^2 + Q(D, CD, AD, BD, ABD, ACD, BCD, ABCD)\) |
| CD | 1 | \(\sigma^2 + Q(CD, ACD, BCD, ABCD)\) |
| AC | 1 | \(\sigma^2 + Q(AC, ABC, ACD, ABCD)\) |
| AD | 1 | \(\sigma^2 + Q(AD, ABD, ACD, ABCD)\) |
| BC | 1 | \(\sigma^2 + Q(BC, ABC, BCD, ABCD)\) |
| BD | 1 | \(\sigma^2 + Q(BD, ABD, BCD, ABCD)\) |
| ABC | 1 | \(\sigma^2 + Q(ABC, ABCD)\) |
| ABD | 1 | \(\sigma^2 + Q(ABD, ABCD)\) |
| ACD | 1 | \(\sigma^2 + Q(ACD, ABCD)\) |
| BCD | 1 | \(\sigma^2 + Q(BCD, ABCD)\) |
| ABCD | 1 | \(\sigma^2 + Q(ABCD)\) |
| Split-Plot | 12 | \(\sigma^2\) |
| Error | | |

The commands for the analysis using proc mixed are shown below.

```
proc mixed data=sausage;
   class A B Block C D;
   model y=A B A*B C D C*D A*C A*D B*C B*D A*B*C A*B*D
      A*C*D B*C*D A*B*C*D;
   random A*Block Block(A*B);
   lsmeans A;
   lsmeans C;
   lsmeans A*B*C;
   run;
```