# 10.11 Multidimensional Scaling

In the previous section, we assumed that the exact surface is unknown, so we have to find the unknown three-dimensional vectors $\vec{j}$ that contain the geometric location of the $j$th node on this surface. Here, on the other hand, the unknown $\vec{j}$ is an $n$-dimensional column vector (for some integer $n \ge 2$) that represents the $j$th node only formally in terms of its distance from the other nodes. The problem of finding such optimal vectors $\vec{j}$ is referred to as multidimensional scaling.

Because the geometric location of the $j$th node is available, the distance between the $j$th and $k$th nodes is known as well, and is denoted by $\delta_{j,k}$. For example, $\delta_{j,k}$ could stand for the geodesic distance on the surface or just the Cartesian distance in the three-dimensional space in which the surface is embedded.

Furthermore, let $\Phi$ be some differentiable mapping from the $n$-dimensional Cartesian space to the $l$-dimensional Cartesian space (for some integer $l \ge 2$). ($\Phi$ can be used to deform the $n$-dimensional space and enhance certain parts of it to make distances calculated there more pronounced, if necessary.) Moreover, let $\Phi'$ denote the Jacobian of $\Phi$, namely, the $l \times n$ matrix whose rows are the gradients of the individual components of $\Phi$ (as in Section 9.14). For example, in the trivial case in which $l=n$ and $\Phi$ is just the identity mapping that changes nothing, $\Phi'=I$ is just the identity matrix of order $l=n$.

Finally, let $\Phi''$ be the $l$-dimensional column vector whose components are not just scalars but rather $n \times n$ matrices (as in Section 9.14). More precisely, each individual component in $\Phi''$ is the Hessian (the matrix of second partial derivatives; see Section 28.7) of the corresponding component of $\Phi$.

Now, let $m$ be the collection of the unknown $n$-dimensional vectors of the form $\vec{j}$. The problem is to find an $m$ that minimizes the function

```
$$g(m) \equiv \sum_{\substack{j,k\in m,\ j\ne k}} \left(\left\|\Phi(\vec{j})-\Phi(\vec{k})\right\|_2^2-\delta_{j,k}^2\right)^2.$$
```

Clearly, $g$ is minimized at such an $m$ for which the gradient of $g$ (the vector of partial derivatives of $g$ with respect to each coordinate of each $\vec{j}\in m$) vanishes:

```
$$f(m)\equiv\nabla g(m)=0.$$
```

To solve this system of equations for $m$, let us first write $f$ more explicitly, using the chain rule. (See Sections 12.5, 28.5, and 30.10; also see Section 12.33 in [69].)

Let $f_j(m)$ denote the $n$-dimensional subvector of $f(m)$ that contains the $n$ components of $f(m)$ that correspond to $\vec{j}\in m$. Note that, in the double sum in the definition of $g(m)$ above, $\vec{j}$ may appear either in the former or in the latter term in the inner squared $l_2$-norm, which contributes an extra factor 2 to the partial derivative of $g(m)$ with respect to $\vec{j}$: