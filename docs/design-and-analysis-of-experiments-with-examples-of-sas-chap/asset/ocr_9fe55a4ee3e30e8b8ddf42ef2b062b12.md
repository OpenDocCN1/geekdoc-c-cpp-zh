# 11.7.1 Models for Mixture Experiments With Process Variables

The model for a mixture experiment with process variables results from crossing the model for the mixture components and the model for the process variables. For fixed levels of the process variables, the model for the mixture components is

\(\eta_x = f(x), \quad (11.22)\)

and the model for the process variables is

\(\eta_z = g(z), \quad (11.23)\)

where \(f(x)\) is the Scheffé linear, quadratic, or cubic mixture model, and \(g(z)\) is the linear or general quadratic model for independent factors. The combined model is then found as the cross-product \(\eta_{xz} = (f(x)) \times (g(z))\). For example, assuming a quadratic mixture model for the coating experiment where there were three mixture components and one two-level process variable,

\(f(x) = \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_{12} x_1 x_2 + \beta_{13} x_1 x_3 + \beta_{23} x_2 x_3,\)

and

\(g(z) = \alpha_0 + \alpha_1 z.\)

The combined model is

\(\eta_{xz} = \beta_1(z)x_1 + \beta_2(z)x_2 + \beta_3(z)x_3 + \beta_{12}(z)x_1 x_2 + \beta_{13}(z)x_1 x_3 + \beta_{23}(z)x_2 x_3, \quad (11.24)\)

where \(\beta_i(z) = \beta_i \times (\alpha_0 + \alpha_1 z).\)

Multiplying the terms we can write this model as:

\(\eta_{xz} = \gamma_0^0 x_1 + \gamma_2^0 x_2 + \gamma_3^0 x_3 + \gamma_{12}^0 x_1 x_2 + \gamma_{13}^0(z)x_1 x_3 + \gamma_{23}^0(z)x_2 x_3 + \gamma_1^1 x_1 z + \gamma_2^1 x_2 z + \gamma_3^1 x_3 z + \gamma_{12}^1 x_1 x_2 z + \gamma_{13}^1 x_1 x_3 z + \gamma_{23}^1 x_2 x_3 z, \quad (11.25)\)

where \(\gamma_i^0 = \beta_i \times \alpha_0\) and \(\gamma_i^1 = \beta_i \times \alpha_1\).

In this model, the first six terms represent the linear and quadratic blending of the mixture components since these terms involve only the mixture components. The last six terms in the model represent the changes in the linear and quadratic blending effects caused by changes in the process variable.

If the process variable has a constant effect on the response, which would cause the same change in all blends of the mixture components, there is no term in model 11.25 that can represent the constant effect of the process variable. Gorman and Cornell (1982) have suggested an alternate form of the model substituting \((1 - x_2 - x_3)\) for \(x_1\) in the term \(\gamma_1^1 x_1 z\), resulting in the model