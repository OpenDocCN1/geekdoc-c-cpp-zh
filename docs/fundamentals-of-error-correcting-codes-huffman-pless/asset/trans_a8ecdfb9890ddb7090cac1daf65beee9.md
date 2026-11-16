

- (c) 证明 $\lim_{n \to \infty} -n^{-1} (n \log_q n - \lfloor \delta n \rfloor \log_q \lfloor \delta n \rfloor - (n - \lfloor \delta n \rfloor) \log_q (n - \lfloor \delta n \rfloor)) = -\delta \log_q \delta - (1 - \delta) \log_q (1 - \delta)$. $\unknown$

**练习 136** 设 $0 < 1 < \delta n$，其中 $0 < \delta \le 1 - q^{-1}$ 且 $q \ge 2$。证明 $\binom{n}{1} \times (q - 1)^{-1} < \binom{q-1}{q-1}$。$\unknown$

回顾，$\mathbb{F}_q^n$ 中以某个向量为中心、半径为 $a$ 的球包含

$V_q(n, a) = \sum_{i=0}^a \binom{n}{i} (q - 1)^i$ (2.44)

个向量。以下引理给出了 $V_q(n, a)$ 与熵函数之间的关系。

**引理 2.10.3** 设 $0 < \delta \le 1 - q^{-1}$，其中 $q \ge 2$。则

$\lim_{n \to \infty} n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) = H_q(\delta).$

**证明：** 在 (2.44) 中，令 $a = \lfloor \delta n \rfloor$，根据练习 136，在 $1 + \lfloor \delta n \rfloor$ 项中，最大的一项是 $i = \lfloor \delta n \rfloor$ 时的那一项。因此

$\binom{n}{\lfloor \delta n \rfloor} (q - 1)^{\lfloor \delta n \rfloor} \le V_q(n, \lfloor \delta n \rfloor) \le (1 + \lfloor \delta n \rfloor) \binom{n}{\lfloor \delta n \rfloor} (q - 1)^{\lfloor \delta n \rfloor}.$

对两边取对数并除以 $n$ 得到

$A + n^{-1} \lfloor \delta n \rfloor \log_q (q - 1) \le n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) \le A + n^{-1} \lfloor \delta n \rfloor \log_q (q - 1) + n^{-1} \log_q (1 + \lfloor \delta n \rfloor)$

其中 $A = n^{-1} \log_q \binom{n}{\lfloor \delta n \rfloor}$。因此，

$\lim_{n \to \infty} n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) = \lim_{n \to \infty} A + \delta \log_q (q - 1)$ (2.45)

因为 $\lim_{n \to \infty} n^{-1} \log_q (1 + \lfloor \delta n \rfloor) = 0$.

由于 $\binom{n}{\lfloor \delta n \rfloor} = n! / (\lfloor \delta n \rfloor! (n - \lfloor \delta n \rfloor)!)$，根据斯特林公式，

$\frac{n^{n+1/2} e^{-n+7/8}}{\lfloor \delta n \rfloor^{\lfloor \delta n \rfloor + 1/2} e^{-\lfloor \delta n \rfloor} (n - \lfloor \delta n \rfloor)^{n - \lfloor \delta n \rfloor + 1/2} e^{-(n - \lfloor \delta n \rfloor + 1/2)}} \le \binom{n}{\lfloor \delta n \rfloor}$

且

$\binom{n}{\lfloor \delta n \rfloor} \le \frac{n^{n+1/2} e^{-n+1}}{\lfloor \delta n \rfloor^{\lfloor \delta n \rfloor + 1/2} e^{-\lfloor \delta n \rfloor + 7/8} (n - \lfloor \delta n \rfloor)^{n - \lfloor \delta n \rfloor + 1/2} e^{-(n - \lfloor \delta n \rfloor + 1/8}}};$

因此

$B e^{-9/8} \le \binom{n}{\lfloor \delta n \rfloor} \le B e^{-3/4},$

其中

$B = \frac{n^{n+1/2}}{\lfloor \delta n \rfloor^{\lfloor \delta n \rfloor + 1/2} (n - \lfloor \delta n \rfloor)^{n - \lfloor \delta n \rfloor + 1/2}}.$

由于

$$
\lim_{n \to \infty} n^{-1} \log_q (B^k e) = \lim_{n \to \infty} n^{-1} (\log_q B + k \log_q e) = \lim_{n \to \infty} n^{-1} \log_q B,
$$

我们得出

$$
\begin{aligned}
\lim_{n \to \infty} A &= \lim_{n \to \infty} n^{-1} \log_q B \\
&= \lim_{n \to \infty} n^{-1} [n \log_q n - \lfloor \delta n \rfloor \log_q \lfloor \delta n \rfloor - (n - \lfloor \delta n \rfloor) \log_q (n - \lfloor \delta n \rfloor)] \\
&\quad + \lim_{n \to \infty} n^{-1} (1/2) [\log_q n - \log_q \lfloor \delta n \rfloor - \log_q (n - \lfloor \delta n \rfloor)] \\
&= -\delta \log_q \delta - (1 - \delta) \log_q (1 - \delta) + 0
\end{aligned}
$$

根据练习 135。代入 (2.45)，得到

$$
\lim_{n \to \infty} n^{-1} \log_q V_q(n, \lfloor \delta n \rfloor) = -\delta \log_q \delta - (1 - \delta) \log_q (1 - \delta) + \delta \log_q(q - 1),
$$

即 $H_q(\delta)$，从而证明了结果。$\square$

## 定理 2.10.4（渐近汉明界）设 $0 < \delta \le 1 - q^{-1}$，其中 $q \ge 2$。则 $\alpha_q(\delta) \le 1 - H_q(\delta)/2$.

