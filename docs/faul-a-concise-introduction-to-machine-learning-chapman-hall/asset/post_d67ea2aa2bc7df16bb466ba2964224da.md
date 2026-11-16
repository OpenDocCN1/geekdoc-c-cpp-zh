
Schematically, this can be visualized as

![](img/d3c00252180686426c9e63ab889b535b_311_0.png)

This is reminiscent of a three layer neural network with two sets of hidden neurons and the linear activation function, which is the identity, in each neuron. The weights of the synapses from the input neurons to the first set of hidden neurons are given by the entries of the matrix \(\mathbf{D}^T\), while the weights of the synapses from the first set to the second set of hidden neurons are given by the entries of the matrix \((\mathbf{D}^T \mathbf{D})^{-1}\). Lastly, the weights from the second set of hidden neurons to the output neurons are given by the matrix \(\mathbf{D}\). The variables of the second set of hidden neurons are the coefficients \(c_1, \dots, c_M\).

In a neural network, however, the weights of the synapses are updated iteratively in a learning process, until the output is similar enough to the input. In ordinary least squares, all is entirely determined by the design matrix \(\mathbf{D}\), which only depends on the chosen basis functions, but not \(t_1, \dots, t_D\). However, if a set of training data \(\mathbf{t}_1, \dots, \mathbf{t}_N\) is available, they can be fed through this neural network. The error sum of squares between the predictions and the input is

\[
E(\mathbf{D}) = \sum_{n=1}^N (\mathbf{t}_n^T \mathbf{t}_n - \mathbf{t}_n^T \mathbf{D} (\mathbf{D}^T \mathbf{D})^{-1} \mathbf{D}^T \mathbf{t}_n) ,
\]

since it is the ordinary least squares solution. The derivative with regards to the entry \(D_{ij}\) of \(\mathbf{D}\) is

\[
\frac{\partial}{\partial D_{ij}} E(\mathbf{D}) = \sum_{n=1}^N ((\mathbf{D}^T \mathbf{D})^{-1} \mathbf{D}^T \mathbf{t}_n)_j (\mathbf{D} (\mathbf{D}^T \mathbf{D})^{-1} \mathbf{D}^T \mathbf{t}_n - \mathbf{t}_n)_i ,
\]

where the subscript of the brackets denotes the component of the vector in the brackets. It is the sum over the training data of the products of the latent variable of the \(j^{th}\) neuron in the second set of hidden neurons with the error in the i-th output neuron, when the n-th training sample passes through the network. The thus obtained gradient can be used to update the entries of D. Note that this effectively means only updating the weights in the final layer giving a new matrix D, since the weights of the other layers are given by D^T and (D^T)^{-1}. This inverse might not exist, which is an inherent problem of ordinary least squares, which can be addressed by ridge regression as seen in equation 8.3. Thus the design matrix can be inferred from the data, if there are enough data samples t_n.

The matrix DD^T is symmetric and positive semi-definite. It can be diagonalized by an orthogonal matrix Q such that DD^T = QPQ^T, where P is a diagonal matrix with non-negative entries. Thus the predictions are

\[
D(D^T D)^{-1} D^T t = D(QP^{1/2} P^{1/2} Q^T)^{-1} D^T t
= (DQP^{-1/2})(P^{-1/2} Q^T D^T) t
= (DQ P^{-1/2})(DQ P^{-1/2})^T t.
\]

This is a tied two-layer autoencoder with the linear layer as activation function. The weights of the first layer are given by the entries of (DQ P^{-1/2})^T and those of the second layer by DQ P^{-1/2}. This illustrates again the link of the weights of an autoencoder to the model space which was originally defined as the columns of D being functions evaluated at the points, where data samples are taken. The application of P^{-1/2} are different scalings of the hidden variables, while Q is either a rotation or a reflection, since it is an orthogonal matrix.

Continuing in this vein, the mean of the predictive distribution for t in Section 8.13 is given by

\[
\mathbf{D}\mu = \sigma^{-2} \boldsymbol{\Sigma} \mathbf{D} \mathbf{D}^T \mathbf{t}.
\]

Schematically, this can be drawn as

![](img/d3c00252180686426c9e63ab889b535b_312_0.png)

Again, it can be viewed as a neural network with two sets of hidden neurons. As before, the weights from the input neurons to the first set of hidden neurons are given by the entries of \(\mathbf{D}^T\), and from the second set of hidden neurons to the output neurons by the entries of \(\mathbf{D}\). The weights between the two sets of hidden neurons are given by the entries of \(\sigma^{-2}\boldsymbol{\Sigma}\). Since \(\boldsymbol{\Sigma} = (\mathbf{A} + \sigma^{-2}\mathbf{D}^T\mathbf{D})^{-1}\) and since the entries of \(\mathbf{A}\) are determined by maximizing the log evidence of \(\mathbf{t}\), the weights between the hidden neurons may depend on both the design matrix \(\mathbf{D}\) and \(t_1, \dots, t_D\). The number of hidden neurons in each set, \(M\), can change dynamically which is equivalent to the addition and deletion of basis functions. Equally, the number of input and output neurons can increase, if samples are taken at previously unseen locations.

