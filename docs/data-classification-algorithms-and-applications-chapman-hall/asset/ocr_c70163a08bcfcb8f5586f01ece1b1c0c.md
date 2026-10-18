the first RBM’s hidden layer outputs as the second RBM’s visible layer, and then continuing up to the last hidden layer.

# 8.6.2.2  Stack Auto-Encoder

Stacked auto-encoders are MLPs with an architecture designed to regenerate input data [11, 55]. The MLP is trained to reproduce an estimate $\hat{\mathbf{x}} = (\hat{x}_1, \cdots, \hat{x}_d)$ of the input $\mathbf{x} = (x_1, \cdots, x_d)$, thus forcing the MLP to encode an internal representation of $\mathbf{x}$ in the hidden units. It generally features a single or two hidden layers that are responsible for creating a hidden representation of the data. The network tries to minimize the mean square error $E$ between input and output as

$$E(\hat{\mathbf{x}},\mathbf{x}) = \sum_{i=1}^{d}(x_i-\hat{x}_i)^2 \tag{8.88}$$

and by doing so, the MLP encodes an internal presentation in the hidden layers that can be used to regenerate the data in the output layer. Auto-encoding can be likened to a non-linear principal component estimation. When used within a deep-learning system, each hidden layer of the DNN is used as a hidden layer in an encoder and trained accordingly. After training is done, the weights are fixed and used to generate data for the next layer, which is also trained within an auto-encoder using the outputs of the previously trained layer. The process is repeated up to the last hidden layer. A deep CNN (DCNN) design was proposed based on those principles and achieved an improved performance compared to the original CNN version [81, 109]; it was a good showcase of the dual-use of domain knowledge in the design of the CNN architecture and layer-wise training for network optimization.

# 8.6.3  Limits and Applications

Deep learning is a powerful methodology well-suited to training deep and large networks. However, it does require the availability of powerful computing capabilities, which justifies the use of special accelerator hardware such as GPU in training deep neural networks.

Successful applications of deep networks have already been presented on a large variety of data. We have pointed out the impressive results obtained by the CNN and the DCNN in image recognition [31, 81, 109], speech detection recognition [123], and sound classification [82]. Deep learning has had an important impact on speech recognition where it has helped achieve better performance than state-of-the-art systems. For speech recognition, it is used as a probability estimator within a hidden Markov model architecture, which demonstrates an example of a hybrid system-based deep learning technique [54, 72].

# 8.7  Summary

We have seen in this chapter that neural networks are powerful universal mappers for data classification endowed with certain properties such as non-linearity, the capacity to represent information in a hierarchical fashion, and the use of parallelism in performing the classification tasks. The resurging interest of neural networks coincides with the availability of high-performance computing to perform computationally demanding tasks. The emergence of training methodologies to exploit these computing resources and the concrete results achieved in selected classification tasks make neural networks an attractive choice for classification problems. The choice of a particular network is still linked to the task to be accomplished. Prior knowledge is an important element to consider