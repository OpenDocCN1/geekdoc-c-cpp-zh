
# Algorithm SubspaceDecisionPath(Test Example: t, Data Set: D, MaxDimensionality: l, MaxBranchFactor: b_max, Minimum Interest Ratio: ir_min)

```
begin
  PATH = {D};
  while not(termination) do
  begin
    Pick the last data set L indicated in PATH;
    E = {E1 ... Eq} = ComputeClassificationSubspaces(L, t, l, b_max, ir_min);
    for each Ei ConstructDensityProfile(Ei, L, t);
    { "Zooming in" refers to further subspace exploration }
    if (zoom-in (user-specified)) then
    begin
      User specifies choice of branch Ei;
      User specifies accuracy density threshold λ for zoom-in;
      { p(L', Ci) is accuracy significance of class Ci in L' with respect to L }
      (L', p(L', C1) ... p(L', Ck)) = IsolateData(L, t, λ);
      Add L' to the end of PATH;
    end;
    else begin (retreat)
      User specifies data set L' on PATH to backtrack to;
      Delete all data set pointers occuring after L' on PATH; (backtrack)
    end;
    { Calculate cumulative dominance of each class Ci along PATH in order to provide the user a measure of its significance }
    for each class Ci do
      Output CD(PATH, Ci) = 1 − ∏_{L∈PATH, L≠D} (1 − p(L, Ci)) to user;
  end;
end
```

## FIGURE 6.5: The subspace decision path method.

diagnostic characteristics, a maximum branch factor b_max, and a minimum interest density ir_min. In addition, the maximum dimensionality l of any subspace utilized in data exploration is utilized as user input. The value of l = 2 is especially interesting because it allows for the use of visual profile of the accuracy density. Even though it is natural to use 2-dimensional projections because of their visual interpretability, the data exploration process along a given path reveals a higher dimensional combination of dimensions, which is most suitable for the test instance. The branch factor b_max is the maximum number of possibilities presented to the user, whereas the value of ir_min is the corresponding minimum interest density of the test instance in any subspace presented to the user. The value of ir_min is chosen to be 1, which is the break-even value for interest density computation. This break-even value is one at which the interest density neither under-estimates nor over-estimates the accuracy of the test instance with respect to a class. The variable PATH consists of the pointers to the sequence of successively reduced training data sets, which are obtained in the process of interactive decision tree construction. The list PATH is initialized to a single element, which is the pointer to the original data set D. At each point in the decision path construction process, the subspaces E1 ... Eq are determined, which have the greatest interest density (of the dominant class) in the locality of the test instance t. This process is accomplished by the procedure ComputeClassificationSubspaces. Once these subspaces have been determined, the density profile is constructed for each of them by

the procedure ConstructDensityProfile. Even though one subspace may have higher interest density at the test instance than another, the true value of a subspace in separating the data locality around the test instance is often a subjective judgement that depends both upon the interest density of the test instance and the spatial separation of the classes. Such a judgement requires human intuition, which can be harnessed with the use of the visual profile of the accuracy density profiles of the various possibilities. These profiles provide the user with an intuitive idea of the class behavior of the data set in various projections. If the class behavior across different projections is not very consistent (different projections are indicative of different classes), then such a node is not very revealing of valuable information. In such a case, the user may choose to backtrack by specifying an earlier node on PATH from which to start further exploration.

On the other hand, if the different projections provide a consistent idea of the class behavior, then the user utilizes the density profile in order to isolate a small region of the data in which the accuracy density of the data in the locality of the test instance is significantly higher for a particular class. This is achieved by the procedure IsolateData. This isolated region may be a cluster of arbitrary shape depending upon the region covered by the dominating class. However, the use of the visual profile helps to maintain the interpretability of the isolation process in spite of the arbitrary contour of separation. An example of such an isolation is illustrated in Figure 6.4(b), and is facilitated by the construction of the visual density profile. The procedure returns the isolated data set L′ along with a number of called the accuracy significance p(L′, Ci) of the class Ci. The pointer to this new data set L′ is added to the end of PATH. At that point, the user decides whether further exploration into that isolated data set is necessary. If so, the same process of subspace analysis is repeated on this node. Otherwise, the process is terminated and the most relevant class label is reported. The overall exploration process also provides the user with a good diagnostic idea of how the local data distributions along different dimensions relate to the class label.

