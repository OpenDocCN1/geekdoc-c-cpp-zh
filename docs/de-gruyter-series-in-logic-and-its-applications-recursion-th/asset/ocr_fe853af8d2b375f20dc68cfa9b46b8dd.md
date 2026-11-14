# Claim 1. $\tilde{g}_{O, \tau+1}(j_0) \ge \tilde{g}_{O, \tau}(j_0)$ for any $t > t_0 + 1$ and hence $\lim_{t \to \omega} \tilde{g}_{O, t}(j_0) = +\infty$.

Proof. If we assign a new value $k$ to $\tilde{g}_{O, t}(j_0)$ at some stage $\alpha_t > \alpha_{t+1}$, it must be the case that $\tilde{g}_{O, \tau}(0)^\frown \cdots \frown \tilde{g}_{O, \tau}(j_0 - 1)^\frown k \in T_2[\alpha_t]$. However, $\tilde{g}_{O, \tau}(0)^\frown \cdots \frown \tilde{g}_{O, \tau}(j_0 - 1) \in T_2[\alpha_t]$ by the assumption on $j_0$, so that $k > \tilde{g}_{O, \tau+1}(j_0)$. 

Claim 1 implies that at infinitely many $t$'s, left turns were selected at locally splitting nodes in $T_0[\alpha_t]$ during the decoding phase for the purpose of approximating $f_O(j_0)$. 

Let $\sigma = \sigma_{0, j_0}^{\langle \alpha_t \rangle}[\alpha_t]$ and $\tau = \tau_{0, j_0}[\alpha_t]$. Note that $|\sigma| > |\tau|$. Define

$X = \{x > \bar{\sigma} \mid \forall n \tau \beta < y \exists \beta' \exists \tau' > \tilde{\tau} \beta \le \beta' < \gamma \land |\tau'| = n \land (x | n, \tau') \in T_0[\beta']\}$.

If we let $\tilde{p}(\tau) = \{ \sigma \mid \exists \sigma (\sigma, \tau) \in T$ is a "local projection" of a tree $T \subseteq \tau^{<\omega} \times \omega^{<\omega}$, then it is not difficult to see that $\cap_{\beta < \gamma} p(T_0[\tilde{\sigma}, \tilde{\tau}][\beta])$ is a tree (Note: $T_0[\tilde{\sigma}, \tilde{\tau}][\beta]$ denotes the analog of $T_0[\tilde{\sigma}, \tilde{\tau}]$ for $T_0[\beta]$). Moreover,

$X = \bigcap_{\beta < \gamma} \tilde{p}(T_0[\tilde{\sigma}, \tilde{\tau}][\beta])$ .

In other words, $X$ consists of all the reals $x$ "potentially" with an accompanying witness $f$ so that $(x, f)$ is an infinite path in $T_0[\tilde{\sigma}, \tilde{\tau}][\gamma]$. Note that since $\gamma < \omega_1^{CK}$, $X$ is a $\Delta_1^1$ closed subset of $2^\omega$.

# Claim 2. $x_0$ is the leftmost path in $X$.

Proof. Suppose not. Then there exist $y_0$ and $\sigma$ such that $\tilde{\sigma} < \sigma$, $y_0 \succ^* 0$, $x_0 \succ^* 1$, and $\forall \beta < y \exists \beta' \exists \tau' > \tilde{\tau} (\beta \le \beta' < \gamma \land |\tau'| = |\sigma| + 1 \land (y_0 | |\sigma| + 1, \tau') \in T_0[\beta'])$.

Now by Claim 1 let $t_1 > t_0$ be such that $\tilde{g}_{O, t}(j_0) > |\sigma| + 1$ for all $t \ge t_1$. Then there are $\tau, \tau'$ of length $|\sigma|$ so that $(x_0 | |\sigma| + 1, \tau, (y_0 | |\sigma| + 1, \tau') \in T_0[\alpha_{t+1}]$. However, since $y_0$ is to the left of $x_0$, the value of $\tilde{g}_{O, t+1}(j_0)$ coded by $x_0$ is at most $|\sigma| + 1$. Thus $\tilde{g}_{O, t+1}(j_0) \le |\sigma| + 1$, a contradiction.

Claim 2 implies that $x_0$ is hyperarithmetic which is a contradiction. Hence there is a $t^0$ such that for any $t \ge t^0$, $\tilde{g}_{O, t}(j_0) = \tilde{g}_{O, t+1}(j_0)$ and so $\sigma_{0, j_0}^{\langle \alpha_{t+1} \rangle}[\alpha_t]$ is a constant for all $t > t^0$.

We leave it to the reader to verify the stabilization of the other sequences of parameters.

It follows that for each $j$, there is a $t_j$ such that $\tilde{g}_{O, t}(j) = \tilde{g}_{O, t}(j) = f_O^j(\alpha_t)$ for $t \ge t_j$. Define $\tilde{g}(j) = \lim_{t \to \omega} \tilde{g}_{O, t}(j)$ for $j \in \omega$. Then $\tilde{g}(j) = \lim_{t \to \omega} f_O^j(\Omega)[t]$ and $\tilde{g} \in L_{\gamma+1}$. Now $\tilde{g}$ is the leftmost path in $T_2[\gamma]$ and so in $T_2$ as well. Thus $\tilde{g} = f_O \in L_{\gamma+1}$. This contradicts the assumption that $\gamma < \omega_1^{CK}$. Hence $\gamma = \omega_1^{CK}$ and so $f_O = x_0 \le_h x_1$.

Using this, one may decode by the entire construction in $T_1[\omega_1^{CK}]$ and conclude that $z \le_h x_0 \oplus x_1$, completing the proof of the Theorem.