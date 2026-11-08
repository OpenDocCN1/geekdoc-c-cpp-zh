$$R_n(t)=\left(\sum_H r^H\mid r^H<0\right)/c\cdot((T+1)-T). \tag{4}$$

$$R_p(t)=\left(\sum_H r^H\mid r^H>0\right)/c\cdot((T+1)-T). \tag{5}$$

The differences of the population densities $r^H$ are added to the negative growth rates ($R_n$), if $r^H<0$, and otherwise, if $r^H>0$, $r^H$ is added to the positive growth rates ($R_p$). If the model time is scaled to one month, for the denominator in equation 4 and 5 the value $12\cdot(1918-1888)=360$ results for the first simulation period.

At which cells the population density rises or falls is defined by assessment curves for moving away from or moving into individual inhabitants. These curves indicate which areas are evaluated as the least attractive ones by the current inhabitants due to the density and supply values of these locations and therefore that a decline in population is probable, or which areas are evaluated as the most attractive ones by the current inhabitants for the same reasons and therefore that an increase of population is probable. The probability $\rho$ for moving away from a cell or moving to a cell of an inhabitant results from the assessment functions $\rho_D$ for the population density and $\rho_V$ for the supply potential of a cell:

$$\rho^H(t)=\left(\rho_D^H(t)+\rho_V^H(t)\right)/2. \tag{8}$$

Following Krugmann (1996), the assessment function for the population density ($\rho_D$) results from a trade-off between two exponential functions for calculation of a centripetal $F_{\text{in}}$ and a centrifugal $F_{\text{out}}$ force:

$$\rho_D^H(t)=F_{\text{in}}^H(t)-F_{\text{out}}^H(t). \tag{7}$$

To simplify equation 7 we use the beta distribution¹ for the calculation of $\rho_D$ which allows one to model an assessment curve with 2 instead of 4 control parameters. This will be relevant in chapter 6 where the search for optimal parameter settings is described. Since we assume different assessment curves for moving away from a cell or moving to a cell, equation 6 is to be distinguished in two cases, which in the following are indicated with $\rho_{D\_out}$ for the moving-away-from-curve and with $\rho_{D\_in}$ for the moving-to-curve:

$$\rho_{D\_out}^H(t)=\frac{1}{B(p_{out},q_{out})}\cdot x^{p_{out}-1}(1-x)^{q_{out}-1},$$
$$\rho_{D\_in}^H(t)=\frac{1}{B(p_{in},q_{in})}\cdot x^{p_{in}-1}(1-x)^{q_{in}-1}. \tag{8}$$

¹ cf. Wikipedia: http://en.wikipedia.org/wiki/Beta_distribution (last visited at 09.07.2008)