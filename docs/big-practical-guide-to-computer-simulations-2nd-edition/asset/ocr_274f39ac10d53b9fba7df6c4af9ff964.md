![](bbox=[0.07, 0.11, 0.47, 0.43])

![](bbox=[0.53, 0.11, 0.93, 0.43])

![](bbox=[0.07, 0.51, 0.47, 0.79])

![](bbox=[0.53, 0.51, 0.93, 0.79])

Fig. 8.43 Upper left: Result of the clustering of sample set A with the k-means algorithm for k = 3. Different symbols correspond to different clusters. The lines show how the centers have moved during the iterations of the algorithm. Upper right: result of the k-means algorithm for sample set B and k = 5. Here, the algorithm mistakenly subdivides the cluster around (1.0,0) into three sub-clusters. Lower left: spread χ² as a function of the number of clusters k. Above the most suitable number k = 3 the spread decreases only slightly when increasing the number of clusters. Lower right: For sample set B, k-means fails even if the most suitable number k = 2 is chosen.

seeds for the random number generator, different spreads and thus different cluster assignments will occur. Such a non-unique convergence, observed after restarting the cluster_k_means() function, may also be used as an indicator that k is not well chosen.

Often, the most suitable number k of clusters is in fact not known in advance. In this case, it helps sometimes to perform the clustering for several values of k and observe the spread χ² as a function of k, see lower left of Fig. 8.43. The spread shrinks monotonously when increasing k. When