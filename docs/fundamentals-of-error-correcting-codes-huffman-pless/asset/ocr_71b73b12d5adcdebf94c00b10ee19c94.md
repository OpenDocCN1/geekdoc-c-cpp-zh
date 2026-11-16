Proof: Part (i) is a restatement of Theorem 2.3.1. In an $(n, M, 2w)$ constant weight code $\mathcal{C}$ over $\mathbb{F}_q$ with codewords of weight $w$, no two codewords can have the same nonzero entries in the same coordinate. Thus if $\mathcal{M}$ is the $M \times n$ matrix whose rows are the codewords of $\mathcal{C}$, each column of $\mathcal{M}$ can have at most $q-1$ nonzero entries. So $\mathcal{M}$ has at most $n(q-1)$ nonzero entries. However, each row of $\mathcal{M}$ has $w$ nonzero entries and so $Mw \le n(q-1)$. This gives (ii). For (iii), let $\mathcal{C} = \{e_1, \dots, e_M\}$, where $M = \lfloor n/w \rfloor$ and $e_i$ is the vector of length $n$ consisting of $(i-1)0$s followed by $w$ 1s followed by $n-iw$ 0s, noting that $n-Mw \ge 0$. Clearly $\mathcal{C}$ is a constant weight binary $(n, \lfloor n/w \rfloor, 2w)$ code. The existence of this code and part (ii) with $q=2$ give (iii). Part (iv) is left for Exercise 97.

Exercise 97. Show that two binary codewords of the same weight must have even distance between them. Then use this to show that $A_2(n, 2e-1, w) = A_2(n, 2e, w)$.

# 2.3.1 The Restricted Johnson Bound

We consider two bounds on $A_q(n, d, w)$, the first of which we call the Restricted Johnson Bound.

# Theorem 2.3.4(Restricted Johnson Bound for $A_q(n, d, w)$)

$A_q(n, d, w) \le \left\lfloor \frac{nd(q-1)}{qw^2 - 2(q-1)nw + nd(q-1)} \right\rfloor$

provided $qw^2 - 2(q-1)nw + nd(q-1) > 0$, and

$A_2(n, d, w) \le \left\lfloor \frac{nd}{2w^2 - 2nw + nd} \right\rfloor$

provided $2w^2 - 2nw + nd > 0$.

Proof: The second bound is a special case of the first. The proof of the first uses the same ideas as in the proof of the Plotkin Bound. Let $\mathcal{C}$ be an $(n, M, d)$ constant weight code with codewords of weight $w$. Let $\mathcal{M}$ be the $M \times n$ matrix whose rows are the codewords of $\mathcal{C}$. Let

$S = \sum_{\mathbf{x} \in \mathcal{C}} \sum_{\mathbf{y} \in \mathcal{C}} d(\mathbf{x}, \mathbf{y}).$

If $\mathbf{x} \neq \mathbf{y}$ for $\mathbf{x}, \mathbf{y} \in \mathcal{C}$, then $d \le d(\mathbf{x}, \mathbf{y})$ implying that

$M(M-1)d \le S.$ (2.7)

For $1 \le i \le n$, let $n_{i,\alpha}$ be the number of times $\alpha \in \mathbb{F}_q$ occurs in column $i$ of $\mathcal{M}$. So

$S = \sum_{i=1}^n \sum_{\alpha \in \mathbb{F}_q} n_{i,\alpha}(M - n_{i,\alpha}) = \sum_{i=1}^n (Mn_{i,0} - n_{i,0}^2) = \sum_{i=1}^n \sum_{\alpha \in \mathbb{F}_q} (Mn_{i,\alpha} - n_{i,\alpha}^2).$ (2.8)