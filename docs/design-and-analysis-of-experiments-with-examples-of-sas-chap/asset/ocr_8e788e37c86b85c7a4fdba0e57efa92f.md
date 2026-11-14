designs for experiments with mixtures. These designs consist of all possible combinations of proportions, where the ith proportion takes on the values \(x_i = 0, \frac{1}{m}, \frac{2}{m}, ... 1\). A simplex-lattice design (SLD) in k components with m+1 equally spaced proportions for each component is designated as a simplex-lattice(k,m) or SLD(k,m) design.

Figure 11.6 shows the linear (SLD(3,1)) and the quadratic (SLD(3,2)) designs in three components. Only the pure components (i.e., \((x_1, x_2, x_3) = (1, 0, 0)\), \((x_1, x_2, x_3) = (0, 1, 0)\), and \((x_1, x_2, x_3) = (0, 0, 1)\)) are required for a linear design and the coefficient \(\beta_1\) in model 11.4 can be estimated as average of all the response data at the pure component where \(x_i = 1.0\). In the linear model, the effect of blending two or more components is assumed to be linear, and no intermediate points are necessary in the design. The 50/50 mixtures of each pair of components are required to estimate the coefficients \(\beta_{ij}\) of the quadratic blending effects in model 11.5, thus the mixtures \((x_1, x_2, x_3) = (\frac{1}{2}, \frac{1}{2}, 0)\), \((x_1, x_2, x_3) = (\frac{1}{2}, 0, \frac{1}{2})\), and \((x_1, x_2, x_3) = (0, \frac{1}{2}, \frac{1}{2})\) are required in addition to the pure components for a quadratic design.

# Figure 11.6 Linear and Quadratic Simplex Lattice Designs

![](bbox=[0.2, 0.41, 0.8, 0.6])

In response surface experiments conducted with independent factors, as discussed in Chapter 10, the experimental region can be restricted so that the general quadratic model is usually a good approximation to the true nonlinear model relating the response to the factor levels in the restricted region. In a mixture experiment, the experimental region consists of the full (k - 1) dimensional simplex or tetrahedron and cannot be restricted. Therefore, higher order polynomial equations are sometimes necessary to approximate the true model over the entire simplex. A full cubic model in three-mixture components is shown in Equation (11.8).

```
y = \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3
\beta_{12} x_1 x_2 + \beta_{13} x_1 x_3 + \beta_{23} x_2 x_3
\delta_{12} x_1 x_2 (x_1 - x_2) + \delta_{13} x_1 x_3 (x_1 - x_3) + \delta_{23} x_2 x_3 (x_2 - x_3)
\beta_{123} x_1 x_2 x_3
(11.8)
```