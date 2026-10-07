
# Data Clustering: Algorithms and Applications

## 1.2 Feature Selection Methods

The feature selection phase is an important preprocessing step which is needed in order to enhance the quality of the underlying clustering. Not all features are equally relevant to finding the clusters, some may be noisier than others. Therefore, it is often helpful to utilize a process in which the noisy and irrelevant features are pruned from contention. Feature selection and dimensionality reduction are closely related. In dimensionality reduction, linear combinations of features may be used in techniques such as principal component analysis [50] in order to further enhance the feature selection effect. The advantage of the former is greater interpretability, whereas the advantage of the latter is a lesser number of transformed dimensions required for the representation process. Chapter 2 of this book will discuss feature selection methods in detail. A comprehensive book on feature selection may be found in [61].

It should be noted that feature selection can also be integrated directly into the clustering algorithm well. This is particularly useful, when different features are relevant to different localities of the data. The motivating factor for high dimensional clustering algorithms is the failure of global feature selection algorithms. As noted in [9]: in many real data examples, some points are correlated with respect to a given set of dimensions and others are correlated with different dimensions. Thus, it may not always be feasible to prune off many dimensions at the same time incurring a substantial loss of information; the use of local selection, by integrating the feature selection process into the algorithm, is the best way of achieving this goal. Local feature selections can also be extended to the dimensionality reduction problem [8, 19] and are sometimes referred to as local dimensionality reduction. Such methods are discussed in detail in Chapter 9. Furthermore, Chapter 2 also discusses the consequences of these classes of methods to the problem of feature selection.

### 1.2.2 Probabilistic and Generative Models

In probabilistic models, the core is to model the data from a generative process. First, a specific form of the generative model (e.g., mixture of Gaussians) is assumed, and then the parameters of this model are estimated with the use of the Expectation Maximization (EM) algorithm [27]. The available data set is used to estimate the parameters in such way that they have a maximum likelihood fit to the probabilistic model. Given this model, we estimate the generative probabilities (or fit probabilities) of the underlying data points. Data points which fit the distribution will have high probabilities, whereas anomalies will have very low probabilities.

The broad principle of a mixture-based generative model is to assume that the data were generated from a mixture of k distributions with the probability distributions $G_1 \dots G_k$ with the use of the following process:

- Pick a distribution with prior probability $\alpha_i$, where $i \in \{1...k\}$, in order to pick one of the k distributions.
- Generate a data point from $G_i$.

The probability distribution $G_i$ is picked from a host of different possibilities. Note that this generative process requires the determination of several parameters such as the prior probabilities and the model parameters for each distribution $G_i$. Models with level of flexibility may be designed upon whether the prior probabilities are specified as part of the problem setting, or whether interattribute correlations are assumed within a component of the mixture. Note the model parameters and the probability assignment of data points to clusters are dependent on one another in a circular way. Iterative methods are desirable in order to resolve this circular. The generative models are typically solved with the use of an EM approach, which starts off with a random or heuristic initialization and then iteratively uses two steps to resolve the circularity in computation:

- (E-Step) Determine the expected probability of assignment of data points to clusters with the current model parameters
- (M-Step) Determine the optimum model parameters of each mixture using the assignment probabilities as weights.

One nice property of EM-models is that they can be generalized easily to different kinds of data, as long as the generative model for each component is properly selected for the individual mixture $G_i$. Some examples are as follows:

- For numerical data, a Gaussian mixture may be used in order to model each component $G_i$. Such a model is discussed in detail in Chapter 3.
- For categorical data, a Bernoulli model may be used for $G_i$ in order to model the generation of the discrete values.
- For sequence data, a Hidden Markov Model (HMM) may be used for $G_i$ in order to model the generation of a sequence. Interestingly, an HMM is itself a special kind of mixture model in which the components of the mixture are dependent on each other through transitions. Thus, the clustering of sequence data with a mixture of HMMs can be considered a two-level mixture model.

Generative models are the most fundamental of all clustering methods, because they help to understand the underlying process through which a cluster is generated. A number of interesting connections exist between other clustering methods and generative models, by considering cases in terms of prior probabilities or mixture parameters. For example, the special case in which each probability is fixed to the same value and the radius along all dimensions reduces to a soft version of the $k$-means algorithm. These connections will be discussed in detail in Chapter 3.

### 1.2.3 Distance-Based Algorithms

Many forms of generative algorithms can be shown to be distance-based algorithms. This is because the mixture components in generative models often use a distance function within the probability distribution. For example, the Gaussian distribution represents data probabilities in the euclidean distance from the mean of the mixture. As a result, a generative model with the Gaussian distance can be shown to have a very close relationship with the $k$-means algorithm. In fact, distance-based algorithms can be shown to be reductions or simplifications of decent generative models.

Distance-based methods are also desirable because of their simplicity and ease of implementation. Distance-based algorithms can generally be divided into types:

- Flat: In this case, the partitioning is performed directly on the data. It is instructive to compare the partitioning of data points to clusters which are dependent on one another in a circular way. Iterative methods are desirable in order to resolve this circularity. The generative models are typically solved with the use of an EM approach, which starts off with a random or heuristic initialization and then iteratively uses two steps to resolve the circularity in computation:

- (E-Step) Determine the expected probability of assignment of data points to clusters with the current model parameters
- (M-Step) Determine the optimum model parameters of each mixture using the assignment probabilities as weights.

One nice property of EM-models is that they can be generalized easily to different kinds of data, as long as the generative model for each component is properly selected for the individual mixture $G_i$. Some examples are as follows:

- For numerical data, a Gaussian mixture may be used in order to model each component $G_i$. Such a model is discussed in detail in Chapter 3.
- For categorical data, a Bernoulli model may be used for $G_i$ in order to model the generation of the discrete values.
- For sequence data, a Hidden Markov Model (HMM) may be used for $G_i$ in order to model the generation of a sequence. Interestingly, an HMM is itself a special kind of mixture model in which the components of the mixture are dependent on each other through transitions. Thus, the clustering of sequence data with a mixture of HMMs can be considered a two-level mixture model.

Generative models are the most fundamental of all clustering methods, because they help to understand the underlying process through which a cluster is generated. A number of interesting connections exist between other clustering methods and generative models, by considering cases in terms of prior probabilities or mixture parameters. For example, the special case in which each probability is fixed to the same value and the radius along all dimensions reduces to a soft version of the $k$-means algorithm. These connections will be discussed in detail in Chapter 3.

Distance-based methods are also desirable because of their simplicity and ease of implementation. Distance-based algorithms can generally be divided into types:

- Hierarchical: In these methods, the clusters are represented hierarchically using a dendrogram, with varying levels of granularity. Depending upon whether this hierarchical representation is created in top-down or bottom-up fusion, these representations may be either agglomerative or divisive.

- Agglomerative: In these methods, a bottom-up approach is used, in which we start with the initial data points and successfully merge clusters in order to create a tree-like structure. A variety of choices are possible in how these clusters may be merged, which provide different tradeoffs between quality and efficiency. Some examples of these are single-linkage, all-pairs linkage, centroid-linkage, and sampled-linkage clustering. In single-linkage, the shortest distance between any two points is used. In all-pairs linkage, the average over all pairs is used, whereas sampled linkage, a sampling of the data points in the two clusters is used for calculating the average distance. In centroid-linkage, the distance between the centroids is used. Some of these methods have the disadvantage of chaining, in which larger clusters are naturally biased towards having closer distances to other points and will attract a successively larger number of points.
Single linkage
