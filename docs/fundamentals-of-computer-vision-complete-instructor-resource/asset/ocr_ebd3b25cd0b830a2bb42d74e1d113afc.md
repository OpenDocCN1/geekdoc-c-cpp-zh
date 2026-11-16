The derivative is required to perform gradient descent with respect to the unknown image \( f \) so we calculate (from Eq. B.8):

```
\(\frac{\partial H_p}{\partial f_i} = \frac{b}{\sqrt{2\pi}\tau} \left( \left( \frac{(f \otimes r)}{\tau^2} \exp \left( - \frac{(f \otimes r)^2}{2\tau^2} \right) \right) \otimes r_{rev} \right)_i\)
```

where \( r_{rev} \) denotes the mirror image of the kernel \( r \). In order to follow the derivation most easily, think of \( r \) as the kernel that estimates the first derivative. Then \( (f \otimes r)_i \) can be written \( (\nabla f)_i \). Below, the subscript \( i \) will be dropped just to keep the number of parentheses manageable.

We seek to make the magnitude of the gradient of the image small almost everywhere. To get insight into what is going on, replace some of the convolution notation in Eq. 6.34 by gradients:

```
\(\frac{\partial H_p}{\partial f_i} = \kappa ((\nabla f) \exp(-(\nabla f)^2)) \otimes r_{rev}\)
```

and then

```
\(\frac{\partial H_p}{\partial f_i} = -\kappa (\nabla ((\nabla f) \exp(-(\nabla f)^2)))\)
```

In the equation above, the constants are lumped together into \( \kappa \); and the annealing control parameter, \( \tau \), is set to 1 for clarity. Note that for centered first derivative kernels, \( f \otimes r = - (f \otimes r_{rev}) \).

Finally, consider the use of \( \frac{\partial H_p}{\partial f_i} \) in a gradient descent algorithm. In the simplest implementations of gradient descent, \( f \) is updated by

```
\( f^{k+1} = f^k - \eta \frac{\partial H_p}{\partial f_i} \)
```

where \( f^k \) denotes the value of \( f \) at iteration \( k \), and \( \eta \) is some small constant. Rewriting Eq. 6.37,

```
\( -\frac{\partial H_p}{\partial f_i} = \frac{f_i^{k+1} - f_i^k}{\eta} \)
```

Note that the left-hand side of Eq. 6.38 represents a change in \( f \) between iterations \( k \) and \( k + 1 \), and in fact bears a strong resemblance to the form of the derivative of \( f \). We make this similarity explicit by defining that iteration \( k \) is calculated at time \( t \) and iteration \( k + 1 \) calculated at time \( t + \Delta t \). Since \( t \) is an artificially introduced parameter, without physically meaningful units, we may scale it by any convenient proportionality constant, and we obtain

```
\( -\frac{\partial H_p}{\partial f_i} = \frac{f(t + \Delta t) - f(t)}{\Delta t} \approx \frac{\partial f_i}{\partial t} \)
```

where we have allowed the constant \( \alpha \) to be renamed \( \Delta t \) so that the expression looks like a derivative with respect to time. Substituting this (re)definition into Eq. 6.35, we have our final result: By simply changing notation and making explicit the time between iterations, the derivative of the MAP prior term may be rewritten as

```
\(\frac{\partial f_i}{\partial t} = \kappa (\nabla ((\nabla f) \exp(-(\nabla f)^2)))\)
```