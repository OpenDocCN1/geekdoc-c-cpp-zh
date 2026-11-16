
since the linear activation function is used. The dependence of the activation \(a_k^{(L)}\) on \(\mathbf{x}_n\) and \(\mathbf{w}\) is made explicit by writing \(a_k^{(L)}(\mathbf{x}_n, \mathbf{w})\).

Taking the derivative with respect to \(w_{ji}^{(l)}\), we arrive at

```
\(\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \sum_{k=1}^K (a_k^{(L)}(\mathbf{x}_n, \mathbf{w}) - t_{nk}) \frac{\partial}{\partial w_{ji}^{(l)}} a_k^{(L)}(\mathbf{x}_n, \mathbf{w})\)
\(= \sum_{k=1}^K (y_k(\mathbf{x}_n, \mathbf{w}) - t_{nk}) \frac{\partial}{\partial w_{ji}^{(l)}} a_k^{(L)}(\mathbf{x}_n, \mathbf{w}).\)
(9.1)
```

It is the weighted sum of the errors in the output neurons, where the weights are the derivative of the corresponding activation with respect to \(w_{ji}^{(l)}\). Note that also in this derivative the chain rule needs to be employed, unless \(l=L\), in which case \(a^{(L)}\) depends directly on \(w_{ji}^{(l)}\). We look at this in more detail later. First, we take a look at the other possible machine learning tasks.

If the neural network performs binary classification, there is only one output neuron. We resolve the last step of the forward propagation, that is the application of the final activation function, explicitly in the \(n^{\text{th}}\) error function,

```
\(E_n(\mathbf{w}) = -t_n \log \frac{1}{1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))}\)
\(-(1 - t_n) \log \left( 1 - \frac{1}{1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))} \right)\)
\(= t_n \log \left( 1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w})) \right)\)
\(-(1 - t_n) \log \frac{\exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))}{1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))}\)
\(= \log \left( 1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w})) \right) + (1 - t_n) a^{(L)}(\mathbf{x}_n, \mathbf{w}).\)
```

Differentiating with respect to \(w_{ji}^{(l)}\) gives

```
\(\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \frac{\exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))}{1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))} \frac{\partial}{\partial w_{ji}^{(l)}} (-a^{(L)}(\mathbf{x}_n, \mathbf{w}))\)
\(+ (1 - t_n) \frac{\partial}{\partial w_{ji}^{(l)}} a^{(L)}(\mathbf{x}_n, \mathbf{w})\)
\(= \left( \frac{1}{1 + \exp(-a^{(L)}(\mathbf{x}_n, \mathbf{w}))} - 1 \right) \frac{\partial}{\partial w_{ji}^{(l)}} a^{(L)}(\mathbf{x}_n, \mathbf{w})\)
\(+ (1 - t_n) \frac{\partial}{\partial w_{ji}^{(l)}} a^{(L)}(\mathbf{x}_n, \mathbf{w})\)
\(= (y(\mathbf{x}_n, \mathbf{w}) - t_n) \frac{\partial}{\partial w_{ji}^{(l)}} a^{(L)}(\mathbf{x}_n, \mathbf{w})\)
```

It has the same functional form as (9.1) with \(K=1\).

Using the fact that the error function of $K$ simultaneous binary classification tasks is the sum over the error functions of the individual binary classification problems, also for this error function, the derivative of the $n^{\text{th}}$ contribution with respect to $w_{ji}^{(l)}$ takes the form of (9.1).

Lastly, we look at classifying $K$ multiple classes, when $\mathbf{t}_n$ has a 1-of-$K$ representation. Let $k_n$ be the index of the component of $\mathbf{t}_n$ which equals one. Since all other components are zero, the $n^{\text{th}}$ contribution to the error function is

$E_n(\mathbf{w}) = -\log \frac{\exp(a_{k_n}^{(L)})}{\sum_{s=1}^K \exp(a_s^{(L)})} = \log \left( \sum_{s=1}^K \exp(a_s^{(L)}) \right) - a_{k_n}^{(L)}.$

The derivative with respect to $w_{ji}^{(l)}$ is

$\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \frac{\sum_{r=1}^K \exp(a_r^{(L)}) \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(L)}}{\sum_{s=1}^K \exp(a_s^{(L)})} - \frac{\partial}{\partial w_{ji}^{(l)}} a_{k_n}^{(L)} = \sum_{r=1}^K y_r(\mathbf{x}_n, \mathbf{w}) \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(L)} - t_{nr} \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(L)} = \sum_{r=1}^K (y_r(\mathbf{x}_n, \mathbf{w}) - t_{nr}) \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(L)},$

where we used the 1-of-$K$ representation of $\mathbf{t}_n$. This has the same functional form as (9.1).

The fact that the derivatives of the $n^{\text{th}}$ contribution of all error functions result in (9.1) is known as the *canonical link* between the output activation functions and the error function.

The chain rule needs to be employed, until we reach the layer, where there is a direct dependency on $w_{ji}^{(l)}$. Let $s$ be any layer index greater than or equal to $l$. We will show by backwards induction that

$\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \sum_{m=1}^{M_s} \delta_m^{(s)} \frac{\partial}{\partial w_{ji}^{(l)}} a_m^{(s)}(\mathbf{x}_n, \mathbf{w})$ (9.2)

for suitably chosen $\delta_m^{(s)}$.

This is already the case for $s=L$, due to Equation (9.1), if we set $M_L = K$ and define