**证明：** 首先注意，根据球堆积界，$A_q(n, \delta n) = A_q(n, \lfloor \delta n \rfloor) \le q^n / V_q(n, (\lfloor \delta n \rfloor - 1)/2)$。若 $n \ge N$，则 $(\lfloor \delta n \rfloor - 1)/2 \ge \lceil \delta n / 2 \rceil - 1 \ge (\lfloor \delta - (2/N)n \rfloor / 2)$。因此 $A_q(n, \delta n) \le q^n / V_q(n, (\lfloor \delta - (2/N)n \rfloor / 2)n)$，这意味着

$$
\begin{aligned}
\alpha_q(\delta) &= \limsup_{n \to \infty} n^{-1} \log_q A_q(n, \delta n) \\
&\le \limsup_{n \to \infty} 1 - n^{-1} \log_q V_q \left( n, \left\lfloor \frac{1}{2} \left( \delta - \frac{2}{N} \right) n \right\rfloor \right) \\
&= 1 - H_q \left( \frac{1}{2} \left( \delta - \frac{2}{N} \right) \right)
\end{aligned}
$$

根据引理 2.10.3。但当 $n$ 趋于无穷时，我们可以令 $N$ 任意大，从而表明 $\alpha_q(\delta) = 1 - H_q(\delta)/2$，因为 $H_q$ 是连续的。$\square$

**练习 137** 继续练习 134，在为 $q = 2$、$q = 3$ 和 $q = 4$ 绘制的图中加入渐近汉明界不等式的图。（计算机绘图工具可能会有所帮助。）在每种情况下，对于哪些 $\delta$ 的值，渐近汉明界比渐近辛格界和渐近普洛特金界更强？$\unknown$

## 2.10.4 渐近埃利亚斯界

渐近埃利亚斯界优于渐近辛格界、普洛特金界和汉明界。已知当 $1 - q^{-1} = r \le \delta \le 1$ 时 $\alpha_q(\delta) = 0$，因此我们只考察 $0 < \delta < r$ 的情况。

## 定理 2.10.5（渐近埃利亚斯界）设 \( 0 < \delta < r = 1 - q^{-1} \)，其中 \( q \ge 2 \)。则 \( \alpha_q(\delta) \le 1 - H_q(r - \sqrt{r(r-\delta)}) \).

**证明：** 选取 $x$ 使得 \( 0 < x < r - \sqrt{r(r-\delta)} \)。则 \( x^2 - 2rx + r\delta > 0 \)。令 \( w = \lfloor xn \rfloor \) 和 \( d = \lceil \delta n \rceil \)。根据练习 138，当 $n$ 足够大时，\( w^2 - 2rnw + rnd > 0 \)。由于 $x < r$，有 $w < rn$。因此根据埃利亚斯界，当 $n$ 足够大时，

$$
A_q(n, \delta n) = A_q(n, d) \le \frac{rnd}{w^2 - 2rnw + rnd} \cdot \frac{q^n}{V_q(n, w)}.
$$

所以

$$
\begin{aligned}
n^{-1} \log_q A_q(n, \delta n) &\le n^{-1} \log_q \left( \frac{rnd}{w^2 - 2rnw + rnd} \cdot \frac{q^n}{V_q(n, w)} \right) \\
&= n^{-1} \log_q \left( \left(\frac{w}{n}\right)^{-2} \frac{d}{n} \frac{w}{r} \frac{d}{r} \right) + 1 - n^{-1} \log_q V_q(n, \lfloor xn \rfloor).
\end{aligned}
$$

观察到 \(\lim_{n \to \infty} d/n = \delta\) 和 \(\lim_{n \to \infty} w/n = x\)，对上述取极限并使用引理 2.10.3，

$$
\alpha_q(\delta) \le 1 - H_q(x).
$$

由于这对所有满足 \( 0 < x < r - \sqrt{r(r-\delta)} \) 的 $x$ 都成立，且 \( H_q(x) \) 是连续的，故 \( \alpha_q(\delta) \le 1 - H_q(r - \sqrt{r(r-\delta)}) \).

**练习 138** 假设 \( x^2 - 2rx + r\delta > 0 \)，\( w = \lfloor xn \rfloor \)，且 \( d = \lceil \delta n \rceil$，其中 \(\delta, x, \text{和 } n\) 为正数。证明当 $n$ 足够大时，\( w^2 - 2rnw + rnd > 0 \)。提示：利用 \( xn - 1 < w \le xn \) 和 \( \delta n - 1 < d \) 对 \( (w^2 - 2rnw + rnd)/n^2 \) 求下界。\(\unknown\)

**练习 139** 继续练习 137，在为 \( q = 2, q = 3, \text{和 } q = 4 \) 绘制的图中加入渐近埃利亚斯界不等式的图。（计算机绘图工具可能会有所帮助。）在每种情况下，对于哪些 \( \delta \) 的值，渐近埃利亚斯界比渐近辛格界、渐近普洛特金界和渐近汉明界更强？\(\unknown\)

## 2.10.5 MRRW 界

线性规划界有两个渐近版本，它们通常是 \( \alpha_q(\delta) \) 的最佳上界。这些界由 McEliece, Rodemich, Rumsey, and Welch [236] 发现。因此它们被称为 MRRW 界。其中第一个最初是为二进制码开发的，但已推广到任意域上的码；参见 Levenshtein [194, Theorem 6.19]。第二个仅适用于二进制码。第一个 MRRW 界，当仅考虑二进制码时，是第二个 MRRW 界的推论，如练习 141 所示。除练习 141 中展示的内容外，这些界的证明超出了本文的范围。同样，当 \( 1 - q^{-1} = r \le \delta \le 1 \) 时，\( \alpha_q(\delta) = 0 \)；MRRW 界仅适用于 \( 0 < \delta < r \).

