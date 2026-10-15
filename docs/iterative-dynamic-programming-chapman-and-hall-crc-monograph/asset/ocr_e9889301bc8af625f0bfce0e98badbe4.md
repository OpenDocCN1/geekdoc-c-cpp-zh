![](bbox=[0.34, 0.07, 0.64, 0.38])

Figure 2.10: Convergence profile from initial values $k_i = 0.05, i = 1,2,\cdots,5$ to $I = 4.5777 \times 10^{-4}$ for Example 2

where these equality constraints are “difficult” in the sense that they can not be used to solve for some particular variable.

Although a two-pass method to deal with equality constraints [13] was effective to solve optimization problems involving recycle streams [15], the general approach for handling equality constraints with the LJ optimization procedure was not solved satisfactorily, until quite recently when Hartig et al. [5] showed that penalty functions can be used very effectively in direct search optimization. The work was extended by Luus and Wyrwicz [34], who investigated the use of different types of penalty functions for steady state optimization problems. This work was extended further by Luus [20], who showed that shifting terms inside a penalty function can lead to very accurate values of the optimum. Now it appears that the use of a quadratic penalty function incorporating a shifting term is the best way of dealing with difficult equality constraints [20]. We consider the augmented performance index

$$J = I + \theta \sum_{i=1}^{m} (h_i - s_i)^2 \tag{2.84}$$

where a shifting term $s_i$ is introduced for each equality constraint. To solve this optimization problem, the LJ optimization procedure is used in a multi-pass fashion, where, at the beginning of each pass consisting of a number of iterations, the region sizes are restored to a fraction of the sizes used at the beginning of the previous pass. The shifting terms $s_i$ are updated after every pass simply by adjusting the values at the beginning of pass $(q + 1)$ based on the deviation of the left hand side in Eq. (2.83)