$\delta_k^{(L)} = y_k(\mathbf{x}_n, \mathbf{w}) - t_{nk},$

which is the error in the $k^{\text{th}}$ output.

We assume that (9.2) is true for some $s > l$ and show that it is true for $s-1$. Since

$a_m^{(s)}(\mathbf{x}_n, \mathbf{w}) = \sum_{r=1}^{M_{s-1}} w_{mr}^{(s)} z_r^{(s-1)} = \sum_{r=1}^{M_{s-1}} w_{mr}^{(s)} h_{s-1} \left( a_r^{(s-1)}(\mathbf{x}_n, \mathbf{w}) \right),$

the derivative with respect to \( w_{ji}^{(l)} \) is

\(\frac{\partial}{\partial w_{ji}^{(l)}} a_m^{(s)}(\mathbf{x}_n, \mathbf{w}) = \sum_{r=1}^{M_{s-1}} w_{mr}^{(s)} h'_{s-1}(a_r^{(s-1)}) \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(s-1)}(\mathbf{x}_n, \mathbf{w}),\)

where \( h'_{s-1} \) is the derivative of \( h_{s-1} \).

Inserting this into (9.2), we obtain

\(\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \sum_{m=1}^{M_s} \delta_m^{(s)} \sum_{r=1}^{M_{s-1}} w_{mr}^{(s)} h'_{s-1}(a_r^{(s-1)}) \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(s-1)}(\mathbf{x}_n, \mathbf{w})\)
\(= \sum_{r=1}^{M_{s-1}} \underbrace{h'_{s-1}(a_r^{(s-1)}) \sum_{m=1}^{M_s} \delta_m^{(s)} w_{mr}^{(s)}}_{\delta_r^{(s-1)}} \frac{\partial}{\partial w_{ji}^{(l)}} a_r^{(s-1)}(\mathbf{x}_n, \mathbf{w}),\)

which is of the required form.

The errors \(\delta^{(s-1)}\) are defined in terms of \(\delta^{(s)}\), the weights in the \( s^{\text{th}} \) layer and the derivative of the activation function in layer \( s-1 \) evaluated at the activations of this layer. They can be calculated by propagating backwards through the network from one set of neurons to the next. This is known as _error backpropagation_

Once we reach the \( l^{\text{th}} \) layer, we have

\(\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \sum_{m=1}^{M_l} \delta_m^{(l)} \frac{\partial}{\partial w_{ji}^{(l)}} a_m^{(l)}(\mathbf{x}_n, \mathbf{w}),\)

and \( a_m^{(l)} \) is directly dependent on \( w_{ji}^{(l)} \) via

\( a_m^{(l)} = \sum_{s=1}^{M_{l-1}} w_{ms}^{(l)} h_s^{(l-1)}.\)

Differentiation is straightforward and we arrive at

\(\frac{\partial}{\partial w_{ji}^{(l)}} a_m^{(l)}(\mathbf{x}_n, \mathbf{w}) = \begin{cases} 0 & \text{for } m \neq j \\ z_i^{(l-1)} & \text{for } m = j \end{cases}.\)

The derivative of the \( n^{\text{th}} \) contribution to the error becomes

\(\frac{\partial}{\partial w_{ji}^{(l)}} E_n(\mathbf{w}) = \delta_j^{(l)} z_i^{(l-1)}.\)

It is the error in the \( j^{\text{th}} \) neuron of the \( l^{\text{th}} \) set of neurons (letting the output neurons be the \( L^{\text{th}} \) set) multiplied by the \( i^{\text{th}} \) variable in the previous set of neurons, if the synapse connects neuron \(i\) to neuron \(j\). Note that, if \(l = 1\), then those variables are the input variables, while, when \(l > 1\), they are the latent variables. Schematically, this is illustrated as

![](img/d3c00252180686426c9e63ab889b535b_296_0.png)

In the process of training a neural network, the weights are first initialized, most often randomly. In forward propagation, the training samples are passed through the neural network, calculating all intermediate activations and latent variables, as well as the output for each. Then the errors of each training point are calculated in a backward pass through the network. After this, the derivative with respect to every weight in the network of the contribution to the error function of each training sample is calculated. These form the gradient, either batch, mini-batch or stochastic. The weights are updated by the chosen optimization method.

To get some intuition of what is happening, consider binary classification. We denote the weights in the last layer by \(w^{(L)}\), since there is only one output neuron. Because of \(a^{(L)} = \sum_{k=1}^{M_{L-1}} w_{k1}^{(L)} z_k^{(L-1)}\), the derivatives with respect to the weights in the last layer of the \(n\)th contribution to the error sum are

\(\frac{\partial}{\partial w_{ki}^{(L)}} E_n(\mathbf{w}) = (y(\mathbf{x}_n, \mathbf{w}) - t_n) z_i^{(L-1)}\)

Since \(y(\mathbf{x}_n, \mathbf{w})\) is interpreted as the probability of \(\mathbf{x}_n\) belonging to the positive class, the difference lies in the interval \((-0.5, 0]\) for \(t_n = 1\), if the network classifies \(x_n\) correctly as belonging to the positive class, and between \([-1, -0.5)\) otherwise. If on the other hand, \(t_n = 0\), the difference lies in \((0.5, 1]\), if the network incorrectly puts this sample in the positive class, and in the interval \([0, 0.5)\) otherwise. This means that, when the weights get updated
