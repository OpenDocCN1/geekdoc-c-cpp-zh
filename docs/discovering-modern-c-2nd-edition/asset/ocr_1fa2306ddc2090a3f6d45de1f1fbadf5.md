| Name | Precond. | Result |
| :--- | :--- | :--- |
| `assoc_legendre (l, m, x)` | for \(|x| \ge 0\) | \(\mathrm{P}_n^m(x) = (1 - x^2)^{m/2} \frac{d^m}{dx^m} \mathrm{P}_l(x)\) |
| `beta (x, y)` | for \(x, y > 0\) | \(\mathrm{B}(x, y) = \frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)}\) |
| `comp_ellint_1 (k)` | for \(|k| \le 1\) | \(\mathrm{K}(k) = \mathrm{F}(k, \pi/2)\) |
| `comp_ellint_2 (k)` | for \(|k| \le 1\) | \(\mathrm{E}(k) = \mathrm{E}(k, \pi/2)\) |
| `comp_ellint_3 (k, nu)` | for \(|k| \le 1\) | \(\Pi(\nu, k) = \Pi(\nu, k, \pi/2)\) |
| `cyl_bessel_i_ (nu, x)` | for \(x \le 0\) | \(\mathrm{Iv}(x) = \mathrm{i}^{-\nu} \mathrm{J}_\nu(\mathrm{i}x)\) |
| `cyl_bessel_j_ (nu, x)` | for \(x \le 0\) | \(\mathrm{J}_\nu(x) = \sum_{k=0}^\infty \frac{(-1)^k (x/2)^{\nu+2k}}{k! \Gamma(\nu+k+1)}\) |
| `cyl_bessel_k_ (nu, x)` | for \(x \ge 0\) | \(\mathrm{Kv}(x) = (\pi/2)\mathrm{i}^{\nu+1}(\mathrm{J}_\nu(\mathrm{i}x) + \mathrm{i}\mathrm{N}_\nu(\mathrm{i}x))\) |
| `cyl_neumann(n u, x)` | for \(x \ge 0\) | \(\mathrm{N}_\nu(x) = \frac{\mathrm{J}_\nu(x) \cos \nu\pi - \mathrm{J}_{-\nu}(x)}{\sin \nu\pi}\) |
| `cyl_neumann(n u, x)` | for \(x \ge 0\) | \(\mathrm{N}_\nu(x) = \lim_{\mu \to \nu} \frac{\mathrm{J}_\mu(x) \cos \mu\pi - \mathrm{J}_{-\mu}(x)}{\sin \mu\pi}\) |
| `ellint_1(k, phi)` | for \(|k| \le 1\) | \(\mathrm{F}(k, \varphi) = \int_0^\varphi \frac{d\theta}{\sqrt{1-k^2\sin^2\theta}}\) |
| `ellint_2(k, phi)` | for \(|k| \le 1\) | \(\mathrm{E}(k, \varphi) = \int_0^\varphi \sqrt{1-k^2\sin^2\theta} \, d\theta\) |
| `ellint_3(k, nu, phi)` | for \(|k| \le 1\) | \(\mathrm{E}(k, \nu, \varphi) = \int_0^\varphi \frac{d\theta}{(1-\nu\sin^2\theta)\sqrt{1-k^2\sin^2\theta}}\) |
| `expint(x)` | | \(\mathrm{Ei}(x) = \int_{-x}^\infty \frac{e^{-t}}{t} dt\) |