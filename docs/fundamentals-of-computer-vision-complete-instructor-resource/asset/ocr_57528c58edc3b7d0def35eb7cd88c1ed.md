Since we want \(x^{(k+1)}\) to be a zero of \(H\), we set

\(H(x^{(k)}) + (x^{(k+1)} - x^{(k)})H'(x^{(k)}) = 0, \quad (3.42)\)

and find that to estimate a root, we should use

\(x^{(k+1)} = x^{(k)} - \frac{H(x^{(k)})}{H'(x^{(k)})}. \quad (3.43)\)

In optimization, however, we are not finding roots, but rather minimizing a function, so how does knowing how to find roots help us? The minima of the function are the roots of its derivative, and the “gradient descent” algorithm becomes

\(x^{(k+1)} = x^{(k)} - \frac{H'(x^{(k)})}{H''(x^{(k)})}. \quad (3.44)\)

In higher dimensions, Eq. 3.44 becomes

\(\mathbf{x}^{(k+1)} = \mathbf{x}^{(k)} - \mathbf{H}^{-1}\nabla H, \quad (3.45)\)

where \(\mathbf{H}\) is the Hessian matrix of second derivatives, which we mentioned earlier in this chapter:

\(\mathbf{H} = \left[ \frac{\partial^2}{\partial x_i \partial x_j} H(\mathbf{x}) \right]. \quad (3.46)\)

and comparing Eq. 3.41 with Eq. 3.45, we have

\(\alpha = \mathbf{H}^{-1}.\)

Note that \(\alpha\) is not a scalar any more.

**Exercise 3.2:** Given a set of \(x, y\) data pairs \(\{(x_i, y_i)\}\) and a function of the form

\(y = ae^{bx}, \quad (3.47)\)

find the parameters \(a\) and \(b\) that minimize

\(H(a, b) = \sum_i (y_i - ae^{bx_i})^2. \quad (3.48)\)

# **Solution**

We can solve this problem with the linear approach by observing that \(\ln y = \ln a + bx\) and redefining variables \(g = \ln y\) and \(r = \ln a\). With these substitutions, Eq. 3.48 becomes

\(H(r, b) = \sum_i (g_i - r - bx_i)^2 \quad (3.49)\)

\(\frac{\partial H}{\partial b} = 2 \sum_i (g_i - r - bx_i)(-x_i) \quad (3.50)\)

\(\frac{\partial H}{\partial r} = 2 \sum_i (g_i - r - bx_i)(-1). \quad (3.51)\)

We can solve this minimization problem by either setting the derivatives equal to zero and finding the root of the simultaneous equations, or using the gradient descent algorithm if