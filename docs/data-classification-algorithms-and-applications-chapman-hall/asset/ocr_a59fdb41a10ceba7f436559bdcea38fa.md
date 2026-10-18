| Age | Hard | No | Soft |
|---|---:|---:|---:|
| 8 | 1 | 1 | 0 |
| 11 | 0 | 1 | 0 |
| 13 | 0 | 1 | 0 |
| 14 | 0 | 1 | 0 |
| 16 | 1 | 0 | 0 |
| 18 | 0 | 0 | 2 |
| 23 | 1 | 1 | 0 |
| 26 | 0 | 1 | 0 |
| 32 | 0 | 1 | 0 |
| 35 | 0 | 1 | 1 |
| 36 | 0 | 0 | 1 |
| 39 | 0 | 1 | 0 |
| 44 | 0 | 0 | 1 |
| 46 | 0 | 1 | 0 |
| 47 | 0 | 1 | 0 |
| 51 | 1 | 0 | 0 |
| 52 | 0 | 1 | 0 |
| 55 | 0 | 1 | 0 |
| 63 | 0 | 1 | 0 |
| 64 | 0 | 1 | 0 |

(a) AVC Table for Age Attribute (RainForest)

| Near/Far | Hard | No | Soft |
|---|---:|---:|---:|
| Far | 1 | 8 | 3 |
| Near | 3 | 7 | 2 |

| Tears | Hard | No | Soft |
|---|---:|---:|---:|
| Normal | 4 | 3 | 5 |
| Reduced | 0 | 12 | 0 |

| Astigmatism | Hard | No | Soft |
|---|---:|---:|---:|
| No | 0 | 7 | 5 |
| Yes | 4 | 8 | 0 |

(b) Other Three AVC Tables (RainForest and SPIES)

| Age | Hard | No | Soft |
|---|---:|---:|---:|
| 1-10 | 1 | 1 | 0 |
| 11-19 | 1 | 3 | 2 |
| 20-29 | 1 | 2 | 0 |
| 30-39 | 0 | 3 | 2 |
| 40-49 | 0 | 2 | 1 |
| 50-59 | 1 | 2 | 0 |
| 60-69 | 0 | 2 | 0 |

(c) Concise AVC Table for Age Attribute (SPIES)

# **FIGURE 4.4:** AVC tables for RainForest and SPIES.

# 4.4.2  SPIES Approach

In [39], a new approach, referred to as SPIES (Statistical Pruning of Intervals for Enhanced Scalability), is developed to make decision tree construction more memory and communication efficient. The algorithm is presented in the procedure *SPIES-Classifier* (Figure 4.2). The SPIES method is based on AVC groups, like the RainForest approach. The key difference is in how the numerical attributes are handled. In SPIES, the AVC group for a node is comprised of three subgroups:

*Small AVC group:* This is primarily comprised of AVC sets for all categorical attributes. Since the number of distinct elements for a categorical attribute is usually not very large, the size of these AVC sets is small. In addition, SPIES also adds the AVC sets for numerical attributes that only have a small number of distinct elements. These are built and treated in the same fashion as in the RainForest approach.

*Concise AVC group:* The range of numerical attributes that have a large number of distinct elements in the dataset is divided into *intervals*. The number of intervals and how the intervals are constructed are important parameters to the algorithm. The original SPIES implementation uses equal-width intervals. The concise AVC group records the class histogram (i.e., the frequency of occurrence of each class) for each interval.

*Partial AVC group:* Based upon the concise AVC group, the algorithm computes a subset of the values in the range of the numerical attributes that are likely to contain the split point. The partial AVC group stores the class histogram for the points in the range of a numerical attribute that has been determined to be a candidate for being the split condition.

SPIES uses two passes to efficiently construct the above AVC groups. The first pass is a quick *Sampling Step*. Here, a sample from the dataset is used to estimate small AVC groups and concise