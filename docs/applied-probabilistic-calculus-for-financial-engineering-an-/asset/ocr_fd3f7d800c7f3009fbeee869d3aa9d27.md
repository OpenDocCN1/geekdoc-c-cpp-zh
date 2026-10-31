Once again \(E(u)=0\), so one may derive the expression for the variance of the new residual as

\[V(u)=E(u'u)=[\Phi^{-1}+p'\Omega^{-1}p]^{-1}\tag{3.100}\]

and the total variance is

\[V[(y|\pi)]=V(\beta)+V(u)\tag{3.101}\]

One began this section by asserting that the variance of the return process is a known quantity. Improved estimation of the quantity \(\hat{\beta}\) does not change the estimate of the variance of the return distribution, \(\Sigma\). Because of the improved estimate, one does expect that the variance of the estimate (the residual) has decreased, thus the total variance has changed. One may simplify the variance formula (3.92):

\[V(\pi)=\Sigma+\Phi\tag{3.92}\]

to

\[V[(y|\pi)]=\Sigma+V(u)\tag{3.102}\]

This is an intuitive result, consistent with the realities of financial time series. One has combined two estimates of the mean of a distribution to arrive at a better estimate of the mean. The variance of this estimate has been reduced, but the actual variance of the underlying process remains unchanged. Given the uncertain estimate of the process, the total variance of the estimated process has also improved incrementally, but it has the asymptotic limit that it cannot be less than the variance of the actual underlying process.

This is the convention for computing the covariance of the posterior distribution of the conditional reference model as shown in He and Litterman (1999).

In the absence of views, (3.102) simplifies to

\[V[(y|\pi)]=\Sigma+\Phi\tag{3.103}\]

which is the variance of the prior distribution of returns.

# **Bayes’ Theorem for the Estimation Model**

In the Black–Litterman model, the prior distribution is based on the equilibrium-implied excess returns. One of the major assumptions made by the Black–Litterman model is that the *covariance of the prior estimate is proportional to the covariance of the actual returns*, but the two quantities are independent. The parameter \(\tau\) serves as the constant of proportionality. The prior distribution for the Black–Litterman model was specified in 3.87a and 3.87b:

\[P(A)\sim N(\Pi,\tau\Sigma)\tag{3.87a}\]