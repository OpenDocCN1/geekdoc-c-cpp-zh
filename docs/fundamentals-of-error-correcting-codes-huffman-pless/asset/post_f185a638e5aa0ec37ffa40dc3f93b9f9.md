
Example 1.12.7 Let $\mathcal{C}$ be the ternary code with generator matrix $[1 \ 1 \ -1]$. Computing the covering radius, we see that $\rho(\mathcal{C}) = \rho(\bar{\mathcal{C}}) = 2$. If $\mathcal{D} = \bar{\mathcal{C}}$ and we puncture $\mathcal{D}$ on the last coordinate to obtain $\mathcal{D}^* = \mathcal{C}$, we have $\rho(\mathcal{D}) = \rho(\mathcal{D}^*)$.

In the binary case by Theorem 1.12.6(iv), whenever we extend a code, we increase the covering radius by 1. But when we puncture a binary code we may not reduce the covering radius.

Example 1.12.8 Let $\mathcal{C}$ be the binary code with generator matrix

```
[ 1 0 1 1 ]
[ 0 1 1 1 ]
```

and let $\mathcal{C}^*$ be obtained from $\mathcal{C}$ by puncturing on the last coordinate. It is easy to see that $\rho(\mathcal{C}) = \rho(\mathcal{C}^*) = 1$. Also if $\mathcal{D}$ is the extension of $\mathcal{C}^*$, $\rho(\mathcal{D}) = 2$, consistent with Theorem 1.12.6.

## 2 Bounds on the size of codes

In this chapter, we present several bounds on the number of codewords in a linear or nonlinear code given the length n and minimum distance d of the code. In Section 1.12 we proved the Sphere Packing (or Hamming) Bound, which gives an upper bound on the size of a code. This chapter is devoted to developing several other upper bounds along with two lower bounds. There are fewer lower bounds presented, with lower bounds are often tied to particular constructions of codes. For example, if a code with a given length n and minimum distance d is produced, its size becomes a lower bound on the code size. In this chapter we will speak about codes that meet a given bound. If the bound is a lower bound on size of a code in terms of its length and minimum distance, then a code C meets the lower bound if the size of C is at least the size given by the lower bound. If the bound is an upper bound on the size of a code in terms of its length and minimum distance, then C meets the upper bound if its size equals the size given by the upper bound. We present the upper bounds first after we take a closer look at the concepts previously developed.

### 2.1 $A_q(n, d)$ and $B_q(n, d)$

In this section, we will consider both linear and nonlinear codes. An $(n, M, d)$ code C over $\mathbb{F}_q$ is a code of length n with M codewords whose minimum distance is d. The code C can be either linear or nonlinear; if it is linear, it is an $[n, k, d]$ code, where $k = \log_q M$ and d is the minimum weight of C; see Theorem 1.4.2.

We stated the Sphere Packing Bound using the notation $B_q(n, d)$ and $A_q(n, d)$, where $B_q(n, d)$, respectively $A_q(n, d)$, is the largest number of codewords in a linear, respectively arbitrary linear or nonlinear, code over $\mathbb{F}_q$ of length n and minimum distance at least d. A code of length n over $\mathbb{F}_q$ and minimum distance at least d will be called optimal if it has $A_q(n, d)$ codewords (or $B_q(n, d)$ codewords in the case that C is linear). There are other perspectives on optimizing a code. For example, one could ask to find the largest d, given n and M, such that there is a code over $\mathbb{F}_q$ of length n with M codewords and minimum distance d. Or, find the smallest n, given M and d such that there is a code over $\mathbb{F}_q$ of length n with M codewords and minimum distance d. We choose to focus on $A_q(n, d)$ and $B_q(n, d)$ here.

We begin with some rather simple properties of $A_q(n, d)$ and $B_q(n, d)$. First we have the following obvious facts:

Table 2.1 Upper and lower bounds on $A_2(n, d)$ for $6 \le n \le 24$

