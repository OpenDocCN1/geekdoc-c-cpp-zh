
Define for $n \ge 0$ integer

$$\xi(n) = \exp -\lambda L \left[ \frac{h}{\lambda} \sum_{j=0}^{n+1} \frac{(\lambda L)^j}{j!} - \frac{p}{\lambda} \sum_{j=n+2}^{n+1+s} \frac{(\lambda L)^j}{j!} \right].$$

We have

$$\xi(n+1) - \xi(n) = \frac{(\lambda L)^{n+2}}{(n+2)!} \frac{\exp -\lambda L}{\lambda} \left[ h + p - p \frac{(\lambda L)^{-s}}{(n+3)\cdots(n+2-s)} \right].$$

Define $n_0 = n_0(s)$ to be the first positive integer such that

$$(n+3)\cdots(n+2-s) \ge \frac{p(L\lambda)^{-s}}{h+p}$$

### Lemma 14.5.
For $s \le 0$, there exists one and only one value $S$ which is a local minimum. i.e. such that

$$\psi'_s(S+0) \ge 0, \psi'_s(S-1+0) < 0.$$

The minimum $S$ is the unique value satisfying this condition

**PROOF.** $n_0$ is the minimum of $\xi(n)$. We first check that

(14.9.6) $$\xi(0) \ge 0 \Rightarrow \xi(n) \ge 0, \forall n.$$

Hence

$$\psi'_s(n+0) \text{ is increasing.}$$

If $\psi'_s(0+) \ge 0$, then $\psi'_s(n+0) \ge 0, \forall n$. Therefore $S=0$. If $\psi'_s(0+) < 0$, noting that $\psi'_s(n+0) > 0$, for $n$ sufficiently large, there exists one and only one $S$ satisfying the property of local minimum.

Let us prove the property (14.9.6). Note that

$$\xi(0) \ge 0 \Rightarrow h(1+\lambda L) \ge p \sum_{j=2}^{1+s} \frac{(\lambda L)^j}{j!}.$$

Therefore

$$\xi(n) \ge \frac{p \exp -\lambda L}{\lambda(1+\lambda L)} \left[ \sum_{j=2}^{1+s} \frac{(\lambda L)^j}{j!} \sum_{j=0}^{n+1} \frac{(\lambda L)^j}{j!} - \sum_{j=n+2}^{n+1+s} \frac{(\lambda L)^j}{j!} (1+\lambda L) \right].$$

Let us set

$$b_j = \frac{(\lambda L)^j}{j!}, \nu = 1+s \ge 1.$$

The positivity of $\xi(n)$ will be a consequence of the inequality

$$\sum_{j=0}^\nu b_j \sum_{k=0}^{n+1} b_k - \sum_{j=0}^{n+\nu} b_j \sum_{k=0}^{n+1} b_k$$

To prove the inequality it is enough to prove that

$$\frac{\sum_{j=0}^{n+\nu} b_j}{\sum_{k=0}^{n+1} b_k}$$

is decreasing in $n$.

Comparing the terms in $n$ and in $n+1$ this amounts to proving

$$b_{n+1+\nu} \sum_{k=0}^{n+1} b_k \le b_{n+2} \sum_{j=0}^{n+\nu} b_j,$$

and it is sufficient to prove

$$b_{n+1+\nu} \sum_{k=0}^{n+1} b_k \le b_{n+2} \sum_{j=\nu-1}^{n+\nu} b_j = b_{n+2} \sum_{k=0}^{n+1} b_{\nu-1+k}$$

It is thus sufficient to check that

$$\frac{b_k}{b_{n+2}} \le \frac{b_{\nu-1+k}}{b_{n+1+\nu}} \forall k \le n+1.$$

This results in checking the property

$$(k+1)\cdots(n+2) \le (k+\nu)\cdots(n+1+\nu), \forall k \le n+1,$$

which is satisfied.

