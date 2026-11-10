
The derivation is as follows.

The squared error for a particular training pattern is,

$$
E = \sum_j (t_j - y_j)^2
$$

where \(E\) is the function of all the weights.

The gradient of \(E\) is a vector consisting of the partial derivatives of \(E\) with respect to each of the weights. The error can be reduced rapidly by adjusting the weight \(W_{IJ}\) in the direction of \(-\partial E/\partial W_{IJ}\).

Differentiating \(E\) partially w.r.t. \(W_{IJ}\),

$$
\frac{\partial E}{\partial W_{IJ}} = \frac{\partial \sum_j (t_j - y_j)^2}{\partial W_{IJ}}
$$

$$
\frac{\partial E}{\partial W_{IJ}} = \sum_j (t_j - y_j)\frac{\partial y_j}{\partial W_{IJ}}
$$

Since the weight \(W_{IJ}\) only influences the error at output unit \(Y_J\)

Since

$$
Y_{inj} = \sum_{i=1} x_i w_{iJ}
$$

$$
\frac{\partial E}{\partial W_{IJ}} = 2(t_j - y_j)(-1)\frac{\partial y_j}{\partial W_{IJ}}
= 2(t_j - y_j)\frac{\partial f(y_{inj})}{\partial W_{IJ}}
$$

$$
\frac{\partial E}{\partial W_{IJ}} = 2(t_j - y_j)x_i f'(Y_{inj})
$$

Hence the error is reduced rapidly for a given learning rate \(\alpha\) by adjusting the weights according to the Delta Rule,

$$
\Delta W_{IJ} = \alpha (t_j - y_j)x_i f'(Y_{inj})
$$

gives the extended Delta Rule.

When using the Delta Rule, it is important to ensure that the input data set is well randomized. Well-ordered or structured presentation of the training set can lead to a network which cannot converge to the desired accuracy. If that happens, then the network is incapable of learning the problem.

## Competitive Learning Law or Kohonen's Learning Law

This procedure, developed by Teuvo Kohonen, was inspired by learning in biological systems. In this procedure, the processing elements compete for the opportunity to learn, or update their weights. The processing element with the largest output is declared the winner and has the capability of inhibiting its competitors as well as exciting its neighbors. Only the winner is permitted an output, and only the winner plus its neighbors are allowed to adjust their connection weights. Further, the size of the neighborhood can vary during the training period. The usual paradigm is to start with a larger definition of the neighborhood, and narrow in as the training process proceeds. Because the winning element is defined as the one that has the closest match to the input pattern, Kohonen networks model the distribution of the inputs. This is good for statistical or topological modeling of the data and is sometimes referred to as self-organizing maps or self-organizing topologies.

For a neuron \(P\) to be the winning neuron, its induced local field \(v_p\) for a given particular input pattern must be largest among all the neurons in the network. The output signal of winning neuron is set to one and the signals that lose the competition are set to zero. Hence,

$$
N=\begin{cases}
1 & \text{if } v_p>v_q \text{ for all } q,\ p\neq q \\
0 & \text{otherwise}
\end{cases}
$$

This rule is suited for unsupervised network training. The winner-takes-all or the competitive learning is used for learning statistical properties of inputs. This uses the standard Kohonen learning rule.

Let \(w_{ij}\) denote the weight of input node \(j\) to neuron \(i\). Suppose the neuron has fixed weights, which are distributed among its input nodes:

$$
\sum_j w_{ij}=1 \quad \text{for all } i
$$

A neuron then learns by shifting weights from its inactive to active input nodes. If a neuron does not respond to a particular input pattern, no learning takes place in that neuron. If a particular neuron wins the competition, its corresponding weights are adjusted.

Using the standard competitive rule, the change in \(w_{ij}\) is given as,

$$
\Delta w_{ij}=\begin{cases}
\alpha(x_j-w_{ij}) & \text{if neuron } i \text{ wins the competition}\\
0 & \text{if neuron } i \text{ loses the competition}
\end{cases}
$$

where \(\alpha\) is the learning rate. This rule has the effect of moving the weight vector \(w_i\) of winning neuron \(i\) toward the input pattern \(x\). Through competitive learning, the neural network can perform clustering.

