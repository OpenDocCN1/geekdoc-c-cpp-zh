![](bbox=[0.196, 0.113, 0.696, 0.276])

Figure 10.25 n points are found that lie along a straight line between \(\theta_1\) and \(\theta_f\). Each of those is then projected onto the manifold to find new value for the \(\theta\)’s.

Find the projections of all these points onto the manifold, and denote them \(\theta_1 - \theta_n\). Since \(\theta'_i = \theta_i\) and \(\theta'_f = \theta_f\) are already on the manifold, there is no need to project them.

+   2. Compute new values for the \(d\)’s, using, as shown in Figure 10.26

```
\(\mathbf{d}_i = (\mathbf{d}_{i-1} + \boldsymbol{\theta}_{i+1})/2, \quad i = 2, \dots, n-1. \quad (10.104)\)
```

This process, estimating \(\mathbf{d}_i\) from \(\mathbf{d}_i - 1\) and \(\boldsymbol{\theta}_{i+1}\), is called *leapfrog*. The set of points defined by the \(\mathbf{d}_i\) defines a *poly-line*, an end-to-end set of straight line segments. Resample that polyline into \(n\) equally spaced (along the polyline) segments. These will be new estimates of the points \(\mathbf{d}_i\).

+   3. Project these \(\mathbf{d}'s\) as above and iterate until converged. Thus usually requires just a couple of iterations.

After convergence, each of these points lies on a geodesic of the manifold of close shapes. This process is illustrated in Figure 10.24. In that figure, the top line illustrates one type of shark at the far left, and a different type at the far right. Both are closed curves. By using the method described in this section, intermediate values may be computed that are also closed curves, unlike the lower portion of Figure 10.24.

![](bbox=[0.196, 0.683, 0.696, 0.863])

Figure 10.26 New values for the d's are computed, and these will closer to the manifold. For example, \(\mathbf{d}_i = (\mathbf{d}_i + \boldsymbol{\theta}_i)/2\).