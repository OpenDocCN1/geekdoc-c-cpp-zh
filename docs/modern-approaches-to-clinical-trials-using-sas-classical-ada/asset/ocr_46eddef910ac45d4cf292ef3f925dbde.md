$\frac{\partial p_C}{\partial p_E} = \frac{ho(1-p_E)}{2p_E}$ and $\frac{\partial p_E}{\partial p_C} = \frac{ho(1-p_C)}{2p_C}$. One can easily show that the lower bound for the variance of $N_E(m)/m$ (the asymptotic variance of ERADE) is

```
$\sigma^2_{ERADE} = \frac{1}{4(\sqrt{p_E}+\sqrt{p_C})^2}\left(\frac{ho p_C}{\sqrt{p_E}} + \frac{ho p_E}{\sqrt{p_C}}ight). \quad (10.9)$
```

The asymptotic variance of DBCD($\gamma$) (Section 10.3.3) is

```
$\sigma^2_{DBCD(\gamma)} = \frac{\sqrt{p_Ep_C}}{(1+\gamma)(\sqrt{p_E}+\sqrt{p_C})^2} + \frac{2(1+\gamma)}{1+2\gamma}\sigma^2_{ERADE}. \quad (10.10)$
```

The asymptotic variance of the SMLE procedure, $\sigma^2_{SMLE}$, is obtained by calculating $\sigma^2_{DBCD(\gamma)}$ with $\gamma=0$. Clearly, $\sigma^2_{SMLE} > \sigma^2_{DBCD(\gamma=2)} > \sigma^2_{ERADE}$:

Figure 10.2 is a plot of asymptotic variance $N_E(m)/m$ of three RAR designs (SMLE, DBCD($\gamma$), and ERADE) for a range of scenarios when $p_C=0.4$ and $0.2 \le p_E \le 0.9$. Interestingly, the variance is monotone decreasing as $p_E$ is increasing from 0.2 to 0.9. For SMLE the variance is decreasing from 0.6 to 0.38; for DBCD($\gamma=2$) it is decreasing from 0.26 to 0.12; and for ERADE it is decreasing from 0.18 to 0.06. For a completely randomized design (CRD) targeting 1:1 allocation (a non-adaptive procedure for which every allocation is made independently with probability 1/2), the variance is constant, 0.25, for any values of $p_C$ and $p_E$. As such, in the considered scenarios both DBCD($\gamma=2$) and ERADE are overall less variable than CRD.

# Figure 10.2 Asymptotic Variance of the Sample Proportion for Three RAR Designs