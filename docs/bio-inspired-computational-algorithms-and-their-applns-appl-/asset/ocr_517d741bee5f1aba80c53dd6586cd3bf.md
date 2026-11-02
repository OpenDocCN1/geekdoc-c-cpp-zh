![](bbox=[0.08, 0.12, 0.48, 0.38])

![](bbox=[0.52, 0.12, 0.92, 0.38])

![](bbox=[0.08, 0.45, 0.48, 0.7])

![](bbox=[0.52, 0.45, 0.92, 0.7])

Fig. 8. Crossover bias in one-dimensional bounded real space

operator: an evolutionary algorithm using that operator, without selection, is attracted to the areas the search operator prefers. Arguably, also when selection is present, the operator bias acts as a background force that makes the search keener to go toward the areas preferred by the search operator. This is not necessarily bad if the bias is toward the optimum or an area with high-quality solutions. However, it may negatively affect performance if the bias is toward an area of poor-quality solutions. If we do not know the spatial distribution of the fitness of the problem, we may prefer not to have any a priori bias of the search operator, and instead use only the bias of selection, which is informed by the fitness of sampled solutions that constitute empirical knowledge about promising areas obtained in the search, and which is better understood.

In this chapter, we investigate the bias caused by crossover itself and crossover combined with mutation in real-coded GAs. Intuitively, box and line crossover are biased toward the center on the Euclidean space. This intuition is easy to verify experimentally by picking a large number of pairs (ideally infinitely many) of random parents and generating offspring uniformly at random in the boxes (or lines) identified by the pairs of parents.