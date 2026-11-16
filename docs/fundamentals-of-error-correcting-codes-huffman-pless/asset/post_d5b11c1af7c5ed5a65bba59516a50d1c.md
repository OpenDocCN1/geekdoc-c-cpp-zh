
$\mathcal{C}_1 = \mathcal{A}$ and the result follows as $\mathcal{A}$ contains three singly-even vectors and one doubly-even vector. Suppose that the number of doubly-even vectors in $\mathcal{H}_1 \perp \mathcal{H}_2 \perp \cdots \perp \mathcal{H}_{l-1} \perp \mathcal{A}$ for some \(i \ge 1\) is \(2^{2i-1} - 2^{i-1}\) and the number of singly-even vectors is \(2^{2i} + 2^{i-1}\). As $\mathcal{H}_l$ has one singly-even and three doubly-even vectors, the number of doubly-even vectors in $\mathcal{H}_1 \perp \mathcal{H}_2 \perp \cdots \perp \mathcal{H}_l \perp \mathcal{A}$ is \(2^{2i-1} - 2^{i-1} + 3(2^{2i-1} - 2^{i-1}) = 2^{2i+1} - 2^i\) by Lemma 7.8.1. Similarly, the number of singly-even vectors in $\mathcal{H}_1 \perp \mathcal{H}_2 \perp \cdots \perp \mathcal{H}_l \perp \mathcal{A}$ is \(3(2^{2i-1} + 2^{i-1}) + 2^{2i-1} - 2^{i-1} = 2^{2i+1} + 2^i\). \(\square\)

### Exercise 421
Prove that \(a\) and \(b\) are as claimed in forms (H) and (O) of Theorem 7.8.6. \(\diamond\)

### Exercise 422
Find the form (H), (O), or (A) from Theorem 7.8.5, the corresponding parameters \(a, b, r,\) and \(m\) from Theorems 7.8.5 and 7.8.6, and the hull of each of the [8, 4] even binary codes with the following generator matrices:

- (a) \(G_1 = \left[ \begin{array}{cccccccc} 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 & 1 & 1 & 0 & 1 \\ 0 & 0 & 0 & 1 & 1 & 1 & 1 & 0 \end{array} \right] \).
- (b) \(G_2 = \left[ \begin{array}{cccccccc} 1 & 0 & 0 & 0 & 1 & 0 & 1 & 1 \\ 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \end{array} \right] \).
- (c) \(G_3 = \left[ \begin{array}{cccccccc} 1 & 0 & 0 & 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \end{array} \right] \). \(\diamond\)

### Example 7.8.7
The MacWilliams equations, or their equivalent forms, can be used to determine whether or not a set of nonnegative integers could arise as the weight distribution of a code. If a set of integers were to be the weight distribution of a code, then the distribution of the dual code can be computed from one of the forms of the MacWilliams equations. The resulting dual distribution must obviously be a set of nonnegative integers; if not the original set of integers could not be the weight distribution of a code. Theorem 7.8.6 cannot be used to eliminate weight distributions that the MacWilliams equations cannot. For example, suppose that \(\mathcal{C}\) is an [8, 4] binary code with weight distribution \(A_0 = A_2 = A_6 = A_8 = 1\) and \(A_4 = 12\). Computing \(A_i^\perp\), one finds that \(A_i^\perp = A_i\), and so the MacWilliams equations do not eliminate this possibility. However, by using Theorem 7.8.6, this possibility is eliminated as Exercise 423 shows. \(\blacksquare\)

### Exercise 423
Referring to Example 7.8.7, show that there is no [8, 4] binary code with weight distribution \(A_0 = A_2 = A_6 = A_8 = 1\) and \(A_4 = 12\). \(\diamond\)

### Corollary 7.8.8
If \(\mathcal{C}\) is an \([n, k]\) even binary code with \(2^{k-1}\) doubly-even and \(2^{k-1}\) singly-even codewords, then the hull of \(\mathcal{C}\) is singly-even.

### Exercise 424
Prove Corollary 7.8.8. \(\diamond\)