| n | d = 4 | d = 6 | d = 8 | d = 10 |
|---|---|---|---|---|
| 6 | 4 | 2 | 1 | 1 |
| 7 | 8 | 2 | 1 | 1 |
| 8 | 16 | 2 | 2 | 1 |
| 9 | 20 | 4 | 2 | 1 |
| 10 | 40 | 6 | 2 | 2 |
| 11 | 72 | 12 | 2 | 2 |
| 12 | 144 | 24 | 4 | 2 |
| 13 | 256 | 32 | 4 | 2 |
| 14 | 512 | 64 | 8 | 2 |
| 15 | 1024 | 128 | 16 | 4 |
| 16 | 2048 | 256 | 32 | 4 |
| 17 | 2720–3276 | 256–340 | 36–37 | 6 |
| 18 | 5312–6552 | 512–680 | 64–72 | 10 |
| 19 | 10496–13104 | 1024–1288 | 128–144 | 20 |
| 20 | 20480–26208 | 2048–2372 | 256–279 | 40 |
| 21 | 36864–43689 | 2560–4096 | 512 | 42–48 |
| 22 | 73728–87378 | 4096–6941 | 1024 | 50–88 |
| 23 | 147456–173491 | 8192–13774 | 2048 | 76–150 |
| 24 | 294912–344308 | 16384–24106 | 4096 | 128–280 |

Theorem 2.1.1 $B_q(n, d) \le A_q(n, d)$ and $B_q(n, d)$ is a nonnegative integer power of $q$. So $B_q(n, d)$ is a lower bound for $A_q(n, d)$ and $A_q(n, d)$ is an upper bound for $B_q(n, d)$. The Sphere Packing Bound is an upper bound on $A_q(n, d)$ and hence on $B_q(n, d)$. Tables which lead to information about the values of $A_q(n, d)$ or $B_q(n, d)$ have been computed and are regularly updated. These tables are for small values of $q$ and moderate to large values of $n$. The most comprehensive table is compiled by A. E. Brouwer [32], which gives upper and lower bounds on the minimum distance $d$ of an $[n, k]$ linear code over $\mathbb{F}_q$. A less extensive table giving bounds for $A_2(n, d)$ is kept by S. Litsyn [205].

To illustrate, we reproduce a table due to many authors and recently updated by Agrell, Vardy, Zeger, and Litsyn in [2, 205]. Most of the upper bounds in Table 2.1 are obtained from the bounds presented in this chapter together with the Sphere Packing Bound; ad hoc methods in certain cases produce the remaining values. Notice that Table 2.1 contains only even values of $d$, a consequence of the following result.

Theorem 2.1.2 Let $d > 1$. Then:
- (i) $A_q(n, d) \le A_q(n-1, d-1)$ and $B_q(n, d) \le B_q(n-1, d-1)$, and
- (ii) if $d$ is even, $A_2(n, d) = A_2(n-1, d-1)$ and $B_2(n, d) = B_2(n-1, d-1)$.
Furthermore:
- (iii) if $d$ is even and $M = A_2(n, d)$, then there exists a binary $(n, M, d)$ code such that all codewords have even weight and the distance between all pairs of codewords is also even.