It remains to consider the case $\xi(0) < 0$, in which case $\xi(n_0) < 0$.

Since $\xi(n) > 0$ for $n$ sufficiently large, there exists $S_1 > n_0$ such that

$$\xi(S_1) \ge 0, \xi(S_1 - 1) < 0.$$

Then

$$\xi(n) \ge 0 \forall n \ge S_1; \xi(n) < 0 \forall 0 \le n < S_1.$$

Therefore $S_1$ is uniquely defined.

Hence

$$\psi'_s(n+1+0) - \psi'_s(n+0) \ge 0, \forall n \ge S_1,$$

$$\psi'_s(n+1+0) - \psi'_s(n+0) < 0, \forall 0 \le n < S_1.$$

Therefore $S_1$ is the minimum of $\psi'_s(n+0)$. If this minimum is positive, we can conclude that $S=0$. If not, it is easily checked that there exists a unique local minimum $S > S_1$. This completes the proof.

We now turn to the case $s > 0$, in which case naturally $S(s) \ge s > 0$. We first compute the derivative

$$\psi'_s(x+0) = R_s([x]) = -pL + \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} \frac{(\lambda L)^j}{j!} ([x] - s - j + 1)$$

$$+ \frac{h+p}{\lambda} \exp -\lambda L \sum_{k=0}^{[x]-1} \frac{(\lambda L)^k}{k!} ([x] - s + 1)$$

$$+ \sum_{k=s}^{[x]} \frac{(\lambda L)^k}{k!} ([x] - k + 1) - \sum_{k=0}^{[x]-s} \frac{(\lambda L)^k}{k!} ([x] - k + 1 - s)$$

$$+ \exp -\lambda L \sum_{j=[x]+1-s}^{[x]} \sum_{m=0}^{[x]-j} \sum_{k=j+1}^{\infty} \left[ \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].$$

The function \(R_s(n), n \ge s\) is increasing in \(n\). We can indeed check

\(R_s(n+1) - R_s(n) = \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{n+1-s} \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=n+2-s}^{n+1} \frac{(\lambda L)^j}{j!} - \exp -\lambda L \sum_{m=0}^{s-1} \sum_{j=n+2-s}^{n+2-m} \frac{(\lambda L)^j}{j!} \frac{(\lambda L)^m}{m!} \right],\)

and

\(R_s(n+1) - R_s(n) \ge 0, \forall n \ge s\)

We next consider \(R_s(s), s \ge 0\). We first check

\(R_s(s) = -pL + \frac{h}{\lambda} \exp -\lambda L + \frac{h+p}{\lambda} \exp -\lambda L \left[ - \sum_{j=s+1}^{\infty} \frac{(\lambda L)^j}{j!} + \exp -\lambda L \sum_{j=0}^{s} \sum_{m=0}^{s-j} \sum_{k=1}^{\infty} \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].\)

It is easy to check that \(R_s(s)\) is an increasing function. We can proceed to define \(S(s)\) in a unique way. We shall need \(\hat{s}\) to be the first positive integer such that \(R_s(s) \ge 0\). This number is uniquely defined.

### Lemma 14.6.
For \(s > \hat{s}\) we have \(S(s) = s\) and for \(0 \le s \le \hat{s} S(s)\) is the first integer such that \(R_s(s) \ge 0\).

**Proof.** The proof is immediate from the monotonicity property of \(R_s(x)\).

## LITTLE'S LAW FOR THE LEAD TIME CASE.
We consider Little's law for positive lead time \(L\). Suppose that at starting time the initial stock is \(x\). Define successively

\(\theta = \inf\{t|x - D(t) \le 0\}; \quad \tau = \inf\{t|x - D(t) \le s\}.\)

Note that

\(D(\tau) - D(\theta) = -s, \text{ if } \tau \neq \theta, \tau \neq 0.\)