If $\mathcal{C}$ is a binary code with odd weight vectors, there are constraints on the number of vectors of any weight equivalent to a fixed number modulo 4; see [272].

## 7.9 Weight preserving transformations

As codes are vector spaces, it is natural to study the linear transformations that map one code to another. An arbitrary linear transformation may send a codeword of one weight to a codeword of a different weight. As we have seen throughout this book, the weights of codewords play a significant role in the study of the codes and in their error-correcting capability. Thus if we are to consider two codes to be "the same", we would want to find a linear transformation between the two codes that preserves weights; such a map is called a *weight preserving linear transformation*. In this section, we will prove that such linear transformations must be monomial maps. This result, first proved by MacWilliams in her Ph.D. thesis [212], is the basis for our definition of equivalent codes in Chapter 1. The proof we present is found in [24]; a proof using abelian group characters can be found in [347].

Let $\mathcal{C}$ be an $[n, k]$ code over $\mathbb{F}_q$. Define

\(\mu(k) = \frac{q^k - 1}{q - 1} .\)

By Exercise 425, the vector space $\mathbb{F}_q^k$ has $\mu(k)$ 1-dimensional subspaces. Let $V_1, V_2, \dots, V_{\mu(k)}$ be these subspaces, and let $\mathbf{v}_i$ be a nonzero vector in $V_i$; so $\{\mathbf{v}_i\}$ is a basis of $V_i$. The nonzero columns of a generator matrix for $\mathcal{C}$ are scalar multiples of some of the $\mathbf{v}_j$'s (of course, viewed as column vectors). Recall from Section 7.8 that $V_i$ is orthogonal to $V_j$, denoted $V_i \perp V_j$, provided $V_i$ and $V_j$ are orthogonal under the ordinary inner product; this is clearly equivalent to $\mathbf{v}_i \cdot \mathbf{v}_j = 0$. Now define a $\mu(k) \times \mu(k)$ matrix $A = [a_{i,j}]$ that describes the orthogonal relationship between the 1-dimensional spaces:

\(a_{i,j} = \begin{cases} 0 & \text{if } V_i \perp V_j, \\ 1 & \text{if } V_i \not\perp V_j. \end{cases}\)

### Exercise 425
Prove that there are $(q^k - 1)/(q - 1)$ 1-dimensional subspaces of $\mathbb{F}_q^k$. $\diamond$

We will first show that $A$ is invertible over the rational numbers $\mathbb{Q}$. In order to do this, we need the following lemma.

### Lemma 7.9.1
Let $A$ be the matrix described above. (i) The sum of the rows of $A$ is the vector $\mathbf{x} = x_1 \cdots x_{\mu(k)}$, with $x_i = \mu(k) - \mu(k-1)$ for all $i$. (ii) For $1 \le j \le \mu(k)$, let $\mathbf{y}^{(j)} = y_1^{(j)} \cdots y_{\mu(k)}^{(j)}$ be the sum of all of the rows of $A$ having 0 in column $j$. Then $y_j^{(j)} = 0$ and $y_i^{(j)} = \mu(k) - 1 - \mu(k-2)$ for all $i \ne j$.

**Proof:** To prove (i) it suffices to show that each column of $A$ has $\mu(k) - \mu(k-1)$ entries that equal 1; this is equivalent to showing that, for $1 \le i \le \mu(k)$, there are $\mu(k) - 1$ subspaces $V_j$ orthogonal to $\mathbf{v}_i$. Let $f_i : \mathbb{F}_q^k \to \mathbb{F}_q$, where $f_i(\mathbf{u}) = \mathbf{v}_i \cdot \mathbf{u}$. By Exercise 426(a), $f_i$ is a surjective linear transformation. Therefore the dimension of the kernel of $f_i$ is $k - 1$. Thus by Exercise 425, there are precisely $\mu(k-1)$ of the $V_j$ in the kernel of $f_i$, proving that there are $\mu(k-1)$ subspaces $V_j$ orthogonal to $V_i$. By (i), there are $\mu(k-1)$ rows of $A$ that have 0 in column $j$. For part (ii) it therefore suffices to show that, for each $i \neq j$, there are $\mu(k-2)$ 1-dimensional subspaces $V_m$ with $V_m \perp V_i$ and $V_m \perp V_j$. Let $f_j : \mathbb{F}_q^k \to \mathbb{F}_q^2$, where $f_j(\mathbf{u}) = (\mathbf{v}_i \cdot \mathbf{u}, \mathbf{v}_j \cdot \mathbf{u})$. By Exercise 426(b), $f_j$ is a surjective linear transformation whose kernel has dimension $k-2$. By Exercise 425, there are precisely $\mu(k-2)$ of the $V_m$ in the kernel of $f_j$, as required.

### Exercise 426
Let $\mathbf{v}$ and $\mathbf{w}$ be (nonzero) independent vectors in $\mathbb{F}_q^k$. (a) Let $f : \mathbb{F}_q^k \to \mathbb{F}_q^2$, where $f(\mathbf{u}) = (\mathbf{v} \cdot \mathbf{u}, \mathbf{w} \cdot \mathbf{u})$. Show that $f$ is a surjective linear transformation. (b) Let $g : \mathbb{F}_q^k \to \mathbb{F}_q^2$, where $g(\mathbf{u}) = (\mathbf{v} \cdot \mathbf{u}, \mathbf{w} \cdot \mathbf{u})$. Show that $g$ is a surjective linear transformation. (See Exercise 419 for a comparable result.)

### Theorem 7.9.2
The matrix $A$ is invertible over $\mathbb{Q}$.

Proof: It suffices to show that $A$ has rank $\mu(k)$ over $\mathbb{Q}$. This is accomplished if we show that by taking some linear combination of rows of $A$ we can obtain all of the standard basis vectors $\mathbf{e}^{(j)}$, where $\mathbf{e}^{(j)}$ has a 1 in position $j$ and 0 elsewhere. But in the notation of Lemma 7.9.1,

$\mathbf{e}^{(j)} = \frac{1}{\mu(k) - \mu(k-1)}\mathbf{x} - \frac{1}{\mu(k-1) - \mu(k-2)}\mathbf{y}^{(j)}$.

Fix a generator matrix $G$ of $\mathcal{C}$. Denote the columns of $G$ by col($G$). Define the linear transformation $f : \mathbb{F}_q^k \to \mathcal{C}$ by $f(\mathbf{u}) = \mathbf{u}G$. (This is the standard way of encoding the message $\mathbf{u}$ using $G$ as described in Section 1.11.) We define a vector $\mathbf{w} = w_1 \cdots w_{\mu(k)}$ with integer entries:

$w_j = |\{\mathbf{c} \in \text{col}(G) \mid \mathbf{c} \neq \mathbf{0}, \mathbf{c}^T \in V_j\}|$.

Thus $w_j$ tells how many nonzero columns of $G$ are in $V_j$, that is, how many columns of $G$ are nonzero scalar multiples of $\mathbf{v}_j$. So there are $n - \sum_{j=1}^{\mu(k)} w_j$ zero columns of $G$. By knowing $\mathbf{w}$ we can reproduce $G$ up to permutation and scaling of columns. Notice that as the vectors $\mathbf{v}_1, \dots, \mathbf{v}_{\mu(k)}$ consist of all the basis vectors of the 1-dimensional subspaces of $\mathbb{F}_q^k$, then $f(\mathbf{v}_1), \dots, f(\mathbf{v}_{\mu(k)})$ consist of all the basis vectors of 1-dimensional subspaces of $\mathcal{C}$, as $G$ has rank $k$ and $\mathcal{C}$ is $k$-dimensional. The weights of these codewords $f(\mathbf{v}_i)$ are determined by $A\mathbf{w}^T$.

### Theorem 7.9.3
For $1 \le i \le \mu(k)$, $(A\mathbf{w}^T)_i = \text{wt}(f(\mathbf{v}_i))$.

Proof: We have

$(A\mathbf{w}^T)_i = \sum_{j=1}^{\mu(k)} a_{i,j} w_j = \sum_{j \in S_i} w_j$.