As before with ordinary least squares, a set of training data \(\mathbf{t}_1, \dots, \mathbf{t}_N\) can be used to infer the entries of \(\mathbf{D}\). Whenever \(\mathbf{D}\) is updated, \(\mathbf{A}\) needs to be updated by maximizing the log evidence of \(\mathbf{t}\) again.

## 9.6 Indian Buffet Process

The last section suggests a technique of inferring a model space with variable dimension. In this section, we consider the data generation process similar to the Chinese Restaurant Process in Section 6.6 where the number of clusters is unknown. Now the dimension of the latent feature space is unknown.

As in the previous section, let \(\mathbf{t}_1, \dots, \mathbf{t}_N\) be a set of data samples in a \(D\) dimensional space. We assume that for \(n = 1, \dots, N\)
\(\mathbf{t}_n = \mathbf{D}\mathbf{c}_n + \boldsymbol{\epsilon}_n,\)

where \(\boldsymbol{\epsilon}_n\) is additive Gaussian noise with zero mean and variance \(\sigma^2\mathbf{I}\) specific to this data sample, the columns of the \(D \times M\) matrix \(\mathbf{D}\) represent latent features, and \(\mathbf{c}_n\) is the sample specific vector of coefficients.

Commonly, this is represented as
\(\mathbf{T} = \mathbf{C}\mathbf{D}^T + \mathbf{E},\)

where \(\mathbf{T}\) is the \(N \times D\) matrix of data samples with each row being one sample, \(\mathbf{C}\) is the \(N \times M\) matrix of coefficients, and \(\mathbf{E}\) is a \(N \times D\) matrix with each entry being drawn from a normal distribution with zero mean and variance \(\sigma^2\). In this context, \(\mathbf{D}\) is the factor loading matrix and its columns are the factor loadings, while \(\mathbf{C}\) is the coordinate matrix.

From the data generation viewpoint, we allow the number of columns in \(\mathbf{C}\) and number of rows in \(\mathbf{D}^T\), which is \(M\), to be infinite. While infinity is conceptually a difficult concept, it can be dealt with by imposing that only a finite, small number of entries in each row of \(\mathbf{C}\) are non-zero. In practical terms, this means that we only see a finite amount of data and each data sample is generated as a finite linear combination of features. Other features from the infinite set are those which we have not yet encountered in our data.

To this end, the matrix C is written in terms of a binary indicator matrix Z and a weight matrix W. That is

\(C = Z \odot W,\)

where \(\odot\) denotes the element-wise, Hadamard product.

The data generation is linked to customers choosing dishes from an Indian Buffet, hence the name Indian Buffet Process (IBP). The customers are indexed by \(1, \dots, n, \dots, N\). There are infinitely many dishes, but not all have been chosen yet. These are the latent features indexed by \(m\). \(M\) is the number of different dishes chosen so far.

The number of dishes \(i_1\) the first customer chooses is drawn from a Poisson distribution with rate \(\lambda\), which is the expected number of dishes each customer chooses. In matrix Z, the first \(i_1\) entries of the first row are set to one and \(M = i_1\). \(M\) is the number of distinct dishes chosen so far. The amount he takes from each dish is recorded in the first row of matrix W.

The \(n^{th}\) customer chooses from the \(M\) dishes any of the previous customers have already chosen with probability \(j_m/n\), if dish \(m\) was chosen \(j_m\) times. In other words, \(j_m\) is the number of non-zero entries in column \(m\) above row \(n^{th}\) in matrix Z. If he chooses a particular dish \(m\), then a one is placed in the \(n^{th}\) column of the \(n^{th}\) row of Z. He also tries \(i_n\) new dishes, where \(i_n\) is drawn from a Poisson distribution with rate \(\lambda/n\). These are indicated by ones in columns with numbers \(M+1, \dots, M+i_n\) in the \(n^{th}\) row. \(M\) is updated to \(M+i_n\). Again, the amount of each dish is recorded in the \(n^{th}\) row of W.

Since \(\lambda/n\) decreases with every new customer, the probability that he will choose even just one new dish decreases, but does not become zero. This means that if our model space does not have enough features to explain the data, there is a non-zero probability to create a feature which will help explain the data.

In each row, the expected number of non-zero entries is \(\lambda\). This is true for the first row, since the expectation of a Poisson distribution is given by the rate \(\lambda\). Assume that the expected number of non-zero entries for rows \(1, \dots, n-1\) is \(\lambda\). The expected number nonzero entries in the \(n^{th}\) row is

\[
\begin{aligned}
\mathbb{E}[\sum_{m=1}^M \frac{j_m}{n}] + \frac{\lambda}{n} &= \frac{1}{n} \mathbb{E}[\sum_{m=1}^M \sum_{k=1}^{n-1} Z_{km}] + \frac{\lambda}{n} \\
&= \frac{1}{n} \sum_{k=1}^{n-1} \mathbb{E}[\sum_{m=1}^M Z_{km}] + \frac{\lambda}{n} \\
&= \frac{(n-1)\lambda}{n} + \frac{\lambda}{n} = \lambda,
\end{aligned}
\]

where \(Z_{km}\) denotes the \((k, m)\) entry in matrix Z. By induction, this proves that the expected number of non-zero entries in each row is \(\lambda\).

Since the probability of choosing a particular dish depends on the number of times it has been the choice of any of the previous customers, we again
