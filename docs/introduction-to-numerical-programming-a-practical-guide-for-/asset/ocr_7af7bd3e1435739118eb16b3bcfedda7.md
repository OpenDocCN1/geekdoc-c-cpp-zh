**TABLE 11.1** Monte Carlo Estimates of the Integral \(I=\int_0^1 xe^{-x}\,dx\) and Associated Standard Deviations \(\sigma\), Calculated Using Random Sequences with the Distributions \(w(x)=1\) and, Respectively, \(w(x)=(3/2)x^{1/2}\)\n\n| \(n\) | \(w(x)=1\): \(I\) | \(w(x)=1\): \(\sigma\) | \(w(x)=(3/2)x^{1/2}\): \(I\) | \(w(x)=(3/2)x^{1/2}\): \(\sigma\) |\n|---:|---:|---:|---:|---:|\n| 10 | 0.25108 | 0.03855 | 0.26860 | 0.00727 |\n| 100 | 0.26252 | 0.01085 | 0.26397 | 0.00285 |\n| 1000 | 0.26622 | 0.00336 | 0.26458 | 0.00089 |\n| 10,000 | 0.26544 | 0.00105 | 0.26423 | 0.00027 |

classical one-dimensional quadrature formula proves the latter to be significantly more efficient. While the Monte Carlo integration can be yet improved, its full potential comes to light only in the evaluation of multidimensional integrals.

# 11.3 Importance Sampling

Having in view that the uncertainty \(\sigma\) (11.2) of the Monte Carlo quadrature is directly related to the variance of the integrand \(\sigma_f\), which measures the deviation of the integrand from its average value, to increase the precision and efficiency of the quadrature, one can apply a general strategy, known as *variance reduction*. More precisely, we discuss a technique called *importance sampling*.

Essentially, one introduces a positive *weight function*, \(w(x)\), normalized to unity over the interval \([0,1]\),

\[\int_0^1 w(x)\,dx=1,\tag{11.8}\]

by which integrand (11.5) is multiplied and divided:

\[I=(b-a)\int_0^1\frac{f((b-a)x+a)}{w(x)}w(x)\,dx.\]

Performing the change of variable \(d\xi=w(x)dx\) or, in integral form,

\[\xi(x)=\int_0^x w(x')\,dx',\tag{11.9}\]

with the boundary conditions \(\xi(0)=0\) and \(\xi(1)=1\) (to comply with normalization (11.8)), the integral becomes

\[I=(b-a)\int_0^1\frac{f((b-a)x(\xi)+a)}{w(x(\xi))}\,d\xi.\tag{11.10}\]

The conservation of the integration domain upon the change of variable is a direct consequence of the normalization of \(w(x)\). To evaluate this integral, one can directly apply the Monte Carlo method described in the preceding section, by averaging the new integrand, \(f/w\), over a set of *uniformly distributed* sampling points \(\xi_i\) from the interval \([0,1]\):

\[I\approx\frac{b-a}{n}\sum_{i=1}^{n}\frac{f((b-a)x(\xi_i)+a)}{w(x(\xi_i))}.\tag{11.11}\]

The performed change of variable may seem at first glance to turn the quadrature more complicated. The advantages of this technique become apparent only if one chooses the weight function \(w(x)\), in as