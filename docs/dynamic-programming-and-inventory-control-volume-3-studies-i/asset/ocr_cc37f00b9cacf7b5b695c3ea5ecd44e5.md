The function \(R_s(n), n \ge s\) is increasing in \(n\). We can indeed check

\(R_s(n+1) - R_s(n) = \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{n+1-s} \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=n+2-s}^{n+1} \frac{(\lambda L)^j}{j!} - \exp -\lambda L \sum_{m=0}^{s-1} \sum_{j=n+2-s}^{n+2-m} \frac{(\lambda L)^j}{j!} \frac{(\lambda L)^m}{m!} \right],\)

and

\(R_s(n+1) - R_s(n) \ge 0, \forall n \ge s\)

We next consider \(R_s(s), s \ge 0\). We first check

\(R_s(s) = -pL + \frac{h}{\lambda} \exp -\lambda L + \frac{h+p}{\lambda} \exp -\lambda L \left[ - \sum_{j=s+1}^{\infty} \frac{(\lambda L)^j}{j!} + \exp -\lambda L \sum_{j=m=0}^{s-j} \sum_{k=1}^{\infty} \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].\)

It is easy to check that \(R_s(s)\) is an increasing function. We can proceed to define \(S(s)\) in a unique way. We shall need \(\hat{s}\) to be the first positive integer such that \(R_s(s) \ge 0\). This number is uniquely defined.

**Lemma 14.6.** For \(s > \hat{s}\) we have \(S(s) = s\) and for \(0 \le s \le \hat{s} S(s)\) is the first integer such that \(R_s(s) \ge 0\).

**Proof.** The proof is immediate from the monotonicity property of \(R_s(x)\).

LITTLE'S LAW FOR THE LEAD TIME CASE. We consider Little's law for positive lead time \(L\). Suppose that at starting time the initial stock is \(x\). Define successively

\(\theta = \inf\{t|x - D(t) \le 0\}; \quad \tau = \inf\{t|x - D(t) \le s\}.\)

Note that

\(D(\tau) - D(\theta) = -s, \text{ if } \tau \neq \theta, \theta, \tau \neq 0.\)

At time \(\tau\) an order is made of size \(S - s\) if \(\tau > 0\), and of size \(S - x\) if \(\tau = 0\). It is delivered at time \(\tau + L\). So after delivery the inventory is \(S - D(\tau + L) + D(\tau)\). Note that we assume \(s\) integer (positive or negative).

The possibility of backlog exists only when \(\theta < \tau + L\). Otherwise there is no backlog and no waiting time. If \(S - D(\tau + L) + D(\tau) > 0\) then the backlog is absorbed at time \(\tau + L\). If it is not positive, the population \(D(\tau + L) - D(\tau) - S\) has to wait till the next delivery. Defining

\(\tau_1 = \inf\{t \ge \tau + L|S - D(t) + D(\tau) \le s\} - \tau - L,\)

then this part of the population will be served at time \(\tau + L + \tau_1 + L\). Note that

\(S - D(\tau + L) + D(\tau) < s \Rightarrow \tau_1 = 0.\)

Moreover

\(S - D(\tau + L) + D(\tau) > s \Rightarrow S - D(\tau + L + \tau_1) + D(\tau) = s.\)

**Exercise 14.12.** Check the formula

\(\lambda E \tau_1 = E(S - s - D(\tau + L) + D(\tau))^+.\)