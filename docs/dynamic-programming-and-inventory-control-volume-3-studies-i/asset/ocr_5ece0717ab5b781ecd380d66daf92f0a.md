with
\[
\Psi_\alpha(z) = g_\alpha(s_\alpha(z), z) + \alpha E \left[ \int_{-m_0}^{s_\alpha(z)-z_2} \chi_\alpha(\xi, z_2) d\xi | z_1 = z \right].
\]

We note that \(|s_\alpha(z)| \le m_0\). Using the estimate (12.5.36), we see that \(|\Psi_\alpha(z)| \le C\). Let us then define
\[
\rho_\alpha = \int \Psi_\alpha(z) \varpi(2) dz,
\]

and \(\bar{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1-\alpha}\). From ergodic theory, we can assert that
\[
\sup_z |\bar{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3-\beta}{1-\beta} \le C,
\]

and we can state the estimate
\[
\left| u_\alpha(x, z) - \frac{\rho_\alpha}{1-\alpha} \right| \le C + \frac{C(x+m_0)^+}{1-\delta_0((x+m_0)^+)} + C(x+m_0)^-.
\]

Define \(\tilde{u}_\alpha(x, z) = u_\alpha(x, z) - \frac{\rho_\alpha}{1-\alpha}\). We write equation (12.5.1) as
(12.5.39) \(\tilde{u}_\alpha(x, z) + \rho_\alpha = \inf_{v \ge 0} [K \mathbf{1}_{v>0} + l(x, v) + \alpha \Phi^v \tilde{u}_\alpha(x, z)].\)

From Lemma 12.4 we can assert that the optimal feedback satisfies
\[
\max(-m_0, x) \le x + \hat{v}(x, z) \le \max(x^+, m_0).
\]

Therefore we can replace (12.5.39) by
\[
\begin{aligned}
\tilde{u}_\alpha(x, z) + \rho_\alpha &= \inf_{\max(-m_0, x) \le x+v \le \max(x^+, m_0)} [K \mathbf{1}_{v>0} + l(x, v) + \alpha \Phi^v \tilde{u}_\alpha(x, z)] \\
&= \inf_{\max(-m_0, x) \le x+v \le \max(x^+, m_0)} L_\alpha(x, z, v).
\end{aligned}
\]

Next
\[
L_\alpha(x, z, v) - L_\alpha(x, z', v) = \alpha \int \tilde{u}_\alpha(x+v-\zeta, \zeta) (f(\zeta|z) - f(\zeta|z')) d\zeta
\]

For \(\max(-m_0, x) \le x \le v \le \max(x^+, m_0)\) we can write
\[
|\tilde{u}_\alpha(x+v-\zeta, \zeta)| \le C + \frac{C(\max(x^+, m_0)+m_0)}{1-\delta_0(\max(x^+, m_0)+m_0)} + C\zeta
\]

Using the assumptions (12.5.23) and (12.5.24) we get easily
\[
|\tilde{u}_\alpha(x, z) - \tilde{u}_\alpha(x, z')| \le \left( C + \frac{C(\max(x^+, m_0)+m_0)}{1-\delta_0(\max(x^+, m_0)+m_0)} \right) \delta|z-z'|.
\]

From the estimates obtained we can assert that \(\tilde{u}_\alpha(x, z)\) has a converging subsequence (still denoted \(\alpha\)) in the sense
(12.5.40) \(\sup_{|x| \le M, z \le N} |\tilde{u}_\alpha(x, z) - u(x, z)| \to 0, \text{ as } \alpha \to 0.\)

Since \(\rho_\alpha\) is bounded, we can always assume that \(\rho_\alpha \to \rho\). Denote
\[
L(x, z, v) = K \mathbf{1}_{v>0} + l(x, v) + \Phi^v u(x, z)
\]

then
\[
L_\alpha(x, z, v) - L(x, z, v) = \alpha \Phi^v (\tilde{u}_\alpha - u)(x, z) - (1-\alpha) \Phi^v u(x, z)
\]