
evaluation of the covariance matrix of the estimates), so his corrections (8.48) would come as an additional benefit at almost no extra cost.

### Karimäki’s assumption revisited.
Karimäki designed his fit under a seemingly restrictive assumption, $|d| \ll R$, but in fact his fit works well under a less restrictive condition:

$$ 1 + \rho d \text{ should not be close to } 0. \quad (8.49) $$

Indeed, let us expand the objective function (8.35) into Taylor series

$$ \mathscr{F}(\Theta) = a_1 + \mathbf{D}_1^T (\Theta - \hat{\Theta}) + \frac{1}{2} (\Theta - \hat{\Theta})^T \mathbf{H}_1 (\Theta - \hat{\Theta}) + \dots \quad (8.50) $$

where higher order terms are omitted; here $\Theta$ denotes the vector of parameters, $\mathbf{D}_1$ is the gradient and $\mathbf{H}_1$ the Hessian of $\mathscr{F}$. Suppose that the expansion is made at the point $\hat{\Theta}$ where (8.35) takes its minimum, then $\mathbf{D}_1 = \mathbf{0}$. Note that $\hat{\Theta}$ is in fact Pratt’s estimate of the circle parameters (see Section 5.5).

Karimäki’s objective function (8.36) can be written as $\mathscr{F}_{\mathrm{Kar}} = g \mathscr{F}$, where $g = (1 + \rho d)^{-2}$. Let us expand the extra factor $g$ into Taylor series, too:

$$ g(\Theta) = a_2 + \mathbf{D}_2^T (\Theta - \hat{\Theta}) + \frac{1}{2} (\Theta - \hat{\Theta})^T \mathbf{H}_2 (\Theta - \hat{\Theta}) + \dots $$

Multiplying the above expansions gives Karimäki’s objective function (8.36):

$$ \mathscr{F}_{\mathrm{Kar}}(\Theta) = a_1 a_2 + a_1 \mathbf{D}_2^T (\Theta - \hat{\Theta}) + \frac{1}{2} (\Theta - \hat{\Theta})^T (a_1 \mathbf{H}_2 + a_2 \mathbf{H}_1) (\Theta - \hat{\Theta}) + \dots $$

The minimum of $\mathscr{F}_{\mathrm{Kar}}$ is taken at

$$ \hat{\Theta}_{\mathrm{Kar}} = \hat{\Theta} - a_1 (a_1 \mathbf{H}_2 + a_2 \mathbf{H}_1)^{-1} \mathbf{D}_2 + \dots $$

where higher order terms are omitted. Let us examine how the minimum $\hat{\Theta}_{\mathrm{Kar}}$ differs from the minimum $\hat{\Theta}$ of the function $\mathscr{F}$ given by (8.50).

As usual, suppose the noise is Gaussian at a level $\sigma \ll R$; then the observed points are at distance $\mathcal{O}(\sigma)$ from the best fitting circle. Then $\mathscr{F} = \mathcal{O}(\sigma^2)$ at its minimum, hence $a_1 = \mathcal{O}(\sigma^2)$. Now the difference between the two minima $\hat{\Theta}_{\mathrm{Kar}}$ and $\hat{\Theta}$ will be of order $\sigma^2$ provided the vector $(a_1 \mathbf{H}_2 + a_2 \mathbf{H}_1)^{-1} \mathbf{D}_2$ is not too large, i.e., if its magnitude is of order one. This vector depends on several factors which are hard to trace completely, but it appears that indeed its magnitude is of order one provided $g(\hat{\Theta}) = a_2$ is not too large, i.e., $1 + \rho d$ is not too close to zero, i.e., we arrive at the mild condition (8.49).

Recall that the statistical error of the estimate $\hat{\Theta}$ (i.e., its standard deviation) is of order $\sigma$, hence an additional error of order $\sigma^2$ would be indeed relatively small. In particular, both fits will have the same covariance matrix, to the leading order. We have seen in Chapter 7 that indeed all the algebraic circle fits have the same covariance matrix. Moreover, the corrections (8.48) may reduce it further, perhaps down to $\mathcal{O}(\sigma^3)$. This is, of course, a conjecture to be verified. If this is true, i.e., if $\hat{\mathcal{F}}_{Kar} - \hat{\mathcal{E}} = \mathcal{O}(\sigma^3)$, then Karimäki's estimator $\hat{\mathcal{F}}_{Kar}$ would not only have the same covariance matrix as other algebraic fits (Chapter 7), but also the same essential bias as the Pratt fit.

Our numerical tests support this hypothesis. We observed that the mean squared error of the Karimäki fit is usually larger than that of the Pratt fit, but after the corrections (8.48) are applied, the mean squared error becomes nearly equal to that of the Pratt fit.