Proof: Let $\mathcal{C}$ be a code (linear or nonlinear) with $M$ codewords and minimum distance $d$. Puncturing on any coordinate gives a code $\mathcal{C}'$ also with $M$ codewords; otherwise if $\mathcal{C}''$ has fewer codewords, there would exist two codewords of $\mathcal{C}$ which differ in one position implying $d=1$. This proves (i); to complete (ii), we only need to show that $A_2(n, d) \ge A_2(n-1, d-1)$ (or $B_2(n, d) \ge B_2(n-1, d-1)$) when $\mathcal{C}$ is linear. To that end let $\mathcal{C}$ be a binary code with $M$ codewords, length $n-1$, and minimum distance $d-1$. Extend $\mathcal{C}$ by adding an overall parity check to obtain a code $\bar{\mathcal{C}}$ of length $n$ and minimum distance $d$, since $d-1$ is odd. Because $\bar{\mathcal{C}}$ has $M$ codewords, $A_2(n, d) \ge A_2(n-1, d-1)$ (or $B_2(n, d) \ge B_2(n-1, d-1)$). For (iii), if $\mathcal{C}$ is a binary $(n, M, d)$ code with $d$ even, the punctured code $\mathcal{C}'$ as previously stated is an $(n-1, M, d-1)$ code. Extending $\mathcal{C}^*$ produces an $(n, M, d)$ code $\bar{\mathcal{C}}'$ since $d-1$ is odd; furthermore this code has only even weight codewords. Since $\mathbf{d}(\mathbf{x}, \mathbf{y}) = \text{wt}(\mathbf{x} + \mathbf{y}) = \text{wt}(\mathbf{x}) + \text{wt}(\mathbf{y}) - 2\text{wt}(\mathbf{x} \cap \mathbf{y})$, the distance between codewords is even.

Exercise 85 In the proof of Theorem 2.1.2, we claim that if $\mathcal{C}$ is a binary code of length $n-1$ and minimum weight $d-1$, where $d-1$ is odd, then the extended code $\bar{\mathcal{C}}$ of length $n$ has minimum distance $d$. In Section 1.5.2 we stated that this is true if $\mathcal{C}$ is linear, where it is obvious since the minimum distance is the minimum weight. Prove that it is also true when $\mathcal{C}$ is nonlinear.

Theorem 2.1.2(ii) shows that any table of values of $A_2(n, d)$ or $B_2(n, d)$ only needs to be compiled for $d$ either always odd or $d$ always even. Despite the fact that $A_2(n, d) = A_2(n-1, d-1)$ when $d$ is even, we want to emphasize that a given bound for $A_2(n, d)$ may not be the same bound as for $A_2(n-1, d-1)$. So since these values are equal, we can always choose the smaller upper bound, respectively larger lower bound, as a common upper bound, respectively lower bound, for both $A_2(n, d)$ and $A_2(n-1, d-1)$.

Example 2.1.3 By using $n=7$ and $d=4$ (that is, $t=1$) in the Sphere Packing Bound, we find that $A_2(7, 4) \le 16$. On the other hand, using $n=6$ and $d=3$ (still, $t=1$) the Sphere Packing Bound yields $64/7$ implying that $A_2(6, 3) \le 9$. So by Theorem 2.1.2(ii) an upper bound for both $A_2(7, 4)$ and $A_2(6, 3)$ is 9.

Exercise 86 Let $\mathcal{C}$ be a code (possibly nonlinear) over $\mathbb{F}_q$ with minimum distance $d$. Fix a codeword $\mathbf{c}$ in $\mathcal{C}$. Let $\mathcal{C}_1 = \{\mathbf{x} - \mathbf{c} \mid \mathbf{x} \in \mathcal{C}\}$. Prove that $\mathcal{C}_1$ contains the zero vector $\mathbf{0}$, has the same number of codewords as $\mathcal{C}$, and also has minimum distance $d$. Prove also that $\mathcal{C} = \mathcal{C}_1$ if $\mathcal{C}$ is linear.

Exercise 87 By Example 2.1.3, $A_2(7, 4) \le 9$.
- (a) Prove that $B_2(7, 4) \le 8$.
- (b) Find a binary [7, 3, 4] code thus verifying $B_2(7, 4) = 2^3 = 8$. In our terminology, this code is optimal.
- (c) Show that $A_2(7, 4)$ is either 8 or 9. (Table 2.1 shows that it is actually 8, a fact we will verify in the next section.)

Exercise 88 By Table 2.1, $A_2(13, 10) = 2$.
- (a) By computing the Sphere Packing Bound using $(n, d) = (13, 10)$ and $(12, 9)$, find the best sphere packing upper bound for $A_2(13, 10)$.
