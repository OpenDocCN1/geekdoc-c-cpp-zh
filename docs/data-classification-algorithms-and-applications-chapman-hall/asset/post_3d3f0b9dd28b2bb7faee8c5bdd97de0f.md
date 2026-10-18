
# TABLE 19.10: Ensemble Output by Bagging

| x | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| y | +1 | +1 | +1 | +1 | -1 | -1 | -1 | +1 | +1 | +1 |

and LeftChildNode and RightChildNode are the child nodes of the current node. We are trying to find a feature q* to maximize i(node) − P_L · i(LeftChildNode) − P_R · i(RightChildNode), where P_L and P_R are the fraction of the data that go to the corresponding child node if the split feature q* is applied. We can use one of the following impurity measures: a) Entropy: i(node) = − Σ_{y_i ∈ Y} p(y_i) log p(y_i); b) Gini index: i(node) = 1 − Σ_{y_i ∈ Y} p(y_i)^2; c) misclassification rate: i(node) = 1 − max_{y_i ∈ Y} p(y_i).

- After we select the splitting feature, we will split the data at the current node v into two parts and assign them to its child nodes LeftChildNode and RightChildNode. We denote these two datasets as D_L and D_R. Label v is the parent node of LeftChildNode and RightChildNode under the split feature q*.

- Call the function LearnDecisionTree(D_L, iteration = iteration + 1, ParentNode = v) and LearnDecisionTree(D_R, iteration = iteration + 1, ParentNode = v) to continue the tree construction.

Random Forest algorithm builds multiple decision trees following the above procedure and takes majority voting of the prediction results of these trees. The algorithm is summarized in Algorithm 19.4. To incorporate diversity into the trees, Random Forest approach differs from the traditional decision tree algorithm in the following aspects when building each tree: First, it infers the tree from a Bootstrap sample of the original training set. Second, when selecting the best feature at each node, Random Forest only considers a subset of the feature space. These two modifications of decision tree introduce randomness into the tree learning process, and thus increase the diversity of base classifiers. In practice, the dimensionality of the selected feature subspace n′ controls the randomness. If we set n′ = n where n is the original dimensionality, then the constructed decision tree is the same as the traditional deterministic one. If we set n′ = 1, at each node, only one feature will be randomly selected to split the data, which leads to a completely random decision tree. In [13], it was suggested that n′ could be set as the logarithm of the dimensionality of original feature space, i.e., n′ = log(n).

Note that although the subset of feature space is randomly selected, the choice of the feature used to split a node is still deterministic. In [56], the authors introduce the VR-tree ensemble method, which further randomizes the selection of features to split nodes. At each node, a Boolean indicator variable is adopted: If the indicator variable is true, the node will be constructed in the deterministic way, i.e., among all possible features, we select the one that achieves the biggest impurity gain; if the indicator variable is false, a feature will be randomly selected to split the node. If the feature space is large, this will benefit the learning process by reducing the computation cost and increasing the diversity among all decision trees.

In practice, Random Forest is simple yet powerful. The diversity among the trees ensures good performance of Random Forest. By tuning the subspace dimensionality n′, different tradeoffs between computation resources and diversity degrees can be achieved. The decision tree building process can be implemented in parallel to reduce running time. There are other variations of Random Forest approaches that have been demonstrated to be effective in density estimation [31,55] and anomaly detection [57].

## Algorithm 19.4 Random Forest

```
**Input:** Training data \(\mathcal{D}=\{(\mathbf{x}_i,y_i)\}_{i=1}^m\) \((\mathbf{x}_i\in\mathbb{R}^n, y_i\in\mathcal{Y})\)  
**Output:** An ensemble classifier \(H\)  

1. **for** \(t\leftarrow 1\) **to** \(T\) **do**  
2. Construct a sample data set \(\mathcal{D}_t\) by randomly sampling with replacement in \(\mathcal{D}\)  
3. Learn a decision tree \(h_t\) by applying  
   \(\mathit{LearnDecisionTree}(\mathcal{D}_t,\mathit{iteration}=0,\mathit{ParentNode}=\mathit{root})\):  
4. If stop criterion is satisfied, return  
5. Randomly sample features in the whole feature space \(\mathbb{R}^n\) to get a new data set  
   \(\widehat{\mathcal{D}}_{current}=\mathit{RandomSubset}(\mathcal{D}_{current})\)  
6. Find the best feature \(q^*\) according to impurity gain  
7. Split data \((\mathcal{D}_L,\mathcal{D}_R)=\mathit{split}(\mathcal{D}_{current},q^*)\)  
8. Label the new parent node \(v=\mathit{parent.newchild}(q^*)\)  
9. Conduct \(\mathit{LearnDecisionTree}(\mathcal{D}_L,\mathit{iteration}=\mathit{iteration}+1,\mathit{ParentNode}=v)\) and  
   \(\mathit{LearnDecisionTree}(\mathcal{D}_R,\mathit{iteration}=\mathit{iteration}+1,\mathit{ParentNode}=v)\)  
10. **end for**  
11. **return** \(H(\mathbf{x})=\arg\max_{y\in\mathcal{Y}}\sum_{t=1}^{T}\mathbf{1}(h_t(\mathbf{x})=y)\)
```

