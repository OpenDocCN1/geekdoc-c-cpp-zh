Let us next define \(\Gamma_a(z) = u_a(0, z)\). We have
\(\begin{aligned}
\Gamma_a(z) &= G_a(s_a(z), z) \\
&= c s_a(z) + p E[(s_a(z) - z_2)^- | z_1 = z] + \alpha E[u_a((s_a(z) - z_2)^+, z_2) | z_1 = z] \\
&= g_a(s_a(z), z) + \alpha E \left[ \int_0^{(s_a(z) - z_2)^+} \chi_a(\xi, z_2) d\xi | z_1 = z \right] + \alpha E[\Gamma_a(z_2) | z_1 = z]
\end{aligned}\)

Therefore we can write
(12.4.34) \(\Gamma_a(z) = \Psi_a(z) + \alpha E[\Gamma_a(z_2) | z_1 = z],\)

with
\(\Psi_a(z) = g_a(s_a(z), z) + \alpha E \left[ \int_0^{(s_a(z) - z_2)^+} \chi_a(\xi, z_2) d\xi | z_1 = z \right].\)

Thanks to Lemma 12.3, we have the estimate (12.4.27), so \(s_a(z) \le m_0\). Using the estimate (12.4.33), we see that \(|\Psi_a(z)| \le C\). Let us then define
\(\rho_a = \int \Psi_a(z) \varpi(z) dz,\)

and \(\bar{\Gamma}_a(z) = \Gamma_a(z) - \frac{\rho_a}{1 - \alpha}\). From ergodic theory, we can assert that
\(\sup_z |\bar{\Gamma}_a(z)| \le \sup_z |\Psi_a(z) - \rho_a| \frac{3 - \beta}{1 - \beta} \le C,\)

and we can state the estimate
\(\left| u_a(x, z) - \frac{\rho_a}{1 - \alpha} \right| \le C + \frac{Cx}{1 - \delta_0(x)}.\)

Define \(\tilde{u}_a(x, z) = u_a(x, z) - \frac{\rho_a}{1 - \alpha}\). We write equation (12.4.1) as
(12.4.35) \(\tilde{u}_a(x, z) + \rho_a = \inf_{v \ge 0} [K \mathbf{1}_{v>0} + l(x, z, v) + \alpha \Phi^v \tilde{u}_a(x, z)].\)

From Lemma 12.3 we can assert that the optimal feedback satisfies \(x + \tilde{u}_a(x, z) \le \max(x, m_0)\). Therefore we can replace (12.4.35) by
\(\begin{aligned}
\tilde{u}_a(x, z) + \rho_a &= \inf_{x+v \le \max(x, m_0)} [K \mathbf{1}_{v>0} + l(x, z, v) + \alpha \Phi^v \tilde{u}_a(x, z)] \\
&= \inf_{0 \le v \le \max(x, m_0) - x} L_a(x, z, v).
\end{aligned}\)

Next
\(L_a(x, z, v) - L_a(x, z', v) = \int [p(x+v-\zeta)^+ - \alpha \tilde{u}_a((x+v-\zeta)^+, \zeta)] (f(z|\zeta) - f(z'|\zeta)) d\zeta\)

For \(v \le \max(x, m_0) - x\) we can write
\(\begin{aligned}
|\tilde{u}_a((x+v-\zeta)^+, \zeta)| \le C + \frac{C \max(x, m_0)}{1 - \delta_0(\max(x, m_0))} \\
\le C'_1 + \frac{C_2 x}{1 - \delta_0(x)}
\end{aligned}\)

Using the assumption (12.4.23) we get easily
\(|\tilde{u}_a(x, z) - \tilde{u}_a(x, z')| \le \left( C_1 + \frac{C_2 x}{1 - \delta_0(x)} \right) |\delta z - z'|.\)