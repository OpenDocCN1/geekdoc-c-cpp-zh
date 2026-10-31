
Idzorek (2005) presents a means to calibrate the confidence or variance of the investors' views in a simple and straightforward method.

Next is a section on measures of extremity or quality of views. Fusai and Meucci (2003) proposed a way to measure how consistent a posterior estimate of the mean is with regard to the prior, or some other estimate. Braga and Natale (2007) described how to use Tracking Error to measure the distance from the equilibrium to the posterior portfolio. Also included are additional original work on using relative entropy to measure quality of the views.

Finally, larger extensions to the model such as Krishnan and Mains (2006) present a method to incorporate additional factors into the model. Qian and Gorman (2001) presented a method to integrate views on the covariance matrix as well as views on the returns.

## Idzorek’s Extension

Idzorek’s apparent goal was to reduce the complexity of the Black–Litterman model for nonquantitative investors. He achieved this by allowing the investor to specify the investors’ confidence in the views as a percentage (0–100%) where the confidence measures the change in weight of the posterior from the prior estimate (0%) to the conditional estimate (100%). This linear relation is shown in Equation (3.123):

confidence = ( w − w_mkt ) / ( w_100 − w_mkt )  (3.123)

where
w_100 is the weight of the asset under 100% certainty in the view,
w_mkt is the weight of the asset under no views, and
w is the weight of the asset under the specified view.

Also provided was a method to back out the value of ω required to generate the proper tilt (change in weights from prior to posterior) for each view. These values may then be combined to form Ω, and the model is used to compute posterior estimates.

Idzorek includes τ in the formulas, but because of the use of the Alternative Reference Model and his formula (3.123), there is no need to use τ with the Idzorek method.

The paper discussed solving for ω using a least-squares method. One may actually solve this analytically. The next section will provide a derivation of the formulas required for this solution.

First one may use the following form of the uncertainty of the views. Idzorek includes τ in this formula, but he uses the Alternative Reference Model so that one may drop τ from the formulation of his method:

Ω = α P Σ P^T  (3.124)

where α, the coefficient of uncertainty, is a scalar quantity in the interval [0, ∞].

- When the investor is 100% confident in their views, then α will be 0.
- When they are totally uncertain, then α will be ∞.

Note that (3.124) is exact, it is identical to Equation (3.122) and the Ω used by He and Litterman (1999) because it is a 1 × 1 matrix. This allows one to find a closed-form solution to the problem of Ω for Idzorek’s confidence.

First one substitutes (3.119)

$$\Pi = \Pi + [1/(1 + \alpha)][P^{-1}Q - \Pi] \tag{3.119}$$

into
$$\underline{\Pi} = \delta\Sigma \underline{w}, \tag{3.83}$$

or
$$\underline{w} = \Pi(\delta\Sigma)^{-1}$$

yielding
$$\underline{w} = \{\Pi + [1/(1 + \alpha)][P^{-1}Q - \Pi]\}(\delta\Sigma)^{-1} \tag{3.125}$$

Now one may solve (3.125) at the boundary conditions for α:
$$\lim_{\alpha\to\infty} w_{mkt} = \Pi(\delta\Sigma)^{-1} \tag{3.126}$$
$$\lim_{\alpha\to0} w_{100} = P^{-1}Q(\delta\Sigma)^{-1} \tag{3.127}$$

Plug them back into (3.123). When the investors apply all their views at once, the interaction among the views may pull the posterior estimate for individual assets away from the results generated when the views were taken one at a time.

Idzorek's method greatly simplified the investor's process of specifying the uncertainty in the views when the investor does not have a quantitative model driving the process. In addition, this model does not add meaningful complexity to the process.

## An Example of Idzorek's Extension

Idzorek described the steps required to implement his extension in his paper, but did not provide a complete worked example. Here, one will work through the example from where Idzorek left off! Idzorek's example includes three views:

- International Development Equity will have absolute excess return of 5.25%, Confidence 25.0%.
- International Bonds will outperform U.S. bonds by 25 bps, Confidence 50.0%.
- U.S. Growth Equity will outperform U.S. Value Equity by 2%, Confidence 65.0%.

Idzorek defined the steps that include calculations of w100 and then the calculation of ω for each view given the desired change in the weights. From the previous section, one noted that one only need to take the investor's confidence for each view, plug it into (3.131), and calculate the value of alpha. Then one plugs α, P, and Σ into Equation (3.124) and compute the value of ω for each view. At this point, one may assemble the Ω matrix and proceed to solve for the posterior returns using (3.104) or (3.105).

In presenting this example, the results for each view will be shown including w_mkt and w_100 in order to make the working of the extension more transparent. Tables 3.8–3.10 show the results for a single view.

Then one may use the freshly computed values for the Ω matrix with all views specified together and arrive at the final result shown in Table 3.11 blending all three views together.

**Table 3.8 Calibrated results for View 1.**

| Asset | ω | w_mkt | w* | w 100% | Implied confidence |
|---|---|---|---|---|---|
| Intl Dev Equity | 0.002126625 | 24.18% | 25.46% | 29.28% | 25.00% |

**Table 3.9 Calibrated results for View 2.**

| Asset | ω | w_mkt | w* | w 100% | Implied confidence |
|---|---|---|---|---|---|
| US Bonds | 0.000140650 | 19.34% | 29.06% | 38.78% | 50.00% |
| Intl Bonds | 0.000140650 | 26.13% | 16.41% | 6.69% | 50.00% |

not contradict the prior estimates. Theil (1971) described a method of performing a hypothesis test to verify that the views are compatible with the prior. That work is being extended to measure compatibility of the posterior and the prior. Fusai and Meucci (2003) described a method for testing the compatibility of the posterior and prior when using the alternative reference model. He and Litterman (1999) and Braga and Natale (2007) described measures that may be used to measure the distance between two distributions, or the amount of tilt between the prior and the posterior. These measures did not lend themselves to hypothesis testing, but they may be used as constraints on the optimization process. He and Litterman (1999) define a metric, Λ, which measured the tilt induced in the posterior by each view. Braga and Natale (2007) used Tracking Error Volatility (TEV) to measure the distance from the prior to the posterior.

## Theil’s Measure of Compatibility Between the Views and the Prior

Theil (1971) described this as testing the compatibility of the views with the prior information. Given the linear mixed estimation model, one has the prior (3.132) and the conditional (3.133):

xβ = π + u
(3.132)

pβ = q + v
(3.133)

The mixed estimation model defines u as a random vector with mean 0 and covariance Σ_u, and v as a random vector with mean 0 and covariance Ω.

The approach being taken here is very similar to the approach taken when analyzing a prediction from a linear regression. One has two estimates of the views, the conditional estimate of the view and the posterior estimate of the returns.

One may define the posterior estimate as β_. One may measure the estimation error between the prior and the views as

ζ = (xβ_ - μ) = x(β_ - β) + u
(3.134)

The vector ζ has mean 0 and variance V(ζ). One shall form one’s own hypothesis test using the formulation

ξ = E(ζ) V(ζ)^{-1} E(ζ)
(3.135)

The quantity ξ is known as the Mahalanobis distance (multidimensional analog of the z-score) and is distributed as χ²(n). In order to use this form, one needs to solve for the E(ζ) and V(ζ).

If one considers only the information in the views, the estimator of β is

β_ = (P^T Ω^{-1} P)^{-1} P^T Ω^{-1} Q
(3.136)

Note that since P is not required to be a matrix of full rank, one might not be able to evaluate this formula as written. One works in return space here (as
