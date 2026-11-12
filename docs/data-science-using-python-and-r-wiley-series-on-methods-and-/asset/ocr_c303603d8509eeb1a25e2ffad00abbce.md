# TABLE 10.1 Mean variable value, by cluster, for the white_wine_training data sets

| Variable | Cluster 1: 712 wines "Sweet Wines" | Cluster 2: 1097 wines "Dry Wines" |
| :--- | :--- | :--- |
| Sugar_z | 0.96 | -0.62 |
| Alcohol_z | -0.76 | 0.49 |

The Python results in Figure 10.2 were copied here in Table 10.1

the k-means clustering algorithm to the predictor variables alcohol and sugar. Python was used. Table 10.1 shows the mean variable value for each predictor, for the two resulting clusters. Cluster 1 contains 712 wines, with a mean sugar content 0.96 standard deviations above the overall mean sugar content for all the white wines in the training data set. (That is, the mean Cluster 1 value for the standard normal sugar_z variable is 0.96.) Cluster 1's mean alcohol content, however, lies 0.76 standard deviations below the mean alcohol level for all wines. On the other hand, Cluster 2 contains 1097 wines, with lower mean sugar content than Cluster 1 (0.62 standard deviations below the overall mean) but with higher alcohol content, at 0.49 standard deviations above the overall mean.

So, we may identify Cluster 1 as containing “Sweet Wines,” high in sugar but low in alcohol, while Cluster 2 contains “Dry Wines,” low in sugar but packing a higher alcoholic punch. Perhaps, the most important cluster validation method is to obtain clusters that make sense to a subject matter expert. A quick Internet search shows how we obtain these different wines in the real world. “During fermentation, yeasts transform sugars ... into ethanol [alcohol]....” So, it is no surprise that our clustering algorithm has uncovered these two “natural” clusters of white wines: sweet wines and dry wines. The dry wines have, on the whole, evidently undergone longer fermentation than the sweet wines.

# 10.4 CLUSTER VALIDATION

Cluster solutions should be validated. Since no predictions were made using the training data set, we simply reapply the k-means algorithm, this time to the white_wine_test data set, and compare the results obtained with the training set. Table 10.2

# TABLE 10.2 Mean variable value, by cluster, for the white_wine_test data sets

| Variable | Cluster 1: 638 wines "Sweet Wines" | Cluster 2: 1122 wines "Dry Wines" |
| :--- | :--- | :--- |
| Sugar_z | 1.07 | -0.61 |
| Alcohol_z | -0.80 | 0.46 |

The Python results in Figure 10.3 are used for this table. The cluster labels “Cluster 1” and “Cluster 2” were reversed, for ease of interpretation. These cluster labels are arbitrarily assigned by the algorithm