Define

$$\rho = \int \Psi(z) \varpi(z) dz.$$

Consider now the equation

$$\Gamma(z) + \rho = \Psi(z) + E[\Gamma(z_2)|z_1 = z], \quad \int \Gamma(z) \varpi(z) dz = 0.$$

From ergodic theory, see Chapter 3, Theorem 3.3 we can assert that

$$\sup_z |\Gamma(z)| \le \sup_z |\Psi(z) - \rho| \frac{3-\beta}{1-\beta},$$

where \(0 < \beta < 1\), depends only on the Markov chain. Similarly, if we set

$$\rho_\alpha = \int \Psi_\alpha(z) \varpi(z) dz, \quad \bar{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1-\alpha},$$

we can write

$$\bar{\Gamma}_\alpha(z) + \rho_\alpha = \Psi_\alpha(z) + \alpha E[\bar{\Gamma}_\alpha(z_2)|z_1 = z],$$

we can also assert that

$$\sup_z |\bar{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3-\beta}{1-\beta}\\ \le 2 \left[ \left( \max(h, c) + \frac{\max(h, p)}{1-\delta(m_0)} \right) m_0 + pc_1 \right] \frac{3-\beta}{1-\beta}$$

Moreover

$$\bar{\Gamma}_\alpha(z) - \bar{\Gamma}_\alpha(z') = \Psi_\alpha(z) - \Psi_\alpha(z') + \alpha \int \bar{\Gamma}_\alpha(\zeta) (f(\zeta|z) - f(\zeta|z')) d\zeta.$$

Using properties (12.2.40), (12.2.43) and the assumption (12.2.29), we can check that

$$|\Psi_\alpha(z) - \Psi_\alpha(z')| \le C(m_0) \delta |z - z'|,$$

and thus also

$$|\bar{\Gamma}_\alpha(z) - \bar{\Gamma}_\alpha(z')| \le C_1(m_0) \delta |z - z'|.$$

Therefore the functions \(\bar{\Gamma}_\alpha(z)\) are uniformly Lipschitz continuous and bounded. It follows that for a subsequence we obtain

(12.2.50) $$\sup_{0 \le s \le N} \left| \Gamma_\alpha(z) - \frac{\rho_\alpha}{1-\alpha} - \Gamma(z) \right| \to 0, \forall M$$

Therefore, also

(12.2.51) $$\sup_{\substack{0 \le x \le M \\ 0 \le z \le N}} \left| u_\alpha(x, z) - \frac{\rho_\alpha}{1-\alpha} - u(x, z) \right| \to 0, \forall x, \forall M, N$$

with

(12.2.52) $$u(x, z) = (h - c)x + \int_0^x \chi(\xi, z) d\xi + \Gamma(z).$$

We deduce

(12.2.53) $$u(x, z) = (h - c)x + \Gamma(z), \forall x \le S(z).$$