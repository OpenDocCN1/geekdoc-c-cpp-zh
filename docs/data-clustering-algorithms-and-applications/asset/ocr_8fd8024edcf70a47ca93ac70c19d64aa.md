# Network Clustering

stream segment and looks for ways of finding communities among the snapshots in a single segment. GraphScope does not require any input parameter.

In order to extend clustering to dynamic networks, Chi et al. [33] propose frameworks Preserving Cluster Quality (PCQ) and Preserving Cluster Membership (PCM), to measure history cost. PCQ defines how well the partition, at a particular time, performs on the data of the previous time. PCM, on the other hand, measures similarity between the two consecutive partitions. This framework allows insertion and removal of nodes in the graph.

FacetNet uses probabilistic membership models for dynamic community discovery and was proposed by Lin et al. [103]. The authors use K/L divergence to measure quality and history cost. One key benefit of probabilistic models is that they allow to multiply communities for individuals by assigning weights degree of membership. When certain assignments hold, optimization of total cost is equivalent to maximizing log-likelihood function $L(U) = \log P(W;U_t) + \log P(U_t|U_{t-1})$ where $W$ is data at time $t$ and $U_t$ is the cost at [131].

Kim and Ham [92] proposed Greedy optimizations. What they suggest as a remedy is to push the cost to each pair of nodes to get a temporal-smoothed version of node distance and then apply density-based clustering. Greedy local clustering based on mutual information was used to make the model capable of dealing with arbitrary creation/dissolution and growing/shrinking of a community over time [131].

# ## 17.1.3 Heterogeneous Networks

Traditional clustering algorithms assume a homogeneous network where the nodes and edges are of uniform types. In the real world, however, the nodes are often different from each other and so are the edges; for instance, relationships based on communication methods as shown in [73] or both nodes differ at the same time [162]. Another example is the IMDB network where nodes can represent movies, actors, directors, etc., and consequently, the edges can represent different relationships. We often have to deal with heterogeneous networks as well. These diverse networks bring great opportunities as well as challenges—opportunity in the sense that we may gain valuable information from diverse information networks and challenges because we do not know of any obvious methods for appropriately clustering heterogeneous networks.

SONAR API aims at aggregating social information from emails, instant messages, chats, and for the purpose of recommendations based on an aggregated network. It was designed by Guy et al. [73] who showed that the recommendations on an aggregated network performed better than any of the input networks. However, methods to find the best combination scheme were not discussed.

Cai et al. [24] focused on finding the best combination of different source networks at building a target network with adjacency matrix $M$ and regressing it on source networks $M_i$,

```
$a^{it} = \arg\min_{a=1}^n ||\hat{M} - \sum a_i M_i||^2 \quad (17.1)$
```

Here $a_i$ are coefficients of corresponding source networks. Since the target network is rarely known in full, it depends on the users provision of a example target relationships and finds a linear programming function that effectively solves the regression [131]. Star network schema..

Sin et al. [162] proposed the NetClust algorithm that clusters star network. In networks network each is a compound of a single target type and several attribute types. A generative model is used to iteratively rank the posterior probabilities for cluster assignment until convergence. Using ranking distribution for each type of object, piecewise ranking can be retrieved. As mentioned above, this algorithm is limited to only networks with star network schema [131].