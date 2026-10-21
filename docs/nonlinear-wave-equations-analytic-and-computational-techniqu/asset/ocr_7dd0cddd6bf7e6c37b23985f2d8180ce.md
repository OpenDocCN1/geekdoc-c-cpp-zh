corresponding to the bottom wall. This is convenient for computing the Dirichlet-Neumann operator [49]. In the formula for \(\hat{\varphi}_k\), the minus sign is taken if \(k < 0\) so that \(\hat{\varphi}_{-k}=\overline{\hat{\varphi}_k}\). We also solve for the period,

(3.5) \[ T = c_{n+1}. \]

The phase shift \(\theta\) is taken as a prescribed parameter here. Alternatively, in a study of traveling-standing waves [48], the author defines a traveling parameter \(\beta\) and varies \(\theta = c_{n+2}\) as part of the algorithm to obtain the desired value of \(\beta\). This parameter \(\beta\) is less meaningful for solitary wave collisions in shallow water, so we use \(\theta\) itself as the traveling parameter in the present study. We also need to specify the amplitude of the wave. This can be done in various ways, e.g. by specifying the value of the energy,

\[ E = \frac{1}{2\pi}\int_0^{2\pi} \tfrac12 \varphi \mathcal{G}\varphi + \tfrac12 g\eta^2 \,dx, \]

by constraining a Fourier mode such as \(\hat{\eta}_1(0)\), or by specifying the initial height of the wave at \(x=0\):

\[ \eta(0,0)=\hat{\eta}_0+\sum_{k=1}^{n/2}2c_{2k-1}. \]

Thus, to enforce (3.3), we can minimize the objective function

(3.6) \[ f(c)=\tfrac12 r(c)^T r(c), \]

where

(3.7) \[ r_1 = (\text{choose one:}\quad E-a\quad ,\quad \hat{\eta}_1(0)-a\quad ,\quad \eta(0,0)-a), \]
\[ r_{2j}=\operatorname{Im}\{e^{ij\theta/2}\hat{\eta}_j(T/2)\},\qquad r_{2j+1}=\operatorname{Re}\{e^{ij\theta/2}\hat{\varphi}_j(T/2)\},\qquad (1\le j\le M/2). \]

Here \(a\) is the desired value of the chosen amplitude parameter. Alternatively, we can impose (3.2) directly by minimizing

(3.8) \[ \tilde f = \tfrac12 r_1^2 + \tfrac{1}{4\pi}\int_0^{2\pi}\Big(\big[\eta(x,T)-\eta(x-\theta,0)\big]^2 + \big[\varphi(x,T)-\varphi(x-\theta,0)\big]^2\Big)\,dx, \]

which also takes the form \(\tfrac12 r^T r\) if we define \(r_1\) as above and

(3.9) \[ r_{4j-2}+i r_{4j-1}=\sqrt{2}\,\big[\hat{\eta}_j(T)-e^{-ij\theta}\hat{\eta}_j(0)\big], \]
\[ r_{4j}+i r_{4j+1}=\sqrt{2}\,\big[\hat{\varphi}_j(T)-e^{-ij\theta}\hat{\varphi}_j(0)\big],\qquad (1\le j\le M/2). \]

Note that \(f\) measures deviation from evenness and oddness of \(\eta(x+\theta/2,T/2)\) and \(\varphi(x+\theta/2,T/2)\), respectively, while \(\tilde f\) measures deviation of \(\eta(x+\theta,T)\) and \(\varphi(x+\theta,T)\) from their initial states. In the first example of §4, we minimize \(\tilde f\) directly, while in the second we minimize \(f\) and check that \(\tilde f\) is also small, as a means of validation. The number of equations, \(m=M+1\) for \(f\) and \(m=2M+1\) for \(\tilde f\), is generally larger than the number of unknowns, \(n+1\), due to zero-padding of the initial conditions. This adds robustness to the shooting method and causes all Fourier modes varied by the algorithm, namely those in (3.4), to be well-resolved on the mesh.