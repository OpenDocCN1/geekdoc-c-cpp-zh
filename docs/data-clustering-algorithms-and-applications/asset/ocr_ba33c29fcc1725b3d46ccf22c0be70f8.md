# Probabilistic Models for Clustering

$Q(\Theta, \Theta^{(i)})$. In situations, a generalized EM algorithm (GEM) [23, 53, 16] is defined for the M-step requires $\Theta^{(r+1)}$ to be chosen such that

$Q(\Theta^{(r+1)}, \Theta^{(i)}) \geq Q(\Theta^{(i)}, \Theta^{(i)})$

holds. That is, one chooses a better value $\Theta^{(r+1)}$ to increase the Q-function, $Q(\Theta, \Theta^{(i)})$, rather than find the local maximum of it. The convergence can be guaranteed using GEM, and has been widely used for the estimation of topic modeling with graph-based regularization, such as NetPLA [30] and TMBP [24].

**Variational EM**: The variational EM addresses the problem of an intractable E-step, which is one of the approximate algorithms used in LDA [14]. The idea is to find a set of variational parameters with respect to hidden variables that attempts to obtain the tightest possible bound in E-step and to maximize the lower bound in M-step. The variational parameters are chosen in a way that simplifies the original probabilistic model and are thus easier to cluster. There is no guarantee that variational EM will find a local optimum.

**Stochastic EM**: In some situations, the EM algorithm involves an integral that may not tractable, such as LDA [14]. The idea of stochastic EM (SEM) [20, 46] is to replace this tedious computation with a stochastic simulation. The E-step is computed with Monte Carlo sampling. This introduces randomness into the optimization, but asymptotically will converge to a local optimum.

# 3.3.2 Mixture Models Revisited

With our general definition of the EM algorithm, let us revisit the case of estimating parameters for Gaussian mixture model and Bernoulli mixture model, respectively. The EM algorithm is an iterative algorithm that has two main steps. In the E-step, it tries to guess the values of the hidden variable $z_{nk}$, in the M-step, it updates the parameters of the model based on the guesses of the E-step.

**Gaussian Mixture Model**: The parameters of a Gaussian mixture model include the mean vectors $\mu_k$, covariance matrices $\Sigma_k$ and mixing weights $\pi_k$. In the E-step, we calculate the posterior, or responsibility, of the hidden variable $z_{nk}$, given the current set of parameters. Using Bayes' theorem,

$q(z_{nk} = 1) = p(z_{nk}|x_n, \mu_k, \Sigma_k) = \frac{\pi_k p(x_n|\mu_k, \Sigma_k)}{\sum_{j=1}^K \pi_j p(x_n|\mu_j, \Sigma_j)} = \gamma(z_{nk})$, (3.28)

which is the responsibility of the component $k$ for data $x_n$. In the M-step, we need to maximize the quantity $Q(\Theta, \Theta^{(i)})$. From the independence, the expectation of the complete log-likelihood (3.25) can be rewritten as

$Q(\Theta, \Theta^{(i)}) = \sum_{n=1}^N \sum_{k=1}^K \gamma(z_{nk}) \log \pi_k p(x_n|\mu_k, \Sigma_k)$. (3.29)

Compared with the log-likelihood function (3.11) for the incomplete data, the algorithm now operates on distributions. By fixing the responsibilities, we can maximize $Q(\Theta, \Theta^{(i)})$ with respect to $\mu_k, \Sigma_k$, and $\pi_k$. This leads to closed-form solutions for updating $\mu_k, \Sigma_k$, and $\pi_k$, by (3.12), (3.14), and (3.15). This is precisely the EM algorithm for Gaussian mixtures as derived.

**Relationship of EM with the k-Means**: Given a data set, the goal of k-means is to partition the data set into number $K$ clusters, such that the sum of the square distances of each data point to the center of its cluster is a minimum. We introduce a binary responsibility, $r_{nk}$, to describe the ownership of a data point that belongs to cluster $k$ if $r_{nk} = 1$, where