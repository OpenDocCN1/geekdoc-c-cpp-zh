# 11.7.2 Application to the famous iris problem

The iris database is perhaps the best known database to be found in the pattern recognition literature. The data set contains 3 classes of 50 instances each, where each class refers to a type of iris plant. The vector of features consists of: sepal length in cm, sepal width in cm, petal length in cm, and petal width in cm. We consider three classes of patterns: Iris Setosa, Iris Versicolour and Iris Virginica. A confusion matrix for 500 learning iterations and two if-then rules has been shown in Table 11.4. Error rate is equal to 1.33%. The increase in the rule number did not cause the diminishing of the error rate.

|  | Iris Setosa | Iris Versicolour | Iris Virginica |
|---|---|---|---|
| Iris Setosa | 50 | 0 | 0 |
| Iris Versicolour | 0 | 50 | 0 |
| Iris Virginica | 0 | 2 | 48 |

Table 11.4 Simulation results for classification of the iris database

# 11.7.3 Application to wine recognition data

These databases are the results of a chemical analysis of wines grown in the same region in Italy but derived from three different cultivars. The analysis determined the quantities of 13 constituents found in each of the three types of wines. The data were collected by M. Forina. The data were used with many others for comparing various classifiers. The classes are separable, though only radial discriminant analysis has achieved 100% correct classification (RDA: 100%, QDA: 99.4%, LDA: 98.9%, 1NN: 96.1%). 500 learning iterations have been executed for the classifier described in Section 6. A confusion matrix for two and three if-then rules is presented in Table 11.5. Correct classifications equal to 99.43% and 100% have been obtained for two and three rules, respectively.

# 11.7.4 Application to MONKS problems

The MONK’s problem was the basis of the first international comparison of learning algorithms. The result of this comparison is summarized in [26]. One significant characteristic of this comparison is that it was performed by a collection of researchers, each of whom was an advocate of the technique they tested (often they were the authors of various methods).