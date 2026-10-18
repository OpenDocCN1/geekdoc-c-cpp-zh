
follows: $\alpha_t(i)=P(x_1=o_1,\ldots,x_t=o_t,y_t=q_i\mid\Lambda)$ and $\beta_t(i)=P(x_{t+1}=o_{t+1},\ldots,x_T=o_T\mid y_t=q_i,\Lambda)$. Note the forward values enable us to solve the problem through marginalizing, then we obtain

$$P(X_1^T\mid\Lambda)=\sum_{i=1}^{N}P(o_1,\ldots,o_T,y_T=q_i\mid\Lambda)=\sum_{i=1}^{N}\alpha_T(i).$$

The forward values can be computed efficiently with the principle of *dynamic programming*:

$$\alpha_1(i)=\pi_i b_i(o_1),$$
$$\alpha_{t+1}(j)=\left[\sum_{i=1}^{N}\alpha_t(i)a_{ij}\right]b_j(o_{t+1}).$$

Similarly, the backward values can be computed as

$$\beta_T(i)=1,$$
$$\beta_t(i)=\sum_{j=1}^{N}a_{ij}b_j(o_{t+1})\beta_{t+1}(j).$$

The backward values will be used in the Baum-Welch algorithm.

Given the parameters of HMM and a particular sequence of observations, another interesting task is to compute the most likely sequence of states that could have produced the observed sequence. We can find the most likely sequence by evaluating the joint probability of both the state sequence and the observations for each case. For example, in Part-of-speech (POS) tagging [18], we observe a token (word) sequence $X_1^T=o_1,\ldots,o_T$, and the goal of POS tagging is to find a stochastic optimal tag sequence $Y_1^T=y_1y_2\ldots y_T$ that maximizes $P(Y_1^T,X_1^T)$. In general, finding the most likely explanation for an observation sequence can be solved efficiently using the **Viterbi algorithm** [12] by the recurrence relations:

$$V_1(i)=b_i(o_1)\pi_i,$$
$$V_t(j)=b_j(o_t)\max_i\left(V_{t-1}(i)a_{ij}\right).$$

Here $V_t(j)$ is the probability of the most probable state sequence responsible for the first $t$ observations that has $q_j$ as its final state. The Viterbi path can be retrieved by saving back pointers that remember which state $y_{t-1}=q_i$ was used in the second equation. Let $Ptr(y_t,q_i)$ be the function that returns the value of $y_{t-1}$ used to compute $V_t(i)$ as follows:

$$y_T=\arg\max_{q_i\in\Omega_Y}V_T(i),$$
$$y_{t-1}=Ptr(y_t,q_i).$$

The complexity of this algorithm is $O(T\times N^2)$, where $T$ is the length of the observed sequence and $N$ is the number of possible states.

Now we need a method of adjusting the parameters $\Lambda$ to maximize the likelihood for a given training set. The **Baum-Welch algorithm** [4] is used to find the unknown parameters of HMMs, which is a particular case of a generalized EM algorithm [9]. We start by choosing arbitrary values for the parameters, then compute the expected frequencies given the model and the observations. The expected frequencies are obtained by weighting the observed transitions by the probabilities specified in the current model. The expected frequencies obtained are then substituted for the old parameters and we iterate until there is no improvement. On each iteration we improve the probability of being observed from the model until some limiting probability is reached. This iterative procedure is guaranteed to converge on a local maximum [34].

## 3.4.3 Markov Random Fields

Now we turn to another major class of graphical models that are described by undirected graphs and that again specify both a factorization and a set of conditional independence relations. A Markov random field (MRF), also known as an undirected graphical model [14], has a set of nodes, each of which corresponds to a variable or group of variables, as well as a set of links, each of which connects a pair of nodes. The links are undirected, that is, they do not carry arrows.

### 3.4.3.1 Conditional Independence

Given three sets of nodes, denoted A, B, and C, in an undirected graph G, if A and B are separated in G after removing a set of nodes C from G, then A and B are conditionally independent given the random variables C, denoted as A ⊥⊥ B|C. The conditional independence is determined by simple graph separation. In other words, a variable is conditionally independent of all other variables given its neighbors, denoted as X_v ⊥⊥ X_{V\{v}∪ne(v)} | X_{ne(v)}, where ne(v) is the set of neighbors of v. In general, an MRF is similar to a Bayesian network in its representation of dependencies, and there are some differences. On one hand, an MRF can represent certain dependencies that a Bayesian network cannot (such as cyclic dependencies); on the other hand, MRF cannot represent certain dependencies that a Bayesian network can (such as induced dependencies).

### 3.4.3.2 Clique Factorization

As the Markov properties of an arbitrary probability distribution can be difficult to establish, a commonly used class of MRFs are those that can be factorized according to the cliques of the graph. A clique is defined as a subset of the nodes in a graph such that there exists a link between all pairs of nodes in the subset. In other words, the set of nodes in a clique is fully connected.