This neighborhood is sometimes extended beyond the simple neuron winner so that it includes the neighboring neurons. Weights are typically initialized at random values and their lengths are normalized during learning in this method. The winner-takes-all neuron is selected either by the dot product or Euclidean norm. Euclidean norm is most widely used because dot product may require normalization.

## Out Star Learning Law

Out star learning rule can be well explained when the neurons are arranged in a layer. This rule is designed to produce the desired response \(t\) from the layer of \(n\) neurons. This type of learning is also called Grossberg learning. Out star learning occurs for all units in a particular layer and no competition among these units is assumed. However, the forms of weight updates for Kohonen learning and Grossberg learning are closely related. In the case of out star learning,

$$
\Delta w_{jk} = \begin{cases}
\alpha(y_k - w_{jk}) & \text{if neuron } j \text{ wins the competition} \\
0 & \text{if neuron } j \text{ loses the competition}
\end{cases}
$$

The rule is used to provide learning of repetitive and characteristic properties of input-output relationships. Though it is concerned with supervised learning, it allows the network to extract statistical properties of the input and output signals. It ensures that the output pattern becomes similar to the undistorted desired output after repetitively applying a distorted output version. The weight change here will be \(\alpha\) times the error calculated.

## Boltzmann Learning Law

The learning is a stochastic learning. A neural net designed based on this learning is called Boltzmann learning. In this learning the neurons constitute a recurrent structure and they work in binary form. This learning is characterized by an energy function, \(E\), the value of which is determined by the particular states occupied by the individual neurons of the machine given by,

$$
E = -\frac{1}{2} \sum_{i} \sum_{j} w_{ij} x_i x_j, \quad i \neq j
$$

where \(x_i\) is the state of neuron \(i\) to neuron \(j\). The value \(i\neq j\) means that none of the neurons in the machine has self feedback. The operation of machine is performed by choosing a neuron at random.

The neurons of this learning process are divided into two groups: visible and hidden. In visible neurons there is an interface between the network and the environment in which it operates but in hidden neurons, they operate independent of the environment. The visible neurons might be clamped onto specific states determined by the environment, called a clamped condition. On the other hand, there is free running condition, in which all the neurons are allowed to operate freely.

## Memory Based Learning Law

In memory based learning, all the previous experiences are stored in a large memory of correctly classified input-output examples \(\{(x_i,t_i)\}_{i=1}^N\) where \(x_i\) is the input vector and \(t_i\) is the desired response. The desired response is a scalar.

The memory based algorithm involves two parts. They are:

- Criterion used for defining the local neighborhood of the test vector
- Learning rule applied to the training in the local neighborhood

One of the most widely used memory based learning is the nearest neighbor rule, where the local neighborhood is defined as the training example that lies in the immediate neighborhood of the test vector \(x\). The vector,

$$
x_n^1 \in \{x_1 \ldots x_n\}
$$

is said to be nearest neighbor of \(x_i\), if, \(\min d(x_i, x_t)=d(x_{n*}^1, x_t)\).

Where \(d(x_i, x_t)\) is the Euclidean distance between the vectors \(x_i\) and \(x_t\).

A variant of nearest neighbor classifier is the K-nearest neighbor classifier, which is stated as,

- Identify the K-classified patterns that are nearest to test vector \(x_t\) for some integer \(K\).
- Assign \(x_t\) to the class that is most frequently represented in the K-nearest neighbors to \(x_t\).

Hence K-nearest neighbor classifier acts like an averaging device. The memory-based learning classifier can also be applied to radial basis function network.

## 2.4.4 MATLAB Implementation of Learning Rules

### MATLAB Snippet to Implement Hebb Rule Syntax

```matlab
[dW, LS] = learnh(W, P, Z, N, A, T, E, gW, gA, D, LP, LS)
```

where

- learnh is the Hebb weight learning function
- learnh(W, P, Z, N, A, T, E, gW, gA, D, LP, LS) takes several inputs
- W -- S x R weight matrix (or S x 1 bias vector)
- P -- R x Q input vectors (or ones(1,Q))
- Z -- S x Q weighted input vectors
