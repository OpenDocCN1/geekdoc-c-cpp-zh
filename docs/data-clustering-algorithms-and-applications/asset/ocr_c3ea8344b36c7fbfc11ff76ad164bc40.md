# 468 Data Clustering: Algorithms and Applications

The additive property from the fact that the statistics in the individual microclusters are expressed as a separable additive sum of the statistics over individual data points. We note that the single component t(C1 ∪ C2) is given by max{t(C1), t(C2)}. Note that the additive property is an important one, which ensures it is easy to keep track of the cluster statistics as new data points arrive. Next, we will discuss the process of microclustering. UMicro algorithm works using an iterative approach which maintains a number of microcentroids around which the clusters are built. It assume that one of the inputs to the algorithm is n_micro which is the number of microclusters to be constructed. The algorithm starts with a number of null clusters and initially creates new singleton clusters, to which new points are subsequently added. For any incoming data point, the closest cluster centroid is determined by the expected distance of the data point to the uncertain microclusters. The process of expected distance computation for the closest centroid is tricky and will be subsequently discussed. Furthermore, for the incoming point, it is determined whether it lies within a critical uncertainty boundary of the microcluster, otherwise the data point is added to the microcluster. To create a new microcluster, either it must be added to the current set of microclusters or it needs to replace one of the existing clusters of the algorithm, the current number of microclusters is less than n_micro. If this is the case, the new data point is added to the current set of microclusters as a separate microcluster with a singleton point in. Otherwise, the data point replaces one of the older microclusters. For this purpose, we replace the least recently updated microcluster from the set. This information is available from the temporal timestamp in the different microclusters. The overall framework for the uncertain stream clustering is illustrated in Figure 18.3. Next, we will discuss the process of computation of individual subtroutines as the expected distance or the uncertainty boundary.

```
Algorithm UMicro(Number of Clusters: n_micro)
begin
 S = {};
 { Set of micro-clusters }
repeat
  Receive the next stream point X;
  { Initially, when S is null, the computations below
    cannot be performed, and X is simply
    added as a singleton micro-cluster to S }
  Compute the expected similarity of X to the closest
    micro-cluster M in S;
  Compute critical uncertainty boundary of M;
  if X lies inside uncertainty boundary
    add X to statistics of M
  else
    add a new micro-cluster to S containing singleton
    point X;
  if |S| = n_micro + 1 then remove the least recently
    updated micro-cluster from S;
until data stream ends;
end
```

FIGURE 18.3: The UMicro algorithm.

© 2014 by Taylor & Francis Group, LLC