We can therefore define the factors in the decomposition of the joint distribution to be functions of the variables in the cliques. Let us denote a clique by C and the set of variables in that clique by x_C. Then the joint distribution is written as a product of potential functions ψ_C(x_C) over the maximal cliques of the graph

p(x_1,x_2,...,x_n) = 1/Z ∏_C ψ_C(x_C),

where the partition function Z is a normalization constant and is given by Z = Σ_x ∏_C ψ_C(x_C). In contrast to the factors in the joint distribution for a directed graph, the potentials in an undirected graph do not have a specific probabilistic interpretation. Therefore, how to motivate a choice of potential function for a particular application seems to be very important. One popular potential function is defined as ψ_C(x_C) = exp(−ε(x_C)), where ε(x_C) = ln ψ_C(x_C) is an energy function [29] derived from statistical physics. The underlying idea is that the probability of a physical state depends inversely on its energy. In the logarithmic representation, we have

p(x_1,x_2,...,x_n) = 1/Z exp( − Σ_C ε(x_C) ).

The joint distribution above is defined as the product of potentials, and so the total energy is obtained by adding the energies of each of the maximal cliques.

A log-linear model is a Markov random field with feature functions f_k such that the joint distribution can be written as

p(x_1,x_2,...,x_n) = 1/Z exp( Σ_{k=1}^K λ_k f_k(x_{C_k}) ),

where f_k(x_{C_k}) is the function of features for the clique C_k, and λ_k is the weight vector of features. The log-linear model provides a much more compact representation for many distributions, especially when variables have large domains such as text.

### 3.4.3.3 The Inference and Learning Algorithms

In MRF, we may compute the conditional distribution of a set of nodes given values $A$ to another set of nodes $B$ by summing over all possible assignments to $v \notin A, B$, which is called *exact inference*. However, the exact inference is computationally intractable in the general case. Instead, approximation techniques such as MCMC approach [1] and loopy *belief propagation* [5, 30] are often more feasible in practice. In addition, there are some particular subclasses of MRFs that permit efficient Maximum a posteriori (MAP) estimation, or more likely, assignment inference, such as associative networks. Here we will briefly describe belief propagation algorithm.

Belief propagation is a message passing algorithm for performing inference on graphical models, including Bayesian networks and MRFs. It calculates the marginal distribution for each unobserved node, conditional on any observed nodes. Generally, belief propagation operates on a factor graph, which is a bipartite graph containing nodes corresponding to variables $V$ and factors $U$, with edges between variables and the factors in which they appear. Any Bayesian network and MRF can be represented as a factor graph. The algorithm works by passing real valued function called *messages* along the edges between the nodes. Taking pairwise MRF as an example, let $m_{ij}(x_j)$ denote the message from node $i$ to node $j$, and a high value of $m_{ij}(x_j)$ means that node $i$ “believes” the marginal value $P(x_j)$ to be high. Usually the algorithm first initializes all messages to uniform or random positive values, and then updates message from $i$ to $j$ by considering all messages flowing into $i$ (except for message from $j$) as follows:

$$m_{ij}(x_j)=\sum_{x_i} f_{ij}(x_i,x_j)\prod_{k\in ne(i)\setminus j}m_{ki}(x_i),$$

where $f_{ij}(x_i,x_j)$ is the potential function of the pairwise clique. After enough iterations, this process is likely to converge to a consensus. Once messages have converged, the marginal probabilities of all the variables can be determined by

$$p(x_i)\propto\prod_{k\in ne(i)}m_{ki}(x_i).$$

The reader can refer to [30] for more details. The main cost is the message update equation, which is $O(N^2)$ for each pair of variables ($N$ is the number of possible states).

Recently, MRF has been widely used in many text mining tasks, such as text categorization [7] and information retrieval [28]. In [28], MRF is used to model the term dependencies using the joint distribution over queries and documents. The model allows for arbitrary text features to be incorporated as evidence. In this model, an MRF is constructed from a graph $G$, which consists of query nodes $q_i$ and a document node $D$. The authors explore full independence, sequential dependence, and full dependence variants of the model. Then, a novel approach is developed to train the model that directly maximizes the mean average precision. The results show significant improvements are possible by modeling dependencies, especially on the larger Web collections.

## 3.4.4 Conditional Random Fields

So far, we have described the Markov network representation as a joint distribution. One notable variant of an MRF is a conditional random field (CRF) [19, 40], in which each variable may also be conditioned upon a set of global observations. More formally, a CRF is an undirected graph whose nodes can be divided into exactly two disjoint sets, the observed variables $X$ and the output variables $Y$, which can be parameterized as a set of factors in the same way as an ordinary Markov network. The underlying idea is that of defining a conditional probability distribution $p(Y|X)$ over label sequences $Y$ given a particular observation sequence $X$, rather than a joint distribution over both label and observation sequences $p(Y,X)$. The primary advantage of CRFs over HMMs is their
