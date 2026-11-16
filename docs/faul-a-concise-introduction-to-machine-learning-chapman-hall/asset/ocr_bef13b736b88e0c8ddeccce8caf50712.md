![](bbox=[0.22, 0.1, 0.76, 0.38])

(a) True function, prediction, bias and constructed basis functions.

![](bbox=[0.22, 0.45, 0.76, 0.56])

(b) Error at training points.

Figure 9.1: Two layer neural network regression with a set of three hidden neurons.

# 9.2 Error Backpropagation

For all neural networks, an error function E(w) needs to be minimized. A necessary condition for a minimum is that the gradient \(\nabla E(\mathbf{w})\) vanishes, where the gradient is the vector formed from the derivatives of E(w) with respect to each component of w, that is each \(w_i^{(l)}\). Hence, one possible technique is to calculate the gradient, set it to zero and solve for the weights. In most cases this is not feasible. Iterative techniques on the other hand use the fact that the gradient evaluated for a particular w points in the direction of the steepest ascent. Thus, its negative gives the direction in which the function decreases most rapidly. The simplest iterative technique is gradient descent and updates the current weight vector w by a step along the negative gradient,

```
\mathbf{w}^{new} = \mathbf{w} - \eta \nabla E(\mathbf{w}),
```