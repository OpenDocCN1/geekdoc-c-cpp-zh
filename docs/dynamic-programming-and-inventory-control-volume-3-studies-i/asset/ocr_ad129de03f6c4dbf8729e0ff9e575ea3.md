**Theorem 12.1.** We assume (12.2.1), (12.2.2), (12.2.6), (12.2.12). Then there exists one and only one solution of equation (12.2.14), such that \(0 \le u \le w_0\). It is continuous and coincides with the value function (12.2.8). There exists an optimal feedback \(\hat{v}(x,z)\) and an optimal control policy \(\hat{V}\).

**PROOF.** We first notice that conditions of Theorem 4.4 and 4.3 are satisfied. Hence the set of solutions of equation (12.2.14) is not empty. It has a minimum and a maximum solution. The minimum solution is l.s.c. and the maximum solution is u.s.c. The minimum solution coincides with the value function. There exists an optimal feedback \(\hat{v}(x,z)\) and an optimal control policy \(\hat{V}\). To prove uniqueness, we have to prove that the minimum and maximum solutions coincide. We begin by proving a bound on \(\hat{v}(x,z)\). It will be first convenient to mention a slightly better estimate for \(w_0\). Indeed, we can write

\(\text{(12.2.15)} \quad w_0(x,z) \le h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z) + \frac{p c_0 z}{1-c_0 \alpha} + \frac{p c_1}{(1-\alpha)(1-c_0 \alpha)},\)

and (12.2.13) was simply derived from (12.2.15) by using \(\Phi^0(x,x) \le x\). Next, from (12.2.14), considering \(\underline{u}\), the minimum solution, we can state that

\(\underline{u}(x,z) \ge h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z),\)

which follows from \(l(x,z,v) \ge hx\), and

\(\text{(12.2.16)} \quad \Phi^v \varphi(x,z) \ge \Phi^0 \varphi(x,z), \forall v \ge 0, \forall \varphi \text{ increasing in } x.\)

Therefore, we can write

\(l(x,z,v) + \alpha \Phi^v \underline{u}(x,z) \ge c v + h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z).\)

Therefore, in minimizing in \(v\), we can bound from above the range of \(v\). More precisely, we get

\(\text{(12.2.17)} \quad \hat{v}(x,z) \le \frac{p c_0 z}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)

We consider the optimal trajectory \(\hat{y}_n, z_n\) obtained from the optimal feedback, namely

with \(\hat{y}_1 = x, z_1 = z\).

Following section 4.5 of Chapter 4, the maximum solution will coincide with the minimum solution, if we can check that \(\hat{V} \in \mathcal{V}\), i.e.

\(\alpha^n E \hat{u}(y_{n+1}, z_{n+1}) \to 0, \text{ as } n \to \infty\)

It is sufficient to replace \(\hat{u}\) by \(w_0\) and by the estimate (12.2.13), it is sufficient to show that

\(\text{(12.2.18)} \quad \alpha^n E \hat{y}_{n+1}, \quad \alpha^n E z_{n+1} \to 0, \text{ as } n \to \infty.\)

However, by standard Markov arguments, \(\alpha^n E z_{n+1} \le (\alpha c \alpha)^n z\). From the assumption (12.2.12), the second part of (12.2.18) follows immediately. We next use

\(\hat{y}_{n+1} \le \hat{y}_n + \hat{v}_n\)
\(\le \hat{y}_n + \frac{p c_0 z_n}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)