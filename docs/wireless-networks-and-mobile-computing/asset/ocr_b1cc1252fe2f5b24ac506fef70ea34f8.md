$v = 2^i + 2^{i+1} + 2^{i+2} + \dots + 2^{k+i-1}.$  (8.1)

Alternatively, we can rewrite Equation (8.1) as,

$v = 2^{k+i} - 2^i.$  (8.2)

Equation (8.2) can be represented in RBNS by a 1 at bit position $(k+i)$ and a $\bar{1}$ at bit position $i$, while all the intermediate 1’s between them are converted to 0’s. We formalize this observation in the form of the following reduction rule.

**Reduction 1.** *A run of $k$ 1’s ($k > 1$) starting from bit position $i$, is replaced by an equivalent representation consisting of a 1 at bit position $k+i$ and a $\bar{1}$ at bit position $i$, with 0’s in all intermediate bit positions.*

Observe that for a run of $k$ 1’s, $k > 1$, the savings in terms of the number of non-zero digits is $k-2$. Note that the number of non-zero digits remains unchanged for $k = 2$. Also, if we consider a string, say 110111, with only one 0 trapped between runs of 1’s, after applying reduction rule 1, we would get the string $10\bar{1}1001$. Note the presence of the pattern $\bar{1}1$ for this trapped 0. A second reduction can now be applied to the bit pattern $\bar{1}1$ to replace it with $0\bar{1}$. Thus, from $10\bar{1}100\bar{1}$, we get the string $100\bar{1}00\bar{1}$ with fewer non-zero digits. We thus have a second reduction rule.

**Reduction 2.** *Every occurrence of the bit pattern $\bar{1}1$ in a string obtained after applying reduction rule 1 is replaced by the equivalent bit pattern $0\bar{1}$.*

The application of reduction rules 1 and 2 warrants a two-pass algorithm. However, it is easy to combine the two rules to obtain a single-pass algorithm, as stated below.

```
1: procedure RBNSiZeCom(IN bit vector data_frame, IN integer len)
2:     /* The data frame is converted to RBNS */
```