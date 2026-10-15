equality constraints was less than 10⁻¹⁰. The total computation time for the run was 0.38 s on a Pentium/120, showing a computation time of about 0.005 s per successful solution.

![](bbox=[0.27, 0.16, 0.7, 0.53])

Figure 1.7: Convergence profile to Solution 1 for Example 6, showing the effect of starting conditions

The convergence profile from three different starting conditions is given in Figure 1.7, where no difficulties were encountered and convergence to Solution 1 was readily obtained. Since the convergence is so rapid, it is natural to take numerous starting points chosen at random over some allowable range, to capture all the possible solutions. The constraints restricting calculations for only meaningful solutions not only reduce the computational effort, but ensure stability during calculations.

Now that the personal computers are very fast, the computation time is negligible for all of these 6 examples that have been outlined here. Of greater concern is the robustness of the method. One of the greatest advantages of separating the set of algebraic equations into two groups is that starting conditions must be specified only for the set of difficult equalities. Also, by minimizing the number of equations included in that set, we minimize the computational effort. Although for these 6 problems outlined here, the computational effort is negligible, if a situation arises