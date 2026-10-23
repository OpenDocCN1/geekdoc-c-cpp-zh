problem is then not only to solve a PDE but first of all to set this missing parameter to its optimal value.

# 30.2  Unspecified Domain

Assume that an elliptic PDE is given in a domain $\Omega$, with, say, mixed boundary conditions on its boundary $\partial\Omega$. However, $\Omega$ is not specified uniquely: it depends on a yet unknown parameter, such as the depth of the slit in Figure 22.3. The problem is then not only to solve the original boundary-value problem in $\Omega$, but first of all to specify this parameter in an optimal way.

# 30.3  Extra Observed Data

To compensate for the missing parameter, we assume that we have an extra piece of information available in advance. For example, we assume that the value $u^{(o)}(z_0)$ of the solution at some boundary point $z_0 \in \partial\Omega$ is known in advance by, say, some preliminary observation. In the model in Figure 22.4, for example, $z_0$ could lie on the right edge of the nearly rectangular domain. In the model in Figure 22.5, on the other hand, $z_0$ could lie on the circular part of the boundary.

# 30.4  Minimizing the Error

For each particular choice of the missing parameter, the domain $\Omega$ has a slightly different shape. For each such domain, one could solve the well-posed PDE numerically and come up with the numerical approximation $u^{(n)}(z_0)$ for the solution at $z_0 \in \partial\Omega$.

Clearly, the optimal value for the parameter is the one for which the error

$$\left|u^{(n)}(z_0)-u^{(o)}(z_0)\right|$$

is minimal. In fact, this error is a scalar function of the parameter. Thus, the golden-ratio algorithm implemented in Section 1.20 can be used to find an optimal parameter that minimizes (locally) this error function.

Furthermore, if observed data are available not only at $z_0$ but also at the boundary points $z_1,z_2,\ldots,z_k \in \partial\Omega$ (for some $k \ge 1$), then the above error can be replaced by the squared average error

$$\sum_{i=0}^{k}\left|u^{(n)}(z_i)-u^{(o)}(z_i)\right|^2.$$

The golden-ratio algorithm can then be used to find the optimal value of the parameter that minimizes (locally) this error function. This value has a better chance to meet the true value of the unknown parameter, as it projects a rather accurate solution not only at $z_0$ but also at the boundary points $z_1,z_2,\ldots,z_k$.

# 30.5  Polluted Cloud

In the above, the inverse problem is to discover an unknown parameter that is important to define the domain properly. In the measuring problem in Section 22.7, for example,