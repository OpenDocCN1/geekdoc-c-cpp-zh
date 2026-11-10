Thus, the evaluation of the problem functions is essentially a “black box” operation as far as the ES is concerned. Obviously, in the interests of overall computational efficiency, the problem function evaluations should be performed efficiently. As long as there are no equality constraints and the feasible space is not disjoint, then infeasible solutions can simply be “rejected.” In an ES this means ensuring that those particular solutions are not selected as parents in the next generation.

If these conditions on the constraints are not met, then a penalty function method should be used. A suitable form for an ES is:

$$f_A(x) = f(x) + M^k w^T c_V(x)    (11.26)$$

where w is a vector of nonnegative weighting coefficients, the vector c_V quantifies the magnitudes of any constraint violations, M is the number of the current generation, and k is a suitable exponent. The dependence of the penalty on generation number biases the search increasingly heavily toward feasible space as it progresses.

# ### 11.9.5 Convergence Criteria

Two standard convergence tests are used to terminate ES searches. One is that the absolute difference in the objective function values of the best and worst members of the post-selection population is less than a user-specified limit, i.e.,

$$f_w - f_b ≤ ω_c    (11.27)$$

The other is that the relative difference in the objective function values of the best and worst members of the post-selection population is less than a user-specified limit, i.e.,

$$f_w - f_b ≤ (ε_d / μ) | ∑_{i=1}^{μ} f_i |    (11.28)$$

Thus, absolutely or relatively, the objective function values of the parents must lie close together before the algorithm is deemed to have converged.

# ### 11.9.6 Computational Considerations

The procedures controlling the generation of new solutions are so simple that the computational cost of implementing an ES is usually dominated by that associated with the evaluation of the problem functions.