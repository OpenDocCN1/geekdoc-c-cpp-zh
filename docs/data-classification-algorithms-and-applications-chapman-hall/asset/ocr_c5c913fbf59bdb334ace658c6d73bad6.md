approximating a mapping $f : \mathbb{R}^d \to \mathbb{R}^K$, where target values are the natural basis of $\mathbb{R}^K$. It has been proven that with the use of the 1-of-K encoding scheme and an adequate error criterion, such as the mean square error or cross-entropy, an MLP output can approximate posterior probabilities [14,111,131]:

$o_k \approx P(C_k|\mathbf{x})$  (8.52)

for all $k$. This is, however, an asymptotic result. In practice, the sigmoidal unit’s output values do not allow for a probabilistic interpretation since they do not sum to one. For a probabilistic interpretation of the network’s outputs, a softmax transformation on the output unit’s net value or activation can be used [26]:

$o_k = \frac{e^{v_k}}{\sum_{j=1}^K e^{v_j}}$  (8.53)

where clearly $\sum_{k=1}^K o_k = 1$.

# 8.5.1.3 Forward Propagation

The forward propagation refers to the transfer of data from the input layer to the output layer. Let us assume that an MLP is made of $L$ layers where indices $1,\cdots ,L-1$ refer to set of hidden layers and the index $L$ represents the output layer. Per convention, we will use index 0 to represent the input layer. For a $K$-class problem, the MLP features $K$ output units, where each output unit produces an output $o_k$, given an input example $\mathbf{x}$. As illustrated in Figure 8.4 the input data is propagated from the input layer to the output layer as follows:

**From input layer to hidden layer:** The input layer passes the $d$-dimensional input example $\mathbf{x}$ to each unit in the first hidden layer, $\mathcal{H}_1$, where the $h$-th unit computes a net value $v_h^{(1)}$ and output $z_h^{(1)}$ as:

$v_h^{(1)} = \sum_{i=0}^d w_{ih}^{(1)} x_i$  (8.54)
$z_h^{(1)} = \phi(v_h^{(1)})$  (8.55)

where $w_{ih}^{(1)}$ denotes the weights of the synapse connecting the $i$-th input unit to the $h$-th hidden unit in the first layer; we assume that $w_{0h}^{(1)}$ refers to bias and $x_0 = 1$. For simplicity, we also assume that all units in the network use the same activation function $\phi(\cdot)$.

**From hidden layer to hidden layer:** A unit $h$ in the $l$-th hidden layer, $\mathcal{H}_l$, gets its data from units in the previous layer, $\mathcal{H}_{l-1}$, to produce an internal output as

$v_h^{(l)} = \sum_{h'\in \mathcal{H}_{l-1}} w_{h'h}^{(l)} z_{h'}^{(l-1)}$  (8.56)
$z_h^{(l)} = \phi(v_h^{(l)})$  (8.57)

where $w_{h'h}^{(l)}$ denotes the synapse weights between the $h'$-th hidden unit in the layer $\mathcal{H}_{l-1}$ and the $h$-th hidden unit in the layer $\mathcal{H}_l$; $l \in \{2,\cdots ,L-1\}$.

**From hidden layer to output layer:** Finally, a $k$-th output unit produces a network’s response:

$v_k^{(L)} = \sum_{h\in \mathcal{H}_{L-1}} w_{hk}^L z_h^{(L-1)}$  (8.58)
$o_k = \phi(v_k^{(L)})$  (8.59)