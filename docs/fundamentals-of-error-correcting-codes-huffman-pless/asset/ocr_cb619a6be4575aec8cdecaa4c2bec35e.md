$\mathbb{F}_4$ given by both $\mu_{-1}$ and $\mu_2$. Finally, if $p = 73$, $\text{ord}_p(2) = 9$ and there is some splitting of 73 over $\mathbb{F}_2$ given by both $\mu_{-1}$ and $\mu_{-2}$; there is also some splitting of 73 over $\mathbb{F}_4$ given by both $\mu_{-1}$ and $\mu_{-2}$.

# **Exercise 350** Find the splittings alluded to in Example 6.4.11. Also, what are the other splittings and what multipliers give them?

**Exercise 351** This exercise explains part of Theorem 6.4.10. In Section 6.6 we will discuss quadratic residue codes over $\mathbb{F}_q$, which are merely duadic codes of odd prime length $p$ with splittings over $\mathbb{F}_q$ given by $S_1 = \mathcal{Q}_p$ and $S_2 = \mathcal{N}_p$, where $\mathcal{Q}_p$ are the nonzero squares and $\mathcal{N}_p$ the nonsquares in $\mathbb{F}_p$. Binary quadratic residue codes exist if $p \equiv \pm 1 \pmod 8$; quadratic residue codes over $\mathbb{F}_4$ exist for any odd prime $p$. Do the following:

+   (a) Show that in $\mathbb{F}_p$, the product of two squares or two nonsquares is a square.
+   (b) Show that in $\mathbb{F}_p$ the product of a square and a nonsquare is a nonsquare.
+   (c) Show that if $p \equiv 1 \pmod 8$, then $-1, 2, \text{and } -2$ are all squares in $\mathbb{F}_p$.
+   (d) Prove that if $p \equiv 1 \pmod 8$, the splitting $S_1 = \mathcal{Q}_p$ and $S_2 = \mathcal{N}_p$ over $\mathbb{F}_p$ cannot be given by either $\mu_{-1}$ or $\mu_{-2}$.

We now consider odd-like duadic codes over $\mathbb{F}_q$. Recall that if $\mathcal{D}$ is an odd-like code of length $n$, the ordinary extension $\widehat{\mathcal{D}}$ of $\mathcal{D}$ is defined by $\widehat{\mathcal{D}} = \{ \widehat{\mathbf{c}} \mid \mathbf{c} \in \mathcal{D} \}$ where $\widehat{\mathbf{c}} = \mathbf{c} c_0 c_1 \cdots c_{p-1} c_\infty$ and

$c_\infty = - \sum_{j=0}^{p-1} c_j$.

Since the odd-like duadic codes are $[n, (n+1)/2]$ codes by Theorem 6.1.3(v), the extended codes would be $[n+1, (n+1)/2]$ codes. Hence these codes could potentially be self-dual. If $\mathcal{D}$ is an odd-like duadic code, $\mathcal{D}$ is obtained from its even-like subcode $\mathcal{C}$ by adding $\bar{j}(x)$ to a basis of $\mathcal{C}$. But $\bar{j}(x)$ is merely a multiple of the all-one vector $\mathbf{1}$, and so if we want to extend $\mathcal{D}$ in such a way that its extension is either self-dual or dual to the other extended-like duadic code, then we must extend $\mathbf{1}$ in such a way that it is orthogonal to itself. The ordinary extension will not always yield this. However, the next result shows that we can modify the method of extension for $\mathcal{D}_1$ and $\mathcal{D}_2$ under $\mu_{-1}$ gives the splitting and the equation

$1 + \gamma^2 n = 0$

has a solution in $\mathbb{F}_q$. Let $\mathcal{D}$ be an odd-like duadic code and suppose (6.11) has a solution. If $\mathbf{c} = c_0 c_1 \cdots c_{n-1} \in \mathcal{D}$, let $\bar{\mathbf{c}} = c_0 c_1 \cdots c_{n-1} c_\infty$, where

$c_\infty = -\gamma \sum_{i=0}^{n-1} c_i$.

The new extension of $\mathcal{D}$ is defined by $\tilde{\mathcal{D}} = \{ \tilde{\mathbf{c}} \mid \mathbf{c} \in \mathcal{D} \}$. Notice that the codes $\widehat{\mathcal{D}}$ and $\tilde{\mathcal{D}}$ are monomially equivalent because $\tilde{\mathcal{D}} = \widehat{\mathcal{D}}D$, where $\mathcal{D}$ is the $(n+1) \times (n+1)$ diagonal matrix $D = \text{diag}(1, 1, \dots, 1, \gamma)$.