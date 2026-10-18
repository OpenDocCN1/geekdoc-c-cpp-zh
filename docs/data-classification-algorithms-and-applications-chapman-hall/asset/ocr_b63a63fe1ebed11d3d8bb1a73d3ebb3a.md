# Algorithm 19.5 Boosting Algorithm

**Input:** Training data \(\mathcal{D}=\{(x_i,y_i)\}_{i=1}^{m}\), \(x_i\in\mathbb{R}^n\), \(y_i\in\{+1,-1\}\)

**Output:** An ensemble classifier \(H\)

```
1: Initialize the weight distribution \(W_1\)
2: **for** \(t\leftarrow 1\) **to** \(T\) **do**
3: &nbsp;&nbsp;&nbsp;&nbsp;Learn weak classifier \(h_t\) based on \(\mathcal{D}\) and \(W_t\)
4: &nbsp;&nbsp;&nbsp;&nbsp;Evaluate weak classifier \(\epsilon(h_t)\)
5: &nbsp;&nbsp;&nbsp;&nbsp;Update weight distribution \(W_{t+1}\) based on \(\epsilon(h_t)\)
6: **end for**
7: **return** \(H=Combination(\{h_1,\ldots,h_T\})\)
```

As summarized in Algorithm 19.5, Boosting approaches learn different weak classifiers iteratively by adjusting the weight of each training example. During each round, the weight of misclassified data will be increased and base classifiers will focus on those misclassified ones more and more. Under this general framework, many Boosting approaches have been developed, including AdaBoost [34], LPBoost [6], BrownBoost [32] and LogitBoost [71]. In the following, we will discuss the most widely used Boosting approach, Adaboost, in more detail.

# 19.4.2  AdaBoost

We will first describe AdaBoost in the context of binary classification. Given a training set \(\mathcal{D}=\{(x_i,y_i)\}_{i=1}^{m}\), \(x_i\in\mathbb{R}^n\), \(y_i\in\{+1,-1\}\), our goal is to learn a classifier that could classify unseen data with high accuracy. AdaBoost [34, 66] derives an ensemble model \(H\) by combining different weak classifiers. During the training process, the weight of each training example is adjusted based on the learning performance in the previous round, and then the adjusted weight distribution will be fed into the next round. This is equivalent to inferring classifiers from training data that are sampled from the original data set based on the weight distribution.

The detailed procedure of AdaBoost is discussed as follows. At first, the weight distribution \(W\) is initialized as \(W_1(i)=\frac{1}{m}\), i.e., we initialize \(W_1\) by uniform distribution when no prior knowledge is provided. We learn a base classifier \(h_t\) at each iteration \(t\), given the training data \(\mathcal{D}\) and weight distribution \(W_t\). Among all possible \(h\in\mathcal{H}\), we choose the best one that has the lowest classification error. In binary classification (\(\mathcal{Y}=\{+1,-1\}\)), if a classifier \(h\) has worse performance than random guessing (error rate \(\epsilon(h)\geq 0.5\)), by simply flipping the output, we can turn \(h\) into a good classifier with a training error \(1-\epsilon(h)\). In this scenario, choosing the best classifier is equivalent to picking either the best or worst one by considering all \(h\in\mathcal{H}\). Without loss of generality, we assume that all the base classifiers have better performance compared with random guessing, i.e., \(\epsilon(h)\leq 0.5\). At each round, we pick the best model that minimizes the training error.

AdaBoost algorithm adopts weighted voting strategy to combine base classifiers. We derive a base classifier \(h_t\) at iteration \(t\) and calculate its weight in combination as

\[
\alpha_t=\frac{1}{2}\ln\frac{1-\epsilon(h_t)}{\epsilon(h_t)},
\]

which is computed according its training error. This weight assignment has the following properties: 1) if \(\epsilon(h_1)\leq\epsilon(h_2)\), then we have \(\alpha_{h_1}\geq\alpha_{h_2}\), i.e., a higher weight will be assigned to the classifier with smaller training error; and 2) as \(\epsilon(h_t)\leq 0.5\), \(\alpha_t\) is always positive.

An important step in each round of AdaBoost is to update the weight distribution of training examples based on the current base classifier according to the update equation

\[
W_{t+1}(i)=\frac{W_t(i)\exp\{-\alpha_t\cdot h_t(x_i)y_i\}}{Z_t},
\]