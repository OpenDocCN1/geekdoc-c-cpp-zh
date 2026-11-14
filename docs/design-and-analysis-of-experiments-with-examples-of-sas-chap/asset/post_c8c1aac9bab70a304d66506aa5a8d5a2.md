
trace plots can be used as a graphical tool to determine the important components similar to the way that the normal or half-normal plot of effects is used for screening experiments with independent factors. Cornell (2002) and Snee and Marquardt (1976) discuss other strategies for screening with mixture experiments.

The least squares fits performed by ADX for mixture experiments (illustrated in Figures 11.14 and 11.15) are designed specifically for fitting Scheffé models. Cornell (2002) explains that standard regression programs like SAS proc glm or SAS proc reg do not provide the correct analysis because when the no-constant option (model option /noint) is used, the fitted model sums of squares and total sums of squares are not corrected for the overall mean. Therefore, the $R^2$ value is inflated and gives the impression that the model fits better than it actually does. For example, Table 11.2 shows a comparison of the sums of squares and $R^2$ statistic produced by SAS ADX, proc glm, and proc reg when fitting the Scheffé quadratic model to the data in Table 11.1 and using the model /noint option with proc glm and proc reg.

Table 11.2 Comparison of Different Programs for Fitting Scheffé Quadratic Model to Data in Table 11.1

| Program | Model df | Model SS | Error SS | Total SS | $R^2$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| ADX Mixture | 5 | 275.64 | 2.41 | 278.05 | 0.9913 |
| proc glm | 6 | 36285.60 | 2.41 | 36288 | 0.9999 |
| proc reg | 6 | 36285.60 | 2.41 | 36288 | 0.9999 |

One way the correct sums of squares and $R^2$ can be computed using proc reg or proc glm is to fit the model

```
$y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_{12} x_1 x_2 + \beta_{13} x_1 x_3 + \beta_{23} x_2 x_3 + \epsilon$. (11.15)
```

By including an intercept and removing $x_3$ from the model, the coefficients $\beta_0$, $\beta_1$, and $\beta_2$ take on a different meaning than in the Scheffé model shown in Equation (11.6). $\beta_0$ takes on the value of $\beta_3$ in Equation (11.6), and $\beta_1$ represents the difference of $\beta_1 - \beta_3$. The code for fitting this model with proc glm and estimating $\beta_1$, $\beta_2$, and $\beta_3$ is shown in the listing on the next page.

```
data form;
   input x1 x2 x3 y;
   datalines;
1.0 0 0 48.7
.8 .1 .1 49.5
.6 .2 .2 50.2
.5 0 .5 52.8
.5 .5 0 49.3
.33333 .33333 .33333 51.1
.3 .2 .5 52.7
.3 .5 .2 50.3
.1 .8 .1 60.7
.1 .1 .8 47.9
0 0 1.0 64.9
0 .5 .5 53.5
0 1.0 0 50.6
proc glm data=form;
   model y = x1*x2 x1*x3 x2*x3/ solution;
   estimate 'beta1' intercept 1 x1 1;
   estimate 'beta2' intercept 1 x2 1;
   estimate 'beta3' intercept 1 x3 1;
   run;
```

When fitting the model 11.5 or 11.15 with proc reg, the mixture that produces the maximum or minimum response can be found numerically using proc nlp as shown in Section 10.7.4, but it is difficult to produce contour plots outside SAS ADX unless the transformation to orthogonal components is used, as described in the last section and illustrated in the appendix to this chapter.

## 11.5 Constrained Mixture Experiments

In some mixture experiments, it is impossible to test pure components. For example, fuel for solid rocket boosters is a mixture of binder, oxidizer, and fuel, and it must contain a percentage of each. Proportions can be varied but must remain within certain constraints in order for the propellant to work. Kurotori (1966) described an example of this situation where experiments with rocket propellant were performed. In this case, x1: the binder, had to be at least 20% of the mixture; x2: the oxidizer, could be no less than 40% of the mixture; and x3: the fuel, had to comprise at least 20% of the mixture. This leads to three new constraints shown in Equation (11.16), and the experimental region is restricted to the shaded subset of the simplex shown in Figure 11.19.