We recall that the Pratt fit is one of the best circle fits, though its statistical accuracy is slightly lower than that of the Taubin fit or the geometric fit or the "Hyperaccurate" fit (see a detailed analysis in Chapter 7).

### Possible extensions.
There are several ways to relax even the mild restriction (8.49). They are not discussed in Karimäki's papers [106, 107], but we include them here in an attempt to extend the applicability of his fit.

First, if all the observed points are close to the circle (i.e., $\sigma \ll R$), one can choose any of them as the origin. In other words, one can choose $1 \leq j \leq n$ and then transform $(x_i, y_i) \mapsto (x_i - x_j, y_i - y_j)$ for all $i = 1, \ldots, n$. This places the origin at the $j$th observed point. In most cases such a shift would guarantee the validity Karimäki's main assumption (8.49). Furthermore, such a choice of the coordinate system does not reduce the size of the sample, as it did in the case of inversion-based fits, see Section 8.5. Even the $j$th point itself, where the origin is placed, effectively participates in the fitting procedure.

Next, one can apply an iterative scheme analogous to that of Rusu, Tico, Kuosmanen, and Delp [159]; see Section 8.6. Namely, one can adjust the origin (pole) $P = (0,0)$ at every iteration. Precisely, suppose for the current origin $P_k$ (where $k$ is the iteration number) the Karimäki fit returns a circle $\mathcal{C}_k$. Then one can set the next origin (pole) $P_{k+1}$ at the point on $\mathcal{C}_k$ closest to $P_k$; then one refits the circle $\mathcal{C}_{k+1}$, etc.

This iterative scheme may converge much faster than the RTKD algorithm of Section 8.6, because Karimäki's circle is more flexible, so it is not rigidly constrained to pass through the current pole. On the other hand, repeating the Karimäki fit iteratively would instantly deprive it of its best asset—fast performance—because its computational time would double or triple.

### A real data example.
We have tested the Karimäki circle fits on the real data example described in Section 5.12. As a pole, we used the first data point in the set.

The original Karimäki fit (Section 8.8) returned a circle with
center $=$ $(7.4408, 22.6155)$, radius $=$ $13.7401$,
so it underestimates the radius. The corrected version described in this section returned a circle with
center $=$ $(7.3909, 22.6636)$, radius $=$ $13.8092$,
which is closer to the ideal circle (5.71) but still slightly worse than circles found by simpler and faster algebraic fits (Section 5.12).

## 8.10 Numerical tests and conclusions

We have tested all the algorithms described in this chapter in a set of numerical experiments with simulated data. Our goal was to “try them on” under various conditions and compare them to the geometric and algebraic circle fits described in the previous chapters.

### Numerical tests.
First, we generated $N = 10^7$ random samples of $n = 20$ points located (equally spaced) on the entire circle $x^2 + y^2 = 1$ and corrupted by Gaussian noise at level $\sigma = 0.05$. For each circle fit we have empirically determined the mean squared error of the parameter vector, i.e.,

$$ \text{MSE} = \frac{1}{N} \sum_{i=1}^{N} [ (\hat{a}_i - a)^2 + (\hat{b}_i - b)^2 + (\hat{R}_i - R)^2 ], $$

where $\hat{a}_i, \hat{b}_i, \hat{R}_i$ denote the estimates of the circle parameters computed from the $i$th sample, and $a = b = 0, R = 1$ are their true values. The resulting MSE's are given in the first column of Table 8.1.

We note that the inversion-based fit and Karimäki fit require a pole (i.e., a point presumably lying on the circle) to be supplied. We did not give them such a luxury as a point on the true circle, but we used a randomly selected data point as a pole (which is a standard strategy; see Section 8.5).

The first column of Table 8.1 shows that the exotic circle fits described in this chapter are generally less accurate than the standard geometric and algebraic fits. The plain RTKD inversion-based fit (the second line) is especially poor; apparently, it heavily depends on the choice of the pole, and a randomly selected data point is just not good enough. The subsequent iterations improve the performance of the inversion-based fit, making it similar to that of the Pratt fit.

The plain Karimäki fit is not very accurate either, but after the subsequent corrective step it performs similarly to the Pratt fit. This fact confirms our theoretical predictions that the iterative RTKD fit and the corrected Karimäki fit would produce nothing but good approximations to the Pratt fit.

The SWFL Riemann fit was implemented with data centering and rescaling, as described in Section 8.4, to enforce its invariance under translations and similarities. These steps were added to the original version published in [175, 173], as without such steps the performance of the Riemann fit was unreliable. Surprisingly, with these additional steps, the Riemann fit becomes very stable, it even slightly outperforms the Pratt fit! But the best fitting schemes are still our “old friends”—Taubin, Hyper, and geometric fits.

Next we simulated more a difficult situation, where the $n = 20$ data points
