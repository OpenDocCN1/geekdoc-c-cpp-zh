It should be emphasized that (3.79) is the canonical Black–Literman reference model, and not (3.76).

# Remarks:

+   1. A common misconception about the Black–Literman model is that (3.76) is the reference model, and also
+   2. $\mu$ is a point estimate in the model.

# Computing the Equilibrium Returns

The Black–Literman model begins with a neutral equilibrium portfolio for the prior estimate of returns. The model relies on General Equilibrium theory, namely, that “if the aggregate portfolio is at equilibrium, then each sub-portfolio must also be at equilibrium.” It may be used with any utility function, making it very flexible. In fact, most practitioners use the Quadratic Utility function and assume a risk-free asset, and thus the equilibrium model simplifies to the Capital Asset Pricing Model (CAPM). In fact, the neutral portfolio in this case is the CAPM Market portfolio.

Some workers have used other utility functions, and others consider other measures of portfolio risk without applying the same theoretical basis. In order to preserve the symmetry of the model, the practitioner should use the same utility function to identify both the neutral portfolio and the portfolio selection area. Here the approach uses the Quadratic Utility function, CAPM, and unconstrained mean-variance because it is a well-understood model. Given these assumptions, the prior distribution for the Black–Literman model is the estimated mean excess return from the CAPM market portfolio. The process of computing the CAPM equilibrium excess returns is straightforward. CAPM is based on the concept that there is a linear relationship between risk (as measured by standard deviation of returns) and return. Furthermore, it requires returns to be normally distributed. This model is of the form

$$E(r)=r_f+\beta r_m+\alpha \tag{3.80}$$

where

+   - $r_f$ is the risk-free rate,
+   - $r_m$ is the excess return of the market portfolio,
+   - $\beta$ is a regression coefficient computed as $\beta=\rho\left(\sigma_p/\sigma_m\right)$, and
+   - $\alpha$ is the residual or asset-specific excess return.

Under CAPM, any irregular risks associated with an asset is uncorrelated with that from other assets, and this issue may be reduced via diversification. And the investor may be rewarded for taking systematic risk measured by $\beta$, but is not compensated for taking irregular risks associated with $\alpha$.

Under CAPM, all investors should hold the same risky CAPM market portfolio. Since all investors hold risky assets only in the market portfolio, at