- x1 ≥ 0.20
- x2 ≥ 0.40
- x3 ≥ 0.20

(11.16)

When each mixture component only has a lower constraint as shown in Figure 11.19, the constrained region (if consistent) will always be a smaller simplex within the original simplex as shown in the figure. The component space within this smaller simplex can be conveniently transformed into a pseudo-component space where the same simplex lattice and simplex centroid designs can be used for an experimental design. If the lower constraint for mixture component \(x_i\) is defined to be \(l_i\), then the \(i\)th pseudo component is defined to be

```
\(x'_i = \frac{x_i - l_i}{1 - \sum_{k=1}^k l_i},\) (11.17)
```

where \(k\) is the number of mixture components. A simplex lattice design can be constructed in the pseudo-components and the actual mixtures to be tested can then be obtained by solving Equation (11.17) for \(x_i\) as

```
\(x_i = l_i + \left( 1 - \sum_{i=1}^k l_i \right) x'_i,\) (11.18)
```

For example, Table 11.3 shows an SLD(3,2) design in pseudo-components translated into a design with the actual components for the rocket propellant experiment using the lower bounds given in Equation (11.16). The experiments were run by making each mixture of fuel oxidizer or binder, then measuring the resulting elasticity. The general quadratic or special cubic model can be fit to either the pseudo or actual components.

### Figure 11.19 Constrained Region for Rocket Propellant Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_476_0.png)

### 11.5.1 Upper and Lower Constraints

In some special cases when there are only upper constraints or both upper and lower constraints, the constrained experimental region will result in a smaller inverted simplex within the simplex component space. However, in the more common situation, the constrained region will be an irregular hyperpolyhedron. In this case, McLean and Anderson (1966) recommend a design that consists of the extreme vertices (EVD) of the experimental region, possibly

Table 11.3 Simplex Lattice Design in Pseudo and Actual Components

| Run | $x_1$ | $x_2$ | $x_3$ | $x_1$=Fuel | $x_2$=Oxidizer | $x_3$=Binder | response elasticity |
|---|---|---|---|---|---|---|---|
| 1 | 1 | 0 | 0 | 0.400 | 0.400 | 0.200 | 2350 |
| 2 | 0 | 1 | 0 | 0.200 | 0.600 | 0.200 | 2450 |
| 3 | 0 | 0 | 1 | 0.200 | 0.400 | 0.400 | 2650 |
| 4 | 1/2 | 1/2 | 0 | 0.300 | 0.500 | 0.200 | 2400 |
| 5 | 1/2 | 0 | 1/2 | 0.300 | 0.400 | 0.300 | 2750 |
| 6 | 0 | 1/2 | 1/2 | 0.200 | 0.500 | 0.300 | 2950 |
| 7 | 1/3 | 1/3 | 1/3 | 0.266 | 0.466 | 0.266 | 3000 |

augmented by edge and facet centroids. They propose an algorithm for finding the extreme vertices by forming a two-level factorial in $k - 1$ mixture components (using the lower and upper constraints as levels), then setting the $k$th component equal to one minus the sum of the other $k - 1$ components. Each point in this factorial, where the computed value of the $k$th component falls within its lower and upper constraints, is an extreme vertex. All the extreme vertices can be found by repeating this procedure using all possible subsets of $k - 1$ mixture components for the two-level factorial.

Once the extreme vertices of the experimental region are found, the coordinates of the edge centroids can be found by first locating all vertices with a constant value for one component (i.e., two points on an edge) then averaging the other components. The centroids of two-dimensional facets can be found by first finding all vertices where two components are constant and then averaging the remaining $k - 2$ components, etc.

Snee and Marquardt (1974) defined the XVERT algorithm for finding the extreme vertices, which is similar to McLean and Anderson's algorithm. When there are many components in the mixture problem, there may be many more extreme vertices in the experimental region than there are coefficients in the Scheffe linear or quadratic model. In that case Snee and Marquardt (1974) recommended choosing an A-optimal subset of the extreme vertices that minimizes the trace of the $(X'X)^{-1}$ matrix.

There are SAS macros, included in the AUTOCALL library, that use either McLean and Anderson's algorithm or Snee and Marquardt's XVERT algorithm to generate the vertices of a multi-constrained experimental region. To