## 6.11 Conclusions and Summary

In this chapter, we presented algorithms for instance-based learning and lazy-learning. These methods are usually computationally more expensive than traditional models, but have the advantage of using information about the test instance at the time of model construction. In many scenarios, such methods can provide more accurate results, when a pre-processed model cannot fully capture the underlying complexities of the data. The other advantage of instance-based methods is that they are typically very simple and easy to implement for arbitrary data types, because the complexity is usually abstracted in determining an appropriate distance function between objects. Since distance function design has been widely studied in the literature for different data types, this allows the use of this methodology for arbitrary data types. Furthermore, existing model-based algorithms can be generalized to local variations in order to transform them to instance-learning methods. Such methods have great diagnostic value for specific test instances, since the model is constructed local to the specific test instance, and also provides knowledge to the analyst that is test-instance specific. Lazy methods are highly flexible and can be generalized to streaming and other temporal scenarios, where the laziness of the approach can be used in order to learn the appropriate temporal horizon, in which lazy learning should be performed.

## Bibliography

[1] A. Aamodt and E. Plaza. Case-based reasoning: Foundational issues, methodological variations, and system approaches, *AI communications*, 7(1):39–59, 1994.

[2] C. Aggarwal, A. Hinneburg, and D. Keim. On the surprising behavior of distance metrics in high dimensional space, *Data Theory—ICDT Conference*, 2001; *Lecture Notes in Computer Science*, 1973:420–434, 2001.

[3] C. Aggarwal. Towards systematic design of distance functions for data mining applications, *Proceedings of the KDD Conference*, pages 9–18, 2003.

[4] C. Aggarwal and P. Yu. Locust: An online analytical processing framework for high dimensional classification of data streams, *Proceedings of the IEEE International Conference on Data Engineering*, pages 426–435, 2008.

[5] C. Aggarwal and C. Reddy. *Data Clustering: Algorithms and Applications*, CRC Press, 2013.

[6] C. Aggarwal. Toward exploratory test-instance-centered diagnosis in high-dimensional classification, *IEEE Transactions on Knowledge and Data Engineering*, 19(8):1001–1015, 2007.

[7] C. Aggarwal, J. Han, J. Wang, and P. Yu. A framework for on demand classification of evolving data streams. In *IEEE TKDE Journal*, 18(5):577–589, 2006.

[8] D. Aha, P. Clark, S. Salzberg, and G. Blix. Incremental constructive induction: An instance-based approach, *Proceedings of the Eighth International Workshop on Machine Learning*, pages 117–121, 1991.

[9] D. Aha. *Lazy learning*. Kluwer Academic Publishers, 1997.

[10] D. Aha. Tolerating noisy, irrelevant and novel attributes in instance-based learning algorithms, *International Journal of Man-Machine Studies*, 36(2):267–287, 1992.

[11] D. Aha, D. Kibler, and M. Albert. Instance-based learning algorithms, *Machine Learning*, 6(1):37–66, 1991.

[12] D. Aha. Lazy learning: Special issue editorial, *Artificial Intelligence Review*, 11:7–10, 1997.

[13] F. Angiulli. Fast nearest neighbor condensation for large data sets classification, *IEEE Transactions on Knowledge and Data Engineering*, 19(11):1450–1464, 2007.

[14] M. Ankerst, G. Kastenmuller, H.-P. Kriegel, and T. Seidl. Nearest Neighbor Classification in 3D Protein Databases, *ISMB-99 Proceedings*, pages 34–43, 1999.

[15] C. Atkeson, A. Moore, and S. Schaal. Locally weighted learning, *Artificial Intelligence Review*, 11(1–5):11–73, 1997.

[16] S. D. Bay. Combining nearest neighbor classifiers through multiple feature subsets. *Proceedings of ICML Conference*, pages 37–45, 1998.

[17] J. Beringer and E Hullermeier. Efficient instance-based learning on data streams, *Intelligent Data Analysis*, 11(6):627–650, 2007.

[18] M. Birattari, G. Bontempi, and M. Bersini. Lazy learning meets the recursive least squares algorithm, *Advances in neural information processing systems*, 11:375–381, 1999.