At time \(\tau\) an order is made of size \(S - s\) if \(\tau > 0\), and of size \(S - x\) if \(\tau = 0\). It is delivered at time \(\tau + L\). So after delivery the inventory is \(S - D(\tau + L) + D(\tau)\). Note that we assume \(s\) integer (positive or negative).

The possibility of backlog exists only when \(\theta < \tau + L\). Otherwise there is no backlog and no waiting time. If \(S - D(\tau + L) + D(\tau) > 0\) then the backlog is absorbed at time \(\tau + L\). If it is not positive, the population \(D(\tau + L) - D(\tau) - S\) has to wait till the next delivery. Defining

\(\tau_1 = \inf\{t \ge \tau + L|S - D(t) + D(\tau) \le s\} - \tau - L,\)

then this part of the population will be served at time \(\tau + L + \tau_1 + L\). Note that

\(S - D(\tau + L) + D(\tau) < s \Rightarrow \tau_1 = 0.\)

Moreover

\(S - D(\tau + L) + D(\tau) > s \Rightarrow S - D(\tau + L + \tau_1) + D(\tau) = s.\)

### Exercise 14.12.
Check the formula

\(\lambda E \tau_1 = E(S - s - D(\tau + L) + D(\tau))^+.\)

A cycle is the interval \(\min(\theta, \tau), \tau + L\). We consider the demands which arrive during a cycle, the backlog they constitute till they are served and the corresponding waiting time. If \(\theta > \tau + L\) there is no backlog and no waiting time. The population which is served at time \(\tau + L\) is

- \(-s + \min(S, D(\tau + L) - D(\tau))\) if \(\tau > 0\),
- \(-x + \min(S, D(L))\) if \(\tau = 0\).

If the inventory at \(\tau + L\) is negative then all demands during the cycle cannot be satisfied at time \(\tau + L\). The leftover will be served at time \(\tau + L + \tau_1\). Its level is \((S - D(\tau + L) + D(\tau))^-\). The average backlog can thus be expressed as

$$B = \int_0^1 (D(\theta) + \rho(\tau + L - \theta)^+ - D(\theta))\,d\rho + (S - D(\tau + L) + D(\tau))^- \frac{L}{\tau + L - \theta} + (S - D(\tau + L) + D(\tau))^- \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}}$$

Then the expected backlog is

$$EB = \frac{\lambda}{2} E(\tau + L - \theta)^+ + L E \frac{(S - D(\tau + L) + D(\tau))^-}{\tau + L - \theta} + E \left[ \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}} \frac{(S - D(\tau + L) + D(\tau))^-}{\tau + L - \theta} \right].$$

We can consider now the waiting time. First we note that the whole population has to wait during the cycle an average time \(\frac{1}{2}(\tau + L - \theta)^+\). In addition the carry over has to wait an additional time \(L + \tau_1\), where \(\tau_1\) can be 0. Weighting with the population ratios we obtain an expected average waiting time

$$EWT = \frac{1}{2} E(\tau + L - \theta)^+ + L E \frac{(S - D(\tau + L) + D(\tau))^-}{D(\tau + L) - D(\theta)} + E \left[ \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}} \frac{(S - D(\tau + L) + D(\tau))^-}{D(\tau + L) - D(\theta)} \right]$$

Little's Law:

$$EB = \lambda EWT,$$

is not verified. It is verified approximately if we neglect the probability of carry over. Namely we assume that

$$\text{Prob } \{D(\tau + L) - D(\tau) > S\} \sim 0,$$

which means

$$\sum_{j=S+1}^\infty \frac{(\lambda L)^j}{j!} \sim 0.$$

Another approximation consists in replacing the total population \(D(\tau + L) - D(\theta)\) by \(\lambda(\tau + L - \theta)\) in the coefficient of \((S - D(\tau + L) + D(\tau))^-\). These two random variables have the same expected value. With these approximations Little's Law remains valid. These approximations require a not too large lead time.
