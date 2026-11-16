Example 1.5.6 Let $C$ be the $[6, 3, 2]$ binary code with generator matrix

$$ G = \begin{bmatrix} 1 & 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 1 & 1 & 1 \\ 0 & 0 & 1 & 1 & 1 & 1 \end{bmatrix} $$

$C^\perp$ is also a $[6, 3, 2]$ code with generator matrix

$$ G^\perp = \begin{bmatrix} 1 & 1 & 1 & 1 & 0 & 0 \\ 1 & 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 \end{bmatrix} $$

If the coordinates are labeled $1, 2, \dots, 6$, let $T = \{5, 6\}$. Generator matrices for the shortened code $C_T$ and punctured code $C^T$ are

$$ G_T = \begin{bmatrix} 1 & 0 & 1 & 0 \\ 0 & 1 & 1 & 0 \\ 0 & 1 & 1 & 0 \end{bmatrix} \text{ and } G^T = \begin{bmatrix} 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 \end{bmatrix} $$

Shortening and puncturing the dual code gives the codes $(C^\perp)_T$ and $(C^\perp)^T$, which have generator matrices

$$ (G^\perp)_T = [1 \ 1 \ 1 \ 1] \text{ and } (G^\perp)^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 0 \end{bmatrix} $$

From the generator matrices $G_T$ and $G^T$, we find that the duals of $C_T$ and $C^T$ have generator matrices

$$ (G_T)^\perp = \begin{bmatrix} 1 & 1 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \text{ and } (G^T)^\perp = [1 \ 1 \ 1 \ 1] $$

Notice that these matrices show that $(C^\perp)_T = (C^T)^\perp$ and $(C^\perp)^T = (C_T)^\perp$.

The conclusions observed in the previous example hold in general.

# **Theorem 1.5.7** Let $C$ be an $[n, k, d]$ code over $\mathbb{F}_q$. Let $T$ be a set of $t$ coordinates. Then:
(i) $(C^\perp)_T = (C^T)^\perp$ and $(C^\perp)^T = (C_T)^\perp$,
(ii) if $t < d$, then $C_T$ and $(C^\perp)^T$ have dimensions $k$ and $n - t - k$, respectively;
(iii) if $t = d$ and $T$ is the set of coordinates where a minimum weight codeword is nonzero, then $C^T$ and $(C^\perp)_T$ have dimensions $k - 1$ and $n - d - k + 1$, respectively.

**Proof.** Let $c$ be a codeword of $C^\perp$ which is $\mathbf{0}$ on $T$ and $c^*$ the codeword with the coordinates in $T$ removed. So $c^* \in (C^\perp)_T$. If $\mathbf{x} \in C$, then $\mathbf{0} = \mathbf{x} \cdot \mathbf{c} = \mathbf{x}^* \cdot \mathbf{c}^*$, where $\mathbf{x}^*$ is the codeword $\mathbf{x}$ punctured on $T$. Thus $(C^\perp)_T \subseteq (C^T)^\perp$. Any vector $\mathbf{c} \in (C^T)^\perp$ can be extended to a vector $\tilde{\mathbf{c}}$ by inserting 0s in the positions of $T$. If $\mathbf{x} \in C$, punctrue $\mathbf{x}$ on $T$ to obtain $\mathbf{x}^*$. As $\mathbf{0} = \mathbf{x}^* \cdot \mathbf{c} = \mathbf{x} \cdot \tilde{\mathbf{c}}$, $\tilde{\mathbf{c}} \in (C^\perp)_T$. Thus $(C^T)^\perp = (C^\perp)_T$. Replacing $C$ by $C^\perp$ gives $(C^\perp)^T = (C_T)^\perp$, completing (i).

Assume $t < d$. Then $n - d + 1 \le n - t$, implying any $n - t$ coordinates of $C$ contain an information set by Theorem 1.4.15. Therefore $C^T$ must be $k$-dimensional and hence $(C^\perp)_T = (C^T)^\perp$ has dimension $n - t - k$ by (i); this proves (ii).