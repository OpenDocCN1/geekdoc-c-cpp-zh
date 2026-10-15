![](bbox=[0.35, 0.07, 0.62, 0.36])

Figure 11.14: Convergence to sum of deviations to 7.37 × 10⁻⁷ giving I = 0.005526 for Example 6

These values of the weighting factors differ somewhat from those obtained by Mekarapiruk and Luus [22], showing that the weighting factors are not unique, and are not related directly to the sensitivities, as the shifting terms are in the quadratic penalty function.

As is shown by Mekarapiruk and Luus [22], the performance index can be reduced slightly to I = 0.005264 by increasing the number of time stages to 20.

# 11.2.4 Remarks on the choice of penalty functions

Luus et al. [17] found no clear computational advantage of the absolute penalty function over the quadratic penalty function with shifting terms in solving the two-stage CSTR problem considered earlier as Example 5. Therefore, more research in this area is needed before choosing one over the other. The use of the quadratic penalty function with shifting terms has the advantage of yielding sensitivity factors that are related to the adjoint variables when Pontryagin’s maximum principle is used. This information is useful and it also provides an indication whether convergence to the optimum has been achieved. It is clear that there must be an upper limit to the number of final state equality constraints that can be considered conveniently in this fashion with the use of penalty functions. Fortunately many real problems involve only a small number of final state constraints; so, the methods used here provide reliable means for dealing with such constraints.