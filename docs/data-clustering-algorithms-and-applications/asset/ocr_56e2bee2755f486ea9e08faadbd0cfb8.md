# Data Clustering: Algorithms and Applications

A Bernoulli mixture model [18] is a special case of mixture models, where each component has a $D$-dimensional Bernoulli distribution with parameters $\mu_k = \{\mu_{k1}, \dots, \mu_{kD}\}^T$,

```
$p(\mathbf{x}|\mu_k) = \prod_{i=1}^D \mu_{ki}^{x_i}(1-\mu_{ki})^{1-x_i}}.$
```

Let $K$ the number of components, a mixture model with $K$ Bernoulli components can be written in the form

```
$p(\mathbf{x}|\pi) = \prod_{k=1}^K \pi_k p(\mathbf{x}|\mu_k),$
```

where $\mu ={\mu_1, \dots, \mu_K\}$ and $\pi ={\pi_1, \dots, \pi_K\}$, the log-likelihood for the model is given

```
$\log p(\mathbf{x}|\mu) = \sum_{k=1}^K \log p(\mathbf{x}|\mu_k)$
```

```
$\log (\sum_{n=1}^N \sum_{k=1}^K \prod_{i=1}^D \mu_{ki}^{x_{ni}}(1-\mu_{ki})^{1-x_{ni}})..$
```

Note that the summation appears inside the log, so that there is no close-form result for maximum likelihood solution. EM is a standard learning algorithm for estimating the parameters of this model. In Section 3.3 we will show the general EM algorithm, and the solution for Bernoulli mixture model will be shown and revisited in Section 3.3.2.

Here us discuss a real application of the Bernoulli mixture model by using it to model written digits. Imagine we are given an $M \times M$ binary (black-and-white) image that is to scan of a digit between 0 and 9, but we do not know which digit is written. We can create a mixture model with $K=10$ different components, where each component is a vector of size $M^2$ of Bernoulli distributions (one per pixel). Such can be trained with the EM algorithm on an unlabeled set of digits and will effectively cluster the images according to the digit written.

# 3.2.4 Model Selection Criteria

With the model-based approach to clustering, issues such as the selection of the number of clusters or the selection of the validity of a given model can be addressed in a principled and formal way. In mixture modeling, an important issue is the selection of the number of components, which is assumed to be fixed in previous subsections. However, unlike the trade-off in model selection problem, with too many components may overfit the data, while a mixture with too few components may not be flexible enough to approximate the underlying model. Thus, we need to adopt some statistical procedures to estimate the parameter in to the number of components.

To illustrate the problem of model selection, let us denote $M_k$ as the class of all possible $k$-component mixtures built from a certain type of distribution. The MLE criterion cannot be directly used to estimate the number of mixture components $K$ the maximized likelihood function $\log p(\mathbf{X}|\Theta_{ML})$ is a nondecreasing function of $k$. Therefore, $M_k \in M_{k+1}$, MLE criterion is useless to estimate the number of components, and some added model selection methods have been proposed.

From a computational point of view, there are two main types of model selection methods: deterministic and stochastic methods. Deterministic methods usually start by setting a set of