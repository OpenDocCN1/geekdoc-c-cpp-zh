

- (b) Choose m = 2 in the Sudan–Guruswami Algorithm. Find the smallest value of $\delta$ for which $nm(m + 1)/2 = 3 < N_\delta(\delta)$. Using $m = 2$, how many errors can the Sudan–Guruswami Algorithm correct?

- (c) Choose m = 3 in the Sudan–Guruswami Algorithm. Find the smallest value of $\delta$ for which $nm(m + 1)/2 = 186 < N_\delta(\delta)$. Using $m = 3$, how many errors can the Sudan–Guruswami Algorithm correct?

As can be seen in Example 5.4.20 and Exercises 311 and 312, the error-correcting capability of the Sudan–Guruswami Decoding Algorithm can grow if m is increased. The tradeoff for higher error-correcting capability is an increase in the (1, k - 1)-weighted degree of p(x, y), which of course increases the complexity of the algorithm. The following corollary gives an idea of how the error-correcting capability varies with m.

### Corollary 5.4.21
The Sudan–Guruswami Decoding Algorithm applied to the [n, k, n - k + 1] code GRS_k(\gamma, v) will produce all codewords within Hamming distance e or less of a received vector where e >= n - 1 - n \sqrt{R(m + 1)/m} and R = k/n.

**Proof:** As $\delta$ is chosen to be the smallest positive integer such that (5.21) holds, $N_{k-1}(\delta - 1) \le nm(m + 1)/2$. By Lemma 5.4.19, $N_{k-1}(\delta - 1) \ge (\delta - 1)(\delta + 1)/(2(k - 1))$. Hence $\frac{\delta^2 - 1}{2(k - 1)} \le \frac{nm(m + 1)}{2}$. If $\delta^2 < k$, then $\delta^2/(2k) < 1/2 \le nm(m + 1)/2$. If $\delta^2 \ge k$, then $\delta^2/(2k) \le (\delta^2 - 1)/(2(k - 1))$ by Exercise 313. In either case, $\delta^2/2k \le nm(m + 1)/2$, implying $\frac{\delta}{m} \le n \sqrt{\frac{k}{n} \frac{m + 1}{m}}$, which produces the desired result from Theorem 5.4.18.

### Exercise 313
Do the following: (a) Show that if $\delta^2 \ge k$, then $\delta^2/(2k) \le (\delta^2 - 1)/(2(k - 1))$. (b) Show that if $\delta^2/(2k) \le nm(m + 1)/2$, then $\delta/m \le n \sqrt{\frac{k}{n} \frac{m+1}{m}}$.

In this corollary, R = k/n is the information rate. If m is large, we see that the fraction e/n of errors of the Sudan–Guruswami Decoding Algorithm can correct is approximately 1 - \sqrt{R}. The fraction of errors that the Peterson–Gorenstein–Zierler Decoding Algorithm can correct is approximately (1 - R)/2. Exercise 314 explores the relationship between these two functions.

### Exercise 314
Do the following:

- (a) Verify that the fraction of errors that the Peterson–Gorenstein–Zierler Decoding Algorithm can correct in a GRS code is approximately $(1 - R)/2$.

- (b) Plot the two functions $y = 1 - \sqrt{R}$ and $y = (1 - R)/2$ for $0 \le R \le 1$ on the same graph. What do these graphs show about the comparative error-correcting capability of the Peterson–Gorenstein–Zierler and the Sudan–Guruswami Decoding Algorithms?

To carry out the Sudan–Guruswami Decoding Algorithm we must have a method to compute the polynomial $p(x, y)$ of Step II and then find the factors of $p(x, y)$ of the form $y - f(x)$ in Step III. (Finding $p(x, y)$ can certainly be accomplished by solving the $nm(m + 1)/2$ equations from (5.22), but as the values in Exercise 312 indicate, the number of equations and unknowns gets rather large rather quickly.) A variety of methods have been introduced to carry out Steps II and III. We will not examine these methods here, but the interested reader can consult [11, 178, 245, 248, 300, 354].

## 5.5 Burst errors, concatenated codes, and interleaving

Reed–Solomon codes, used in concatenated form, are very useful in correcting burst errors. As the term implies, a *burst error* occurs when several consecutive components of a codeword may be in error; such a burst often extends over several consecutive codewords which are received in sequence.

