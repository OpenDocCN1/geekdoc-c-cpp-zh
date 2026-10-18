**TABLE 24.1:** Example of a Discrete Classifier $c$ for a Multi-Class Classification Problem.

| $x$ | $r(x)$ | $c(x)$ |
|---|---|---|
| $x_1$ | A | B |
| $x_2$ | B | B |
| $x_3$ | C | A |
| $x_4$ | A | A |
| $x_5$ | B | B |
| $x_6$ | B | B |
| $x_7$ | B | A |
| $x_8$ | A | C |
| $x_9$ | C | B |
| $x_{10}$ | A | A |

**Note:** In the second column, the real class $r(x)$ of the instance $x$ in the first column is given, while $c(x)$ in the third column denotes the class returned by $c$ for $x$.

# 24.3  Evaluation Measures

Once a validation scheme is chosen, the classifier can build its model on the training data and classify the test instances based on this model. Afterwards, evaluation measures are needed to describe how well this classification is done. We first discuss accuracy related measures that describe how similar the predicted classes of the test instances are to the real classes. Next, we consider additional measures that are needed for a good evaluation of the classifier.

# 24.3.1  Accuracy Related Measures

In this section we study how we can assess the quality of a given classifier based on a list of the real classes of instances and the predicted classes.

In the following we first consider discrete classifiers, for instance, K Nearest Neighbors, which return an actual class for each instance. The second type of classifiers, for instance Bayesian classifiers, are so-called probabilistic classifiers. Instead of returning a class they return the probability that they belong to a certain class. Both types of classifiers require different evaluation measures.

# 24.3.1.1  Discrete Classifiers

We consider a finite set $X = \{x_1, \ldots, x_n\}$ of $n$ instances, and for each instance $x \in X$ we know its real class $r(x)$ and the classification $c(x)$ returned by the classifier $c$. As $c$ is a discrete classifier, $c(x)$ takes values in the same set $C = c_1, \ldots, c_k$ of classes as the real classes $r(x)$. An example of a multi-class classification problem is given in Table 24.1 and an example of a binary classification problem is shown in Table 24.2. Note that we use the capitals $P$ and $N$ for the binary classification problems, referring to the positive and negative class, respectively, which is common use in binary classification problems.

A tool that is very useful when evaluating a discrete classifier is the so-called confusion matrix $M$. The dimension of the squared matrix $M$ is the number of classes, and the entry $M_{ij}$ denotes how many times an instance with real class $c_i$ was classified as $c_j$. The confusion matrix corresponding to the example in Table 24.1 (respectively, Table 24.2) is given in Table 24.3 (respectively, Table 24.4). In the binary case, we denote by True Positives (TP) and True Negatives (TN) the number of correctly classified positive and negative instances, respectively. False Negatives (FN) stands for the number of instances that are predicted negative but that are actually positive, while the False Positives (FP) are the number of instances that are falsely classified to the positive class.