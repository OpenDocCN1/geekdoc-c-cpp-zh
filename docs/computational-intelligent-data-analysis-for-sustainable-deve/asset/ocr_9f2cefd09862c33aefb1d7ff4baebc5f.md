$$D_{KL}(P_Y(y) \| P_Y(\hat{y})) = \sum_i P_Y(\hat{y}=i)\ln\frac{P_Y(y=i)}{P_Y(\hat{y}=i)} \tag{10.23}$$

For baseline comparison, we also developed a linear regression model that is used quite extensively in wind resource assessment [2, 8].

# 10.5 RESULTS AND DISCUSSION

In this section we present the results of comparing the described wind resource assessment techniques on data acquired from the rooftop anemometers at the Boston Museum of Science. We also examine the improvement in performance of each of the algorithms as more data are made available to each one in the forms of increasing training data from 3 to 6 to 8 months.

# 10.5.1 Comparison of Algorithms

First we compare algorithms when the same amount of data is available to each one of them for modeling. Results are presented in Figure 10.6 through Figure 10.8 for datasets $D_3$, $D_6$, and $D_8$, respectively. Each plot shows the KL distance between the ground truth distribution and the distribution estimated based on the predictions provided by each technique for the Year 2 dataset per bin. We plot the KL distance for all 12 bins.

We notice that the copula modeling technique consistently performs better than the other four techniques. The graphical model technique that assumes a naive variable dependency structure performs second best, although it demonstrates poor performance on the first bin. Its performance on this bin, however, improves as we increase the size of the dataset. One would expect the graphical model, which has a learned variable dependency structure, to outperform the one with naive assumptions. Here, except for the first bin, it does not. This may imply that a better structure learning algorithm is necessary, or that the one used needs further fine-tuning. The latter possibility is likely because the structure learning algorithm K2 only looks at a fraction of all possible structures when it references an order of the variables. A more robust structure learning algorithm that does not assume order could potentially yield improvements.

Linear regression is the worst performer of all, but performs well when 8 months of data are available. This is consistent with many studies in the