## 19.4 Boosting

Boosting is a widely used ensemble approach, which can effectively boost a set of weak classifiers to a strong classifier by iteratively adjusting the importance of examples in the training set and learning base classifiers based on the weight distribution. In this section, we review the general procedure of Boosting and its representative approach: AdaBoost.

### 19.4.1 General Boosting Procedure

We wish to learn a strong classifier that has good generalization performance, but this is a difficult task. In contrast, weak classifiers, which have performance only comparable to random guessing, are much easier to obtain. Therefore, people wonder if it is possible to use a set of weak classifiers to create a single strong classifier [48]. More formally speaking, are weakly learnable and strongly learnable equivalent? In [69], it was proved that the answer to this question is yes, and this motivates the development of Boosting.

Boosting is a family of algorithms that could convert weak classifiers to a strong one [70]. The basic idea of Boosting is to correct the mistakes made in weak classifiers gradually. Let’s consider a binary classification task, in which the training set only has three examples, **x₁**, **x₂**, and **x₃**. Boosting starts with a base classifier, say \(h_1\). Suppose \(h_1\) makes correct predictions on **x₁** and **x₂**, but predicts wrongly on **x₃**. (Note that in this binary classification task, we can always find base classifiers with \(\frac{1}{3}\) error rate. If the error rate of some weak classifier is \(\frac{2}{3}\), by simply flipping, we can get base classifiers with \(\frac{1}{3}\) error rate.) From \(h_1\), we can derive a weight distribution for training examples to make the wrongly-classified examples more important. In this example, as \(h_1\) makes an error with **x₃**, the weight distribution will assign a higher value to **x₃**. Based on this weight distribution, we train another classifier, say \(h_2\). Now suppose \(h_2\) misclassifies **x₂** and the weight distribution will be adjusted again: The weight for **x₂** is increased while **x₃**’s weight is decreased and **x₁** has the lowest weight. According to the updated weight distribution, another classifier \(h_3\) is obtained. By combing \(h_1\), \(h_2\) and \(h_3\), we can get a strong classifier that makes correct predictions for all the three training examples.

## Algorithm 19.5 Boosting Algorithm

**Input:** Training data \(\mathcal{D}=\{(x_i,y_i)\}_{i=1}^{m}\), \(x_i\in\mathbb{R}^n\), \(y_i\in\{+1,-1\}\)

**Output:** An ensemble classifier \(H\)

```
1: Initialize the weight distribution \(W_1\)
2: **for** \(t\leftarrow 1\) **to** \(T\) **do**
3:     Learn weak classifier \(h_t\) based on \(\mathcal{D}\) and \(W_t\)
4:     Evaluate weak classifier \(\epsilon(h_t)\)
5:     Update weight distribution \(W_{t+1}\) based on \(\epsilon(h_t)\)
6: **end for**
7: **return** \(H=Combination(\{h_1,\ldots,h_T\})\)
```

As summarized in Algorithm 19.5, Boosting approaches learn different weak classifiers iteratively by adjusting the weight of each training example. During each round, the weight of misclassified data will be increased and base classifiers will focus on those misclassified ones more and more. Under this general framework, many Boosting approaches have been developed, including AdaBoost [34], LPBoost [6], BrownBoost [32] and LogitBoost [71]. In the following, we will discuss the most widely used Boosting approach, Adaboost, in more detail.

### 19.4.2 AdaBoost

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
