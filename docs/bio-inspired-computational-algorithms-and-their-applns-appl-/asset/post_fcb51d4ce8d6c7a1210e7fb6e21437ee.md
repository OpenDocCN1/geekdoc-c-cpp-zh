
For the crossover operator, an operator based on mask crossover [9] is applied, which selects, through the tournament method, two parent individuals, randomly chooses the chromosome of one parent to be used as "crossover mask of the selected individual". The crossing is done by analyzing the chromosome of both parents. If both chromosomes have at least one function node (node 0), the chosen father mask is placed, but if we find documents in the chromosomes of both parents, then the father "not elected" document will be selected and we'll use it as pivot on the father "elected" (mask) to make the crossing that corresponds to the mentioned father, while interchanging the chromosomes of the mentioned father. This creates a new individual, and ensures that in the given chromosome set there are the same structural characteristics of the parents but we only incorporate it in the population if the child has a better fitness than their parents (see figure 5).

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_139_0.png)

Fig. 5. Crossover operator (crossover mask)

## 3.3 Selection

After we evaluate population's fitness, the next step is chromosome selection. Selection embodies the principle of 'survival of the fittest' [5]. Satisfied fitness chromosomes are selected for reproduction, for this, we apply the method of selection of the tournament, using a tournament of 2, and we apply Elitism in each generation [2].

## 4. Parameter control

For its size, and the influence that small changes have on the behavior of the GA during the experiments [1], the choice of parameter values that are going to be used appears as a critical factor. For their election we paid attention to the variation of the GA performance indicators when the value of any of these was changed, specifically the evolution of the successes and the evolution of 'fitness'. Therefore, these parameters are very important parts as they directly influence the performance of the GA [13]. These parameters can be treated independently, but the overall performance of the algorithm does not depend exclusively on a single parameter but on a combination of all parameters. Many researchers pay more attention to some parameters than others, but most agree that the parameters that should be under control are: selection schemes, population size, genetic variation operators and rates of their changes.

Because GA have several parameters that must be carefully chosen to obtain a good performance and avoid premature convergence, in our case and after much testing, we opted for the control of parameters, and some strategies such as:

To control the population size we use the strategy called GAVAPS (Genetic variation in population size) proposed by Michalewicz [9] using the concept of age and lifetime. When creating the first generation all individuals are assigned a zero age, referring to the birth of the individual, and every time a new generation is born the age of each individual increases by one. At the same time an individual is born, it is assigned a lifetime, which represents how long it will live within. Therefore, the individual will die when it reaches the given age. The lifetime of each individual depends on the value of its fitness compared to the average of the entire population. Thus, if an individual has better fitness, it will have more time to live, giving it greater ability to generate new individuals with their features. In our case, we allow each generation to generate new individuals with similar characteristics with this strategy.

Therefore, we adopt this approach essentially for the best individuals from each generation, and apply it to maintain elitism in the following generations, thus ensuring optimum intensification of available space, while keeping them during their lifetime [9]. However, to ensure diversity we randomly generate the remaining individuals in each generation. This way, we explore many different regions of the search space and allow for balance between intensification and diversity of feasible regions.

In all cases, the population size has been set at 50 individuals for the experiments conducted with samples following the suggestion of [1], which advises working with a population size between l and 2l in most practical applications (the length of chromosome l). In our case, "l", the length of our chromosome, is always equal to:

2 * number of documents to cluster -1.

On the other hand, we use two measures of fitness function to calculate the distance and similarity between documents and to be able to form better clusters (see table 1).

Table 1. Measures of the Function

| Measure | Formula |
|---|---|
| Euclidean distance | $d_y = \sqrt{\sum_{i=1}^n (x_i - x_j)^2}$ |
| Pearson correlation coefficient (Similarity) | $r = \frac{1}{n} \sum \left( \frac{x_i - \bar{x}}{\sigma_{x_i}} \right) \left( \frac{x_j - \bar{x}}{\sigma_{x_j}} \right)$ |
| Global Fitness | $\min \left( \alpha \, \text{Distance(Documents } i) + (1 - \alpha) \left(1 / \text{Similarity(Documents } i)\right) \right)$ |

with $x_i$ and $x_j$ the characteristic vectors of the documents that we are grouping, “μ” the number of examples and $\sigma_i$, $\sigma_j$ are the standard deviations of $x_i$ and $x_j$ and where: α is the parameter that adjusts the distance and similarity. The fitness function is used to minimize the distance between the documents and maximize the similarity between them.

