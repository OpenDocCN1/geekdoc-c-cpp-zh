# 248

# 8.3 The reductions

The reduction maps an instance $(G = (V, E), s, t)$ of RUDRATA $(s, t)$-PATH into an instance $G' = (V', E')$ of RUDRATA CYCLE as follows: $G'$ is simply $G$ with an additional vertex $x$ and two new edges $(s, x)$ and $(x, t)$. For instance:

![](bbox=[0.068, 0.143, 0.703, 0.252])

So $V' = V \cup \{x\}$ and $E' = E \cup \{s, x\}, \{x, t\}$. How do we recover a Rudrata $(s, t)$-path in $G$ given any Rudrata cycle in $G$? Easy, just delete the edges $\{s, x\}$ and $\{x, t\}$ from the cycle.

# RUDRATA $(s, t)$-PATH

| Instance $G = (V, E)$ nodes $s, t$ | $G' = (V', E')$ RUDRATA CYCLE | Solution: cycle Delete edges $\{s, x\}, \{x, t\}$ | Solution: path |
|---|---|---|---|n| | Add node $x$ and edges $\{s, x\}, \{x, t\}$ | | No solution | No solution |

To confirm the validity of this reduction, we have to show that it works in the case of either output being decided.

+   1. When the instance of RUDRATA CYCLE has a solution.

Since the new vertex $x$ has two neighbors, $s$ and $t$, and any Rudrata cycle in $G'$ must consecutively traverse the edges $\{t, x\}$ and $\{x, s\}$. The rest of the cycle then traverses every other vertex from $s$ to $t$. Thus deleting the two edges $\{t, x\}$ and $\{x, s\}$ from the Rudrata cycle gives a Rudrata path from $s$ to $t$ in the original graph $G$.
2. When the instance of RudR CYCLE does not have a solution.
In this case we show that the original instance of RUDRATA $(s, t)$-PATH cannot have a solution either. It is easier to prove the contrapositive, that is, to show that if there is a Rudrata $(s, t)$-path in $G$, then there is also a Rudrata cycle in $G'$. But this is easy: just add the two edges $\{t, x\}$ and $\{x, s\}$ to the Rudrata path to close the cycle.

One last detail, but crucially easy to check, that the pre- and postprocessing functions take polynomial in the size of the instance $(G, s, t)$.

It is also possible to go in the other direction and reduce RUDR CYCLE to RUDRATA $(s, t)$-PATH. Together, these reductions demonstrate that the two Rudrata variants are in the same problem—which is not too surprising, given that their