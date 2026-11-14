Therefore

\(E\hat{y}_{n+1} \le E\hat{y}_n + \frac{p c_0^2 z}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)},\)

and we deduce the estimate

\(E\hat{y}_{n+1} \le x + \frac{p z c_0}{c(1-c_0 \alpha)} \frac{1-c_0^n}{1-c_0} + \frac{n p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)

Using again the assumption (12.2.12), we deduce the first part of (12.2.18). This completes the proof.

# 12.2.2. BASE-STOCK POLICY.

We want now to check that the optimal feedback \(\hat{v}(x, z)\) can be obtained by a base stock policy, with a base stock depending on the value of \(z\). We have the

# Theorem 12.2.

We make the assumptions of Theorem 12.1 and \(p > c\). We assume also

(12.2.19) \(f(x, z) \ge a_0(M) > 0, \forall x, z \le M.\)

Then the function \(u(x, z)\) is convex and \(C^1\) in the argument \(x\). Moreover the optimal feedback is given by

(12.2.20) \(\hat{v}(x, z) = \begin{cases} S(z) - x, & \text{if } x \le S(z) \\ 0, & \text{if } x \ge S(z) \end{cases}\)

The function \(S(z)\) is uniformly continuous and the derivative in \(x\), \(u'(x, z)\) is uniformly continuous.

PROOF. We consider the increasing process

\(u_{n+1}(x, z) = \inf_{v \ge 0} [\langle x, z, v \rangle + \alpha \Phi^u u_n(x, z)], \quad u_0(x) = 0\)

which we write also as

\(u_{n+1}(x, z) = (h - c)x + \inf_{\eta \ge z} \{c\eta + p E[(\eta - z_2)^-] \mid z_1 = z\} + \alpha E[u_n((\eta - z_2)^+, z_2) \mid z_1 = z],\)

and we are going to show recursively that the sequence \(u_n(x, z)\) is convex and \(C^1\) in \(x\). Define

\(G_n(x, z) = cx + p E[(x - z_2)^- \mid z_1 = z] + \alpha E[u_n((x - z_2)^+, z_2) \mid z_1 = z],\)

then the function \(G_n(x, z)\) attains its minimum in \(S_n(z)\), which can be uniquely defined by taking the smallest minimum. We first consider

\(G_0(x, z) = cx + p E[(x - z_2)^- \mid z_1 = z].\)

It is convex and \(C^1\) in \(x\). We have

\(G'_0(x, z) = c - p \bar{F}(x|z),\)

with

\(\bar{F}(x|z) = \int_x^\infty f(\xi|z) d\xi.\)