Therefore, for the experiments with our experimental environment, we used samples of documents “very few (20), few (50), many (80) and enough (150)” documents with the requirement that they belonged only to two categories of Reuters collections or Editorials. Each of the samples was processed with five different seeds, and each of the results was compared with the method “K-means.” Then, each experiment was repeated by varying the rate of probability of genetic algorithm operators, using all the parameters shown in table 2 up to find that value of α that best fits the two metrics that are combined in our fitness function.

Table 2. Parameters taken into consideration for the Genetic algorithm with composite function

| Parameters | Values |
|---|---|
| Population size (tree number) | 50 |
| Número de evaluaciones (Generaciones) | 5000 maximum |
| Tournament size | 2 |
| Mutation Probability (Pm) | 0.01, 0.03, 0.05, 0.07, 0.1, 0.3, 0.5, 0.7 |
| Crossover Probability (Pc) | 0.70, 0.75, 0.80, 0.85, 0.90, 0.95 |
| Document quantity | Very Few, Few, Many, Enough |
| α coefficients | 0.85 (best value found) |
| Depth Threshold | 7/10 |

### 4.1 Studies to determine the value of α in the GA

We use the Reuters 21 distribution because it has greater dispersion across its documents and apply the GA varying the value of α in each of the tests with the usual parameters, always trying to test the effectiveness of the GA. We analyzed the relationship between fitness and the value of α using the values in table 2 (the results are shown in table 3 and figure 6).

In Figure 6, we can see that there is an increased dispersion of fitness values over 0.85, due to the increased contribution of Euclidean distance, which makes fitness insensitive for finding the clusters. The results suggest that a value of α close to 0.85 provides better results because it gives us more effectiveness in terms of number of hits, and a better fitness of the algorithm. This was corroborated with other distributions.

Table 3. Results of tests with GA, taking different samples of documents with the distribution 21 of the Reuters collection, to determine the best value for α

| Documents | α | Generation | Best Fitness | Average Middle Fitness | Hits | Effectiveness (%) |
|---|---|---|---|---|---|---|
| 20 | 0.75 | 1436 | 0.25291551 | 0.46849675 | 15 | 75.0 |
| 20 | 0.80 | 1592 | 0.20298477 | 0.47206890 | 16 | 80.0 |
| 20 | 0.85 | 2050 | 0.15255487 | 0.24504483 | 17 | 85.0 |
| 20 | 0.90 | 3694 | 0.15266796 | 0.25909582 | 17 | 85.0 |
| 20 | 0.95 | 1520 | 0.15319261 | 0.24568629 | 17 | 85.0 |
| 50 | 0.75 | 3476 | 0.25290429 | 0.28744261 | 35 | 70.0 |
| 50 | 0.80 | 3492 | 0.20285265 | 0.27862528 | 36 | 72.0 |
| 50 | 0.85 | 3355 | 0.15312467 | 0.29128428 | 36 | 72.0 |
| 50 | 0.90 | 2256 | 0.15318358 | 0.2837470 | 36 | 72.0 |
| 50 | 0.95 | 2222 | 0.15345986 | 0.27863789 | 36 | 72.0 |
| 80 | 0.75 | 3049 | 0.25704660 | 0.3681676 | 61 | 76.2 |
| 80 | 0.80 | 1371 | 0.20782096 | 0.3303315 | 61 | 76.2 |
| 80 | 0.85 | 2131 | 0.15784449 | 0.3447947 | 62 | 77.5 |
| 80 | 0.90 | 1649 | 0.15815252 | 0.32398087 | 62 | 77.5 |
| 80 | 0.95 | 2986 | 0.17796620 | 0.36008861 | 61 | 76.2 |
| 150 | 0.75 | 2279 | 0.26194273 | 0.29866150 | 91 | 60.6 |
| 150 | 0.80 | 1273 | 0.20636391 | 0.2293754 | 93 | 62.0 |
| 150 | 0.85 | 3257 | 0.15468809 | 0.27518240 | 94 | 62.6 |
| 150 | 0.90 | 1136 | 0.25482251 | 0.28218144 | 94 | 62.6 |
| 150 | 0.95 | 2452 | 0.25456480 | 0.26788158 | 91 | 60.6 |
| 250 | 0.75 | 3617 | 0.25754282 | 0.31144435 | 120 | 48.0 |
| 250 | 0.80 | 3274 | 0.20844638 | 0.2511289 | 121 | 48.4 |
| 250 | 0.85 | 3066 | 0.15805103 | 0.19299910 | 121 | 48.4 |
| 250 | 0.90 | 2343 | 0.20634355 | 0.20342140 | 121 | 48.4 |
| 250 | 0.95 | 2047 | 0.25541276 | 0.27844937 | 120 | 48.0 |

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_142_0.png)

Fig. 6. Best Fitness versus α values for different samples of documents of the Reuters Collection: Distribution 21
