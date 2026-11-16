
### Exercise 755 Show that the generator matrices in Examples 12.2.5 and 12.7.3 generate the same $\mathbb{Z}_4$-linear code.

We now use the relative trace to list all the codewords in $K(r+1)$ and $\widehat{K}(r+1)$. Let $\mathbf{I}_n$ denote the all-one vector of length $n$.

### Lemma 12.7.4 Let $r \ge 2$ and $n = 2^r - 1$. Then $\mathbf{c} \in K(r+1)$ if and only if there exists $\lambda \in \mathcal{R} = \text{GR}(4^r)$ and $\epsilon \in \mathbb{Z}_4$ such that

$$\mathbf{c} = (\text{TR}(\lambda), \text{TR}(\lambda\xi), \text{TR}(\lambda\xi^2), \dots, \text{TR}(\lambda\xi^{n-1})) + \epsilon \mathbf{I}_n.$$ (12.23)

The parity check for $\mathbf{c}$ is $\epsilon$.

**Proof:** Using Exercise 755, $\sum_{i=0}^{n-1} (\text{TR}_r(\lambda \xi^i) + \epsilon) = \text{TR}_r(\lambda \sum_{i=0}^{n-1} \xi^i) + (2^r - 1)\epsilon = \text{TR}_r(\lambda \frac{\xi^n - 1}{\xi - 1}) + (2^r - 1)\epsilon \equiv (\text{TR}_r(0) + (2^r - 1)\epsilon \equiv (2^r - 1)\epsilon \equiv 3\epsilon \text{ (mod 4)}$. So the parity check for $\mathbf{c}$ is $\epsilon$.

Let $\mathcal{C} = \{(\text{TR}(\lambda), \text{TR}(\lambda\xi), \text{TR}(\lambda\xi^2), \dots, \text{TR}(\lambda\xi^{n-1})) + \epsilon \mathbf{I}_n \mid \lambda \in \text{GR}(4^r), \epsilon \in \mathbb{Z}_4\}$. We first show that $\mathcal{C}$ has $4^{r+1}$ codewords; this is clear if we show that $\text{TR}_r(\lambda \xi^i) + \epsilon = \text{TR}_r(\lambda_1 \xi^i) + \epsilon_1$ for $0 \le i \le n-1$ implies $\lambda = \lambda_1$ and $\epsilon = \epsilon_1$. But $\epsilon = \epsilon_1$ since the parity check of $\mathbf{c}$ is $\epsilon$. Therefore by Exercise 753, $\text{TR}_r(\xi^i) = 0$ for $0 \le i \le n-1$ where $\lambda = \lambda - \lambda_1$. We only need to show that $\xi = 0$. Since $\text{TR}_r(\xi^i) = 0$, $\text{TR}_r(\xi^{2i}) = 0$ for $0 \le i \le n-1$ where $\lambda = \lambda - \lambda_1$.

We now show that $\epsilon$ can have the form in (12.23), then $\mathbf{c} \in K(r+1)$. Since $\mathbf{I}_n \in K(r+1)$, we only need to show that $\mathbf{c} \in K(r+1)$ when $\epsilon = 0$. If $\lambda = 0$, the result is clear. If $\lambda \ne 0$, then $c(x) \ne 0$ by the above argument. Now $c^*(x)$ is some cyclic shift of $p(x) = \alpha \sum_{i=0}^{n-1} \text{TR}_r(\lambda \xi^{n-1-i}) x^i$ for some $\alpha \in \mathbb{Z}_4$ chosen so that the leading coefficient is 1 or $2$ ($c^*(x)$ may not equal $p(x)$ without the shift as we do not know the degree of $c(x)$). By Lemma 12.7.2, $\mathbf{c} \in K(r+1)$ if $H(\mathbf{c})p(x) = 0$ in $\mathfrak{A}_n$. By the same argument as in the proof of Lemma 12.7.2, the coefficient of $x^k$ for $0 \le k \le n-1$ in the product $H(\mathbf{c})p(x)$ is

$$\alpha \sum_{i+j \equiv k \text{ (mod } n)} H_i \text{TR}_r(\lambda \xi^{n-1-j}) = \alpha \text{TR}_r \left( \lambda \sum_{i=0}^{n-1} H_i \xi^{n-1-k+i} \right) = \alpha \text{TR}_r \left( \lambda \xi^{n-1-k} \sum_{i=0}^{n-1} H_i \xi^i \right),$$

using Exercise 753, as $H_i \in \mathbb{Z}_4$. The latter trace is $\text{TR}_r(\lambda \xi^{n-1-k} H(\xi)) = \text{TR}_r(0) = 0$ and hence $H(\mathbf{c})p(x) = 0$ in $\mathfrak{A}_n$. So $\mathbf{c} \in K(r+1)$. Since $K(r+1)$ and $\mathcal{C}$ each have $4^{r+1}$ codewords and $\mathcal{C} \subseteq K(r+1)$, $\mathcal{C} = K(r+1)$.

### Exercise 756 Let $\mathcal{R} = \text{GR}(4^r)$ with primitive element $\xi$; let $n = 2^r - 1$. Using the fact that $\text{TR}_r : \mathcal{R} \to \mathbb{Z}_4$ is a surjective group homomorphism under addition (Exercise 753), show the following:

- (a) For each \( a \in \mathbb{Z}_4 \), there are exactly \( 4^{r-1} \) elements of \( \mathcal{R} \) with relative trace equal to \( a \).
- (b) For each \( s \in \{0, 2\xi, 2\xi^2, \dots, 2\xi^{k-1}\} = 2\mathcal{R} \), \( \text{Tr}_r(s) \in \{0, 2\} \) with at least one value equaling 2.
- (c) For $a = 0$ or 2, there are exactly \( 2^{r-1} \) elements of \( 2\mathcal{R} \) with relative trace equal to \( a \).

Before we give the Lee weight distribution of \( \widehat{\mathcal{K}}(r+1) \) we need one more computational result.

### Lemma 12.7.5 Let \( \mathcal{R} = \text{GR}(4^r) \) have primitive element \( \xi \). Let \( n = 2^r - 1 \). Suppose that \( \lambda \in \mathcal{R} \) but \( \lambda \notin 2\mathcal{R} \). Then all the elements of \( \mathcal{S} = \mathcal{S}_1 \cup \mathcal{S}_2 \), where \( \mathcal{S}_1 = \{(\xi^j - \xi^k) \mid 0 \le j \le n-1, 0 \le k \le n-1, j \neq k\} \) and \( \mathcal{S}_2 = \{\pm \lambda \xi^j \mid 0 \le j \le n-1\} \) are distinct, and they are precisely the elements of \( \mathcal{R} \setminus 2\mathcal{R} \).

**Proof:** By Exercise 748 the set of invertible elements in \( \mathcal{R} \) is \( \mathcal{R} \setminus 2\mathcal{R} \). We only need to show that the elements of \( \mathcal{S} \) are invertible and distinct because \( \mathcal{R} \setminus 2\mathcal{R} \) has \( 4^r - 2^r \) elements and, if the elements of \( \mathcal{S} \) are distinct, \( \mathcal{S} \) has \( (2^r - 1)(2^r - 2) + 2(2^r - 1) = 4^r - 2^r \) elements.

Since \( \lambda \) is invertible, the elements of \( \mathcal{S}_2 \) are invertible. Clearly, the elements of \( \mathcal{S}_2 \) are distinct as \( -\xi^j = \xi^j + 2\xi^j \) cannot equal \( \xi^k \) for any \( j \) and \( k \).

To show the elements of \( \mathcal{S}_1 \) are invertible it suffices to show that \( \xi^j - \xi^k \) is invertible for \( j \neq k \). If this element is not invertible, \( \xi^j - \xi^k \in 2\mathcal{R} \). Recall that the reduction modulo 2 homomorphism \( \overline{\pi} : \mathcal{R} \to \mathbb{F}_{2^r} = \mathcal{R}/2\mathcal{R} \), discussed before Exercise 749, maps the primitive element \( \xi \) of \( \mathcal{R} \) to the primitive element \( \theta \) of \( \mathbb{F}_{2^r} \). Thus \( \overline{\pi}(\xi^j) + \overline{\pi}(\xi^k) = 0 \), implying that \( \theta^j = \theta^k \). But \( \theta^j \neq \theta^k \) for \( j \neq k \) with \( j \) and \( k \) between 0 and \( n-1 \). Thus the elements of \( \mathcal{S}_1 \) are invertible. We now show that the elements of \( \mathcal{S}_1 \) are distinct. Suppose that \( \xi^j - \xi^k = \xi^\ell - \xi^m \) with \( j \neq k \) and \( \ell \neq m \); then

$$1 + \xi^a = \xi^b + \xi^c, \tag{12.24}$$

where \( m - j \equiv a \pmod n \), \( \ell - j \equiv b \pmod n \), and \( k - j \equiv c \pmod n \). So \( (1 + \xi^a)^2 = v_2(1 + \xi^a) = (\xi^b + \xi^c)^2 = v_2(\xi^b + \xi^c) \), implying that \( 1 + \xi^{2a} + 2\xi^a - v_2(1) - v_2(\xi^a) = \xi^{2b} + \xi^{2c} + 2\xi^{b+c} - v_2(\xi^b) - v_2(\xi^c) \), where \( v_2 \) is the Frobenius automorphism. Thus \( 2\xi^a = 2\xi^{b+c} \), and hence \( a = b + c \pmod n \). Therefore if \( x = \xi^a \), \( y = \xi^b \), and \( z = \xi^c \), then \( x = yz \). Applying \( \overline{\pi} \) to (12.24), we also have \( 1 + x = y + z \). Hence \( 0 = 1 + yz + y + z = (1 + y)(1 + z) \) holds in \( \mathbb{F}_{2^r} \), implying \( y = 1 \) or \( z = 1 \). So \( b \equiv 0 \pmod n \) or \( c \equiv 0 \pmod n \). Hence \( \ell = j \) or \( k = j \); as the latter is impossible, we have \( \ell = j \), which yields \( k = m \) as well. So the elements of \( \mathcal{S}_1 \) are distinct.

Finally, we show that the elements of \( \mathcal{S}_1 \cup \mathcal{S}_2 \) are distinct. Assume \( \xi^j - \xi^k = \pm \xi^m \). By rearranging and factoring out a power of \( \xi \), \( 1 + \xi^a = \xi^b \). So \( (1 + \xi^a)^2 = v_2(1 + \xi^a) = \xi^{2b} - v_2(\xi^b) \), giving \( 1 + 2\xi^a + \xi^{2a} - (1 + \xi^{2a}) = \xi^{2b} - \xi^{2b} \). Therefore \( 2\xi^a = 0 \), which is a contradiction.

We now have the tools to find the Lee weight distribution of \( \widehat{\mathcal{K}}(r+1) \), which is also the Hamming weight distribution of the binary Kerdock code \( \mathcal{K}(r+1) = \Phi(\widehat{\mathcal{K}}(r+1)) \) by Theorem 12.2.2.

### Theorem 12.7.6 Let \( r \ge 3 \) with \( r \) odd. Let \( A_i \) be the number of vectors in \( \widehat{K}(r+1) \) of Lee weight \( i \). Then

\(\begin{aligned} A_i = \left\{ \begin{array}{ll} 1 & \text{if } i = 0, \\ 2^{r+1}(2^r - 1) & \text{if } i = 2^r - 2^{(r-1)/2}, \\ 2^{r+2} - 2 & \text{if } i = 2^r, \\ 2^{r+1}(2^r - 1) + 2^{(r-1)/2} & \text{if } i = 2^r + 2^{(r-1)/2}, \\ 1 & \text{if } i = 2^{r+1}, \\ 0 & \text{otherwise.} \end{array} \right. 
\end{aligned}\)

This is also the Hamming weight distribution of the Kerdock code \( \mathcal{K}(r+1) \).

**Proof:** Let \( \mathcal{R} = \text{GR}(4^r) \) and

\(\mathbf{v}_\lambda = (\text{Tr}_r(\lambda \kappa), \text{Tr}_r(\lambda \kappa^2), \dots, \text{Tr}_r(\lambda \kappa^{n-1})),\)

where \( n = 2^r - 1 \). By Lemma 12.7.4, the vectors in \( \widehat{K}(r+1) \) have the form \( (0, \mathbf{v}_\lambda) + \epsilon \mathbf{1}_{n+1} \) for \( \lambda \in \mathcal{R} \) and \( \epsilon \in \mathbb{Z}_4 \). We compute the Lee weight of each of these vectors by examining three cases. The first two cases give \( A_i \) for \( i = 0, 2^r \), and \( 2^{r+1} \). The last case gives the remaining \( A_i \).

### Case I: \( \lambda = 0 \)

In this case \( \mathbf{v}_\lambda \) is the zero vector, and \( (0, \mathbf{v}_\lambda) + \epsilon \mathbf{1}_{n+1} = \epsilon \mathbf{1}_{n+1} \) has Lee weight 0 if \( \epsilon = 0 \), \( n+1 = 2^r \) if \( \epsilon = 1 \) or 3, and \( 2(n+1) = 2^{r+1} \) if \( \epsilon = 2 \). This case contributes one vector of Lee weight 0, two vectors of Lee weight \( 2^r \), and one vector of Lee weight \( 2^{r+1} \).

### Case II: \( \lambda \in 2\mathcal{R} \) with \( \lambda \neq 0 \)

Thus \( \lambda = 2\xi^i \) for some \( 0 \le i \le n-1 \). Hence the set of components of \( \mathbf{v}_\lambda \) is always \( \{ \text{Tr}_r(2\xi^j) \mid 0 \le j \le n-1 \} \) (in some order) independent of \( i \). But by Exercise 756(c), exactly \( 2^{r-1} \) of these values are 2 and the remaining \( 2^{r-1} - 1 \) values are 0. Thus every vector \( (0, \mathbf{v}_\lambda) + \epsilon \mathbf{1}_{n+1} \) has either \( 2^{r-1} 2\)s and \( 2^{r-1} 0\)s (when \( \epsilon = 0 \) or 2) or \( 2^{r-1} 1\)s and \( 2^{r-1} 3\)s (when \( \epsilon = 1 \) or 3). In all cases these vectors have Lee weight \( 2^r \). This case contributes \( 4n = 2^{r+2} - 4 \) vectors of Lee weight \( 2^r \).

### Case III: \( \lambda \in \mathcal{R} \) with \( \lambda \notin 2\mathcal{R} \)

Let \( \mathcal{R}^* = \mathcal{R} \setminus 2\mathcal{R} \). For \( j \in \mathbb{Z}_4 \), let \( n_j = n_j(\mathbf{v}_\lambda) \) be the number of components of \( \mathbf{v}_\lambda \) equal to \( j \). We set up a sequence of equations involving the \( n_j \) and then solve these equations. Let \( i = \sqrt{-1} \). Define

\( S = \sum_{j=0}^{n-1} i^{\text{Tr}_r(\lambda \kappa^j)} = n_0 - n_2 + i(n_1 - n_3). \) (12.25)
