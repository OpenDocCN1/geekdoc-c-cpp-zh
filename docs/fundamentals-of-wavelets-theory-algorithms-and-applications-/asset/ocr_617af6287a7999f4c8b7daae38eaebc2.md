# 10.5 SPARSITY AND ERROR CONSIDERATIONS

The study of the effects of thresholding the matrix elements on the sparsity and error in the solution is the objective of this subsection. By *thresholding*, we mean setting those elements of the matrix to zero that are smaller (in magnitude) than some positive number \(\delta(0 \le \delta < 1)\), called the *threshold parameter*, times the largest element of the matrix.

Let \(A_{max}\) and \(A_{min}\) be the largest and the smallest elements of the matrix in (10.23). For a fixed value of the threshold parameter \(\delta\), define percent relative error (\(\varepsilon_\delta\)) as
\(\varepsilon_\delta := \frac{\|f_0 - f_\delta\|_2}{\|f_0\|_2} \times 100,\)
(10.62)

and percent sparsity (\(S_\delta\)) as
\(S_\delta := \frac{N_0 - N_\delta}{N_0} \times 100.\)
(10.63)

In the above, \(f_\delta\) represents the solution obtained from (10.23) when the elements whose magnitudes are smaller than \(\delta A_{max}\) have been set to zero. Similarly, \(N_\delta\) is the total number of elements left after thresholding. Clearly, \(f_0(x) = f(x)\) and \(N_0 = N^2\), where \(N\) is the number of unknowns. If we use the intervalic wavelets of Section 10.4 in solving (10.1), then number of unknowns (\(N\)) in (10.23), interestingly, does not depend on \(s_0\). This number \(N\) is