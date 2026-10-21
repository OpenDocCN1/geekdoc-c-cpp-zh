
![](img/c92a9d81ba7f671c83a4c600d27389fb_215_0.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_215_1.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_215_2.png)

FIGURE 15. Errors in the Craig-Sulem calculation of the Neumann data for a pair of traveling Stokes waves with parameters (3.38) and fluid depth h = 0.05.

rapidly for n ≥ 90 while it remains flat for n < 90 in Figure 16. Recall that a third method (the BIM method) was used for the exact solution in both plots.

The second and third panels of Figure 16 were used to decide how many grid points to use in the TFE method. We used M = 2048, N = 32 in double-precision and M = 4096, N = 48 in quadruple-precision. These plots show the partial norms

(3.40) κ_{nj} = √∑_k |α_j^n(k)|², γ_{nk} = √∑_j |α_j^n(k)|²,

where α_j^n(k) are the Chebyshev coefficients of the k-th Fourier mode of u_n:

û_n(k,y) = ∑_{j=0}^N α_j^n(k) T_j(1 + 2h^{-1} y), (|k| ≤ M/2, −h < y < 0).

It is worth noting that many fewer grid points are needed in the y-direction than in the x-direction, so the price of discretizing the bulk fluid is not as severe as one might imagine. Moreover, as with the BIM method, intermediate calculations can be done in double or quadruple-precision arithmetic to achieve similar levels of accuracy in the solution. The overall running times (in seconds) of the various methods on this example are given in the following table:

| method | BIM(d) | BIM(q) | TFE(d) | TFE(q) | CS | AFM | AFM-QR |
|---|---|---|---|---|---|---|---|
| time | 0.156 | 3.53 | 2.46 | 24.0 | 2762 | 11222 | 920 |

The code was run on a 3.33 GHz Intel Xeon X5680 system with 12 cores. Here (d) and (q) stand for double and quadruple-precision, and the other methods were run with 360 bits (108 digits) of precision. The running time of AFM* is nearly identical to that of AFM, and the AFM-QR variant will be described below. Clearly, the BIM and TFE approaches are superior to the CS and AFM-based methods since arbitrary-precision arithmetic is not required.

We conclude with the results of the AFM and AFM* methods on this example, which we selected initially as being relevant to water waves and likely to cause difficulties for the AFM and AFM* methods. Our reasoning was that the second wave is large enough to require many Fourier modes to resolve its shape, but small enough that cosh(kη(x)) is many orders of magnitude larger at the crest of the first wave than at the crest of the second (for large k). Thus, substantial cancellation must occur near x = 0 in order to resolve the behavior of φ near x = π. However, the singular values in the first panel of Figure 17 decay slowly in comparison to the infinite-depth standing wave case of Figure 13. This is because the waves in these two examples have similar Fourier decay rates for η̂_k and Ĝ_k, but the deep-water standing wave has a much larger vertical crest-to-trough height. To the extent that this is generally the case for waves in deep versus shallow water, the AFM and AFM* methods appear to be better suited for finite depth problems.

The errors in the AFM and AFM* methods are nearly identical for every choice of pseudo-inverse cutoff in the second panel of Figure 17. Thus, the methods are equally effective at computing the DNO for this example. Beyond k_cutoff = 970, the error in the second panel reaches a plateau of 3 × 10^−28. This is due to errors in the “exact” solution. Since this plateau is reached already at k_cutoff = 970, it would appear that K and possibly M can be reduced while still achieving the target accuracy of 10^−28. However, reducing K leads to worse results (not shown). The reason is that the high-index columns of A in

A_{j0} = 1/\sqrt{M},   (A_{j,2k-1}, A_{j,2k}) = \sqrt{2/M} \cosh(k(\eta(x_j)+h))/\cosh(k(\eta_{\max}+h)) (\cos kx, \sin kx),   (1 ≤ k < K/2)

comprise a small but important part of the low-index singular vectors U of the singular value decomposition, A = U S V^T. A better way to understand how large K needs to be in order to achieve a prescribed accuracy is to perform a QR factorization, A = Q R, which is a numerically robust way to perform a Gram-Schmidt orthogonalization of the columns of A. We then define the “discrete AFM transform”

𝒩̃_0 = c_0,   𝒩̃_k = c_{2k-1} + i c_{2k},   {c_k}_{k=0}^{K-2} = 1/\sqrt{M} Q^T {𝒩(x_j)}_{j=0}^{M-1}

![](img/c92a9d81ba7f671c83a4c600d27389fb_218_0.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_218_1.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_218_2.png)

FIGURE 17. AFM and AFM* calculation of the Neumann data for the superposition of Stokes waves in Figure 14. These AFM methods are much better conditioned in this shallow water regime than the deep water cases considered above. The optimal cutoff modes at right were k_cutoff = 2046 (AFM) and 2045 (AFM*).

and, in Figure 18, compare it to the discrete Fourier transform

\hat{\mathscr{N}}_k = 1/M \sum_{j=0}^{M-1} \mathscr{N}(x_j) e^{-2\pi i j k},      0 ≤ k ≤ M/2.

Standing wave

Superposition of traveling waves

![](img/c92a9d81ba7f671c83a4c600d27389fb_219_0.png)

FIGURE 18. Comparison of the coefficients in an expansion of the Dirichlet and Neumann data in an orthogonalized AFM basis versus a Fourier basis.

The red curves give the Fourier modes of the input Dirichlet data, which are taken to specify the problem with infinite precision even though they only describe the standing wave and traveling waves to around 25 and 30 digits, respectively. The black curves give the Fourier modes of the boundary integral solutions, which were computed with 212 and 106 bits of precision, respectively. The orange and blue curves give the “AFM transform” of the Dirichlet and Neumann data. The observation that K cannot be reduced significantly below 2048 for the traveling wave problem is seen clearly in the right panel, which shows that \hat{\mathscr{N}}_k does not reach roundoff error until just below k = 1024.

The fact that the AFM coefficients \tilde{\mathscr{D}}_k and \tilde{\mathscr{N}}_k decay faster than the Fourier coefficients \hat{\mathscr{D}}_k and \hat{\mathscr{N}}_k suggests that the Gram-Schmidt version of the AFM basis is more efficient at representing the Dirichlet and Neumann data of many problems of physical interest (such as standing and traveling waves) than the Fourier basis. The abrupt change in slope of the orange and blue curves in the left panel occurs when the AFM method begins to resolve errors in the given Dirichlet data, which is taken to be exact even though it only agrees with physical standing waves to 25 digits. While it is interesting that the Gram-Schmidt version of the AFM basis is more efficient than a Fourier basis for these problems, computing the orthogonal AFM basis is expensive since it requires a great deal of additional precision to avoid losing all significant digits during the QR factorization process.

## Conclusions

We have shown that the Craig-Sulem expansion of the DNO operator, the implicit formulation due to Ablowitz, Fokas and Musslimani, and its dual, due to Ablowitz and Haut, can all be used to compute spectrally accurate solutions of the Dirichlet-Neumann problem. All three methods involve ill-conditioned intermediate calculations when the vertical crest-to-trough distance becomes large relative to the inverse of the highest-frequency wave numbers involved in a Fourier description of the wave profile η(x) and the Dirichlet data \mathscr{D}(x). However, this ill-conditioning can be tamed using extended precision arithmetic. Most importantly, η(x) and \mathscr{D}(x) need only be specified in double-precision to obtain double-precision results for \mathscr{N}(x); extended precision is only required in intermediate calculations. While it is undesirable to work in extended precision arithmetic, a spectrally accurate method requiring 64 digits of accuracy in intermediate calculations may require less work than a more traditional 16-digit calculation using a 2nd or 4th order method if high accuracy is desired.

Nevertheless, our goal in writing the paper was not to advocate the use of these methods, but to explore their limits of applicability. We originally thought that the AFM and AFM* would break down if the potential φ cannot be extended analytically to a strip containing the peak of the wave profile. This was the motivation for studying a potential φ with poles on the real axis and a wave profile that dips below the poles but also extends above them. It is surprising that the AFM basis can still be used to approximate 𝒟 in this case to arbitrary accuracy, and that the term-by-term Neumann data turns out to be a good approximation of the correct solution. We also did not expect the CS expansion to converge for realistic large-amplitude standing waves, but it was able to achieve 25 digits of accuracy at 150th order. For the same problem, the AFM and AFM* methods achieved 25 digits of accuracy in spite of singular values dropping below 10⁻¹⁰⁰. For waves in shallow water, the condition numbers are much more reasonable, making the AFM methods more appealing.

As noted in [23], the CS expansion suffers from significant cancellation requirements. Our numerical investigations confirm this behavior. We note that a suitable rearrangement of the series permits one to account for some of these cancellations, though not all. One of the goals of the present work was to understand whether this behavior is present in the AFM formulation and to what extent as the AFM method may be interpreted as a certain summation of the CS expansion [2]. Our investigations reveal the AFM method is similarly ill-conditioned. Indeed the rapid decay of singular values in the AFM (and AFM*) method mirrors the cancellation properties observed in the CS expansion. Given the delicate nature of CS, AFM and AFM* we recommend the BIM, especially for two-dimensional flows. The TFE version of the CS expansion also performs remarkably well without the need for extended precision arithmetic in intermediate calculations.

Regarding extension to three dimensions, the CS and TFE expansions work with little change. Since the latter can be run effectively in double-precision, it is a viable method. Although the bulk fluid must be discretized, the system of equations that must be solved decouples into many one-dimensional boundary value problems rather than a large system of equations such as arise in finite element methods. The AFM and AFM* methods will lead to large, highly ill-conditioned linear systems that are easy to set up but nearly impossible to solve. Performing the SVD or QR factorization of such a large matrix in extended precision arithmetic would be extremely costly, and iterative methods such as GMRES will not converge when the condition number grows to 10¹⁵ or higher. By contrast, the boundary integral method yields condition numbers close to 1; hence, GMRES converges in just a few iterations. Although it is difficult to implement boundary integral methods in three dimensions due to the slowly decaying lattice sums involved, techniques such as Ewald summation [3,13,18] are available to accelerate convergence.

## Acknowledgments

The author was supported in part by the Director, Office of Science, Computational and Technology Research, U.S. Department of Energy under Contract No. DE-AC02-05CH11231, and by the National Science Foundation through grant
