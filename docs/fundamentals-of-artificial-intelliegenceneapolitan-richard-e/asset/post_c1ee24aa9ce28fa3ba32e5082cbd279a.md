
![](img/67fa924962ee21b3590be9f3b10d9fe7_413_0.png)

Figure 13.19 If our set of conditional independencies is {I_P(X, Y), I_P(W, {X, Y}|Z)}, then P is embedded faithfully in the DAGs in (a) and (b) but not in the DAGs in (c) and (d).

DAGs in Figure 13.19 (c) or 13.19 (d). The reason is that these latter DAGs entail I_P(X, W), and we do not have this conditional independency. That is, the Markov condition says X must be independent of its nondescendents conditional on its parents. Because X has no parents, this means that X must simply be independent of its nondescendents, and W is one of its nondescendents. If we make the causal embedded faithfulness assumption, we conclude that Z causes W.

Example 13.30 Recall that in Example 13.23, V = {X, Y, Z, W}, our set of conditional independencies was

```
{I_P(X, {Y, W}), I_P(Y, {X, Z}),
```

![](img/67fa924962ee21b3590be9f3b10d9fe7_414_0.png)

![](img/67fa924962ee21b3590be9f3b10d9fe7_414_1.png)

![](img/67fa924962ee21b3590be9f3b10d9fe7_414_2.png)

Figure 13.20 If our set of conditional independencies is {I_P(X, {Y, W}), I_P(Y, {X, Z})}, we can conclude that Z and W have a hidden common cause.

13.20 (c). P is also embedded faithfully in the DAG in Figure 13.20 (b). If we make the causal embedded faithfulness assumption, we conclude that Z and W have a hidden common cause.

## 13.6.3 Application: College Student Retention Rate

Next we show a real application of using the theory just discussed to learn causal influences. First, however, we review the edges in a causal graph.

When using a software package to learn causal influences, the graph learned has several different types of edges, with each indicating a different conclusion about the causal relationship between the variables connected by the edge. Different packages may denote these edges differently. Below is the notation used here.

| Edge | Causal Relationship |
|---|---|
| \( X - Y \) | \( X \) causes \( Y \) or (exclusive) \( Y \) causes \( X \); or \( X \) and \( Y \) have a hidden common cause. |
| \( X \rightarrow Y \) | \( X \) causes \( Y \) or \( X \) and \( Y \) have a hidden common cause; and \( Y \) does not cause \( X \). |
| \( X \dashrightarrow Y \) | \( X \) causes \( Y \). |
| \( X \leftrightarrow Y \) | \( X \) and \( Y \) have a hidden common cause. |

In the above, when we do not denote an “or” as exclusive, it is not exclusive. There is one additional restriction. If we have the chain \( X - Y - Z \), we cannot have two causal edges with their heads at node \( Y \). For example, we could not have node \( X \) causing node \( Y \) and nodes \( Y \) and \( Z \) having a hidden common cause.

The example now follows. Using the database collected by the U.S. News and World Report magazine for the purpose of college ranking, Druzdzel and Glymour [1999] analyzed the influences that affect university student retention rate. By “student retention rate” we mean the percent of entering freshmen who end up graduating from the university at which they initially matriculate. Low student retention rate is a major concern at many American universities, as the mean retention rate over all American universities is only 55%.

The database provided by the U.S. News and World Report magazine contains records for 204 U.S. universities and colleges identified as major research institutions. Each record consists of over 100 variables. The data were collected separately for the years 1992 and 1993. Druzdzel and Glymour [1999] selected the following eight variables as being most relevant to their study:

| Variable | What the Variable Represents |
|---|---|
| grad | Fraction of entering students who graduate from the institution |
| rejr | Fraction of applicants who are not offered admission |
| tstsc | Average standardized score of incoming students |
| tp10 | Fraction of incoming students in the top 10% in high school |
| acpt | Fraction of students who accept the institution's admission offer |
| spnd | Average educational and general expenses per student |
| sfrat | Student/faculty ratio |
| salar | Average faculty salary |

Druzdzel and Glymour [1999] used Tetrad II [Scheines et al., 1994] to learn causal influences from the data. Tetrad II allows the user to specify a temporal ordering of the variables. If variable \( Y \) precedes \( X \) in this order, the algorithm assumes there can be no path from \( X \) to \( Y \) in any DAG in which the probability distribution of the variables is embedded faithfully. It is called a temporal ordering because in applications to causality if \( Y \) precedes \( X \) in time, we would assume \( X \) could not cause \( Y \). Druzdzel and Glymour [1999] specified the following temporal ordering for the variables in this study:

![](img/67fa924962ee21b3590be9f3b10d9fe7_416_0.png)

![](img/67fa924962ee21b3590be9f3b10d9fe7_416_1.png)

![](img/67fa924962ee21b3590be9f3b10d9fe7_416_2.png)

![](img/67fa924962ee21b3590be9f3b10d9fe7_416_3.png)

Figure 13.21 The graphs Tetrad II learned from U.S. News and World Report's 1992 database.

```
spnd, sfrat, salar
rejr, acpt
tstsc, tp10
grad
```

Their reasons for this ordering are as follows: They believed the average spending per student (`spnd`), the student/teacher ratio (`sfrat`), and the faculty salary (`salar`) are determined based on budget considerations and are not influenced by any of the other five variables. Furthermore, they placed rejection rate (`rejr`) and the fraction of students who accept the institution's admission offer (`acpt`) ahead of average test scores (`tstsc`) and class standing (`tp10`) because the values of these latter two variables are only obtained from matriculating students. Finally, they assumed the graduate rate (`grad`) does not cause any of the other variables.

Tetrad II allows the user to enter a significance level. A significance level of \(\alpha\) means the probability of rejecting a conditional independency hypothesis, when it is true, is \(\alpha\). Therefore, the smaller the value of \(\alpha\) is, the less likely we are to reject a conditional independency, and therefore the sparser our resultant graph. Figure 13.21 shows the graphs which Druzdzel and Glymour [1999] learned from the 1992 database, provided by U.S. News and World Report, using significance levels of .2, .1, .05, and .01.

Although different graphs were obtained at different levels of significance, all the graphs in Figure 13.21 show that the average standardized test score (`tstsc`) has a direct causal influence on graduation rate (`grad`), and no other variable has a direct causal influence on `grad`. The results for the 1993 database were not as overwhelming, but they too indicated `tstsc` to be the only direct causal influence of `grad`.

To test whether the causal structure may be different for top research universities, Druzdzel and Glymour [1999] repeated the study using only the top 50 universities according to the ranking of U.S. News and World Report. The results were similar to those for the complete database.

These results indicate that although factors such as spending per student and faculty salary may have an influence on graduation rates, they do so only indirectly by affecting the standardized test scores of matriculating students. If the results correctly model reality, retention rates can be improved by bringing in students with higher test scores in any way whatsoever. Indeed, in 1994, Carnegie Mellon changed its financial aid policies to assign a portion of its scholarship fund on the basis of academic merit. Druzdzel and Glymour [1999] noted that this resulted in an increase in the average test scores of matriculating freshman classes and an increase in freshman retention.

## 13.7 Class Probability Trees

Recall that Bayesian networks represent a large joint distribution of random variables succinctly. Furthermore, we can use a Bayesian network to compute the conditional probability of any variable(s) of interest given values of some
