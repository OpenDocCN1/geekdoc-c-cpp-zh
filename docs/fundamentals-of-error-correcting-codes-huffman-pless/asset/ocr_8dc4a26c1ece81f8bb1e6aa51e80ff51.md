(c) Show that $\lim_{n \to \infty} -n^{-1} (n \log_q n - \lfloor \delta n \rfloor \log_q \lfloor \delta n \rfloor - (n - \lfloor \delta n \rfloor) \log_q (n - \lfloor \delta n \rfloor)) = -\delta \log_q \delta - (1 - \delta) \log_q (1 - \delta)$. $\unknown$

**Exercise 136** Let $0 < 1 < \delta n$ where $0 < \delta \le 1 - q^{-1}$ and $q \ge 2$. Prove that $\binom{n}{1} \times (q - 1)^{-1} < \binom{q-1}{q-1}$. $\unknown$

Recall that a sphere of radius $a$ in $\mathbb{F}_q^n$ centered at some vector in $\mathbb{F}_q^n$ contains

$V_q(n, a) = \sum_{i=0}^a \binom{n}{i} (q - 1)^i$ (2.44)

vectors. The following lemma gives a relationship between $V_q(n, a)$ and the entropy function.

**Lemma 2.10.3** Let $0 < \delta \le 1 - q^{-1}$ where $q \ge 2$. Then

$\lim_{n \to \infty} n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) = H_q(\delta).$

**Proof:** In (2.44) with $a = \lfloor \delta n \rfloor$, the largest of the $1 + \lfloor \delta n \rfloor$ terms is the one with $i = \lfloor \delta n \rfloor$ by Exercise 136. Thus

$\binom{n}{\lfloor \delta n \rfloor} (q - 1)^{\lfloor \delta n \rfloor} \le V_q(n, \lfloor \delta n \rfloor) \le (1 + \lfloor \delta n \rfloor) \binom{n}{\lfloor \delta n \rfloor} (q - 1)^{\lfloor \delta n \rfloor}.$

Taking logarithms and dividing by $n$ gives

$A + n^{-1} \lfloor \delta n \rfloor \log_q (q - 1) \le n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) \le A + n^{-1} \lfloor \delta n \rfloor \log_q (q - 1) + n^{-1} \log_q (1 + \lfloor \delta n \rfloor)$

where $A = n^{-1} \log_q \binom{n}{\lfloor \delta n \rfloor}$. Therefore,

$\lim_{n \to \infty} n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) = \lim_{n \to \infty} A + \delta \log_q (q - 1)$ (2.45)

as $\lim_{n \to \infty} n^{-1} \log_q (1 + \lfloor \delta n \rfloor) = 0$.

As $\binom{n}{\lfloor \delta n \rfloor} = n! / (\lfloor \delta n \rfloor! (n - \lfloor \delta n \rfloor)!)$, by Stirling's Formula,

$\frac{n^{n+1/2} e^{-n+7/8}}{\lfloor \delta n \rfloor^{\lfloor \delta n \rfloor + 1/2} e^{-\lfloor \delta n \rfloor + (n - \lfloor \delta n \rfloor)^{n - \lfloor \delta n \rfloor + 1/2} e^{-(n - \lfloor \delta n \rfloor + 1/2}}} \le \binom{n}{\lfloor \delta n \rfloor}$

and

$\binom{n}{\lfloor \delta n \rfloor} \le \frac{n^{n+1/2} e^{-n+1}}{\lfloor \delta n \rfloor^{\lfloor \delta n \rfloor + 1/2} e^{-\lfloor \delta n \rfloor + 7/8} (n - \lfloor \delta n \rfloor)^{n - \lfloor \delta n \rfloor + 1/2} e^{-(n - \lfloor \delta n \rfloor + 1/8}};$

hence

$B e^{-9/8} \le \binom{n}{\lfloor \delta n \rfloor} \le B e^{-3/4},$

where

$B = \frac{n^{n+1/2}}{\lfloor \delta n \rfloor^{\lfloor \delta n \rfloor + 1/2} (n - \lfloor \delta n \rfloor)^{n - \lfloor \delta n \rfloor + 1/2}}.$