Before giving the actual details, we illustrate the process. Suppose that $\mathcal{C}$ is an $[n, k]$ binary code being used to transmit information. Each message from $\mathbb{F}_2^k$ is encoded to a codeword from $\mathbb{F}_2^n$ using $\mathcal{C}$. The message is transmitted then as a sequence of $n$ binary digits. In reality, several codewords are sent one after the other, which then appear to the receiver as a very long string of binary digits. Along the way these digits may have been changed. A random individual symbol may have been distorted so that one cannot recognize it as either 0 or 1, in which case the received symbol is considered erased. Or a random symbol could be changed into another symbol and the received symbol is in error. As we discussed in Section 1.11, more erasures than errors can be corrected because error locations are unknown, whereas erasure locations are known. Sometimes several consecutive symbols, a burst, may have been erased or are in error. The receiver then breaks up the string into codewords of length $n$ and decodes each string, if possible. However, the presence of burst errors can make decoding problematic as the codes we have developed are designed to correct random errors. However, we can modify our codes to also handle bursts: An example where the use of coding has made a significant impact is in compact disc recording; a scratch across the disc can destroy several consecutive bits of information. The ability to correct burst errors has changed the entire audio industry. We will take this up in the next section.

Burst errors are often handled using concatenated codes, which are sometimes then interleaved. Concatenated codes were introduced by Forney in [87]. We give a simple version of concatenated codes; the more general theory can be found, for example, in [75].

Let $\mathcal{A}$ be an $[n, k, d]$ code over $\mathbb{F}_q$. Let $Q = q^k$ and define $\psi : \mathbb{F}_Q \to \mathcal{A}$ to be a one-to-one $\mathbb{F}_q$-linear map; that is $\psi(x + y) = \psi(x) + \psi(y)$ for all $x$ and $y$ in $\mathbb{F}_Q$, and $\psi(\alpha x) = \alpha \psi(x)$ for all $x \in \mathbb{F}_Q$ and $\alpha \in \mathbb{F}_q$, noting that $\mathbb{F}_Q$ is an extension field of $\mathbb{F}_q$. Let $\mathcal{B}$ be an $[N, K, D]$ code over $\mathbb{F}_Q$. The concatenation of $\mathcal{A}$ and $\mathcal{B}$ is the code

$\mathcal{C} = \{\psi(b_1, b_2, ..., b_N) \mid (b_1, b_2, ..., b_N) \in \mathcal{B}\},$

where $\psi(b_1, b_2, ..., b_N) = (\psi(b_1), \psi(b_2), ..., \psi(b_N))$. $\mathcal{C}$ is called a *concatenated code* with *inner code* $\mathcal{A}$ and *outer code* $\mathcal{B}$. In effect, a codeword in $\mathcal{C}$ is obtained by taking a codeword in $\mathcal{B}$ and replacing each component by a codeword of $\mathcal{A}$ determined by the image of that component under $\psi$. The code $\mathcal{C}$ is then a code of length $nN$ over $\mathbb{F}_q$. The following theorem gives further information about $\mathcal{C}$.

### Theorem 5.5.1
Let $\mathcal{A}$, $\mathcal{B}$, and $\mathcal{C}$ be as above. Then $\mathcal{C}$ is a linear $[nN, kK]$ code over $\mathbb{F}_q$ whose minimum distance is at least $dD$.

### Exercise 315
Prove Theorem 5.5.1. $\diamond$

### Example 5.5.2
Let $\mathcal{B}$ be the $[6, 3, 4]$ hexacode over $\mathbb{F}_4$ with generator matrix

$G = $

| 1 | 0 | 0 | 1 | ω | ω |
|---|---|---|---|---|---|
| 0 | 1 | 0 | ω | 1 | ω |
| 0 | 0 | 1 | ω | ω | 1 |

Let $\mathcal{A}$ be the $[2, 1]$ binary code $\mathbb{F}_2^2$ and define $\psi : \mathbb{F}_4 \to \mathcal{A}$ by the following:

$\psi(00) = 00, \quad \psi(1) = 10, \quad \psi(\omega) = 01, \quad \psi(\bar{\omega}) = 11.$

This is $\mathbb{F}_2$-linear, as can be easily verified. The concatenated code $\mathcal{C}$ with inner code $\mathcal{A}$ and outer code $\mathcal{B}$ has generator matrix

| 1 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 1 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 |
| 0 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 1 |
| 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 1 | 1 | 1 |
| 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | 0 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 0 | 1 | 0 |

Rows two, four, and six of this matrix are obtained after multiplying the rows of $G$ by $\omega$. $\mathcal{C}$ is a $[12, 6, 4]$ code. $\blacksquare$

### Exercise 316
Let $\mathcal{B}$ be the hexacode given in Example 5.5.2, and let $\mathcal{A}$ be the $[3, 2, 2]$ even binary code. Define $\psi : \mathbb{F}_4 \to \mathcal{A}$ by the following:

$\psi(000) = 000, \quad \psi(1) = 101, \quad \psi(\omega) = 011, \quad \psi(\bar{\omega}) = 110.$

- (a) Verify that $\psi$ is $\mathbb{F}_2$-linear.

- (b) Give a generator matrix for the concatenated code $\mathcal{C}$ with inner code $\mathcal{A}$ and outer code $\mathcal{B}$.

- (c) Show that $\mathcal{C}$ is an $[18, 6, 8]$ code. $\diamond$

