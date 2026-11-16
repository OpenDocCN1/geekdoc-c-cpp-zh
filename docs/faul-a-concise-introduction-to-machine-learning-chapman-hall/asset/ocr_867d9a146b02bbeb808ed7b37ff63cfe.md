network is illustrated as

![](bbox=[0.12, 0.13, 0.88, 0.43])

The dotted connections indicate that any combination of hidden neurons and layers is possible.

For \( l \neq 1, L \), the result of the propagation function is the activation

\( a_j^{(l)} = \sum_{i=1}^{M_{l-1}} w_{ji}^{(l)} z_i^{(l-1)} = \mathbf{w}_j^{(l)T} \mathbf{z}^{(l-1)}. \)

This is passed to the activation function, also called transfer function, of this layer \( h_l \) to generate the latent variable

\( z_j^{(l)} = h_l(a_j^{(l)}) = h_l\left(\mathbf{w}_j^{(l)T} \mathbf{z}^{(l-1)}\right). \)

For \( l = 1 \), we have

\( a_j^{(1)} = \mathbf{w}_j^{(1)T} \mathbf{x} \quad \text{and} \quad z_j^{(1)} = h_1\left(\mathbf{w}_j^{(1)T} \mathbf{x}\right). \)

For \( l = L \), the output variables \( y_1, \dots y_K \) are calculated,

\( y_k = h_L(a_k^{(L)}) = h_L\left(\mathbf{w}_k^{(L)T} \mathbf{z}^{(L-1)}\right). \)

A list of possible activation functions is given in Section 5.5. The choice depends on the problem at hand:

+   * For regression problems: the identity, i.e. the linear activation function \( h_L(x) = x \) is used in the output layer.