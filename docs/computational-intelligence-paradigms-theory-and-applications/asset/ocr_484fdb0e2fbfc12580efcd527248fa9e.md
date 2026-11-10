The BAM architecture resembles a single layer feedforward network which consists of only one layer of weighted interconnections. There exists “n” number of input neurons in the input layer and “m” number of output neurons in the output layer. The training process is based on the Hebb learning rule. This is a fully interconnected network, wherein the inputs and outputs are different. The most important feature of a bidirectional associative memory is that there exists weighted interconnections from both X-layer to Y-layer and vice versa. The link between one layer to another and its reciprocate is shown in Figure 4.12 by the arrow pointing on both sides. The weights are adjusted between X-layer to Y-layer and also from Y-layer to X-layer.

# Types of Bi-Directional Associative Memory Net

There exists two types of BAM. They are

+   - Discrete BAM
+   - Continuous BAM

# Discrete BAM

The training patterns can be either binary or bipolar. In both the formats the weights are found from the sum of the Hebb outer product of the bipolar form of the training vector pairs. Step activation function with a threshold value is used as the activation function. Generally the bipolar vectors improve the performance of the net.

The weight matrix to store the set of input and target vectors s (p): t (p), p=1,...,P, where

$$s(p)=(s_1(p),\ldots,s_i(p),\ldots,s_n(p))$$

and can be determined with the help of Hebb rule.

For binary input vectors, weight matrix can be determined by the formula.

$$W_{ij}=\sum_p(2s_i(p)-1)(2t_j(p)-1)$$

For bipolar input vectors, the weight matrix is given by,

$$W_{ij}=\sum_p s_i(p)t_j(p)$$

# Activation Function

The activation function for discrete BAM depends on whether binary or bipolar vectors are used. The activation function is the appropriate