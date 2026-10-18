In the second step, for each test object yj with feature vector (yj1,yj2,…,yjd) in Test_D, M(yj1,yj2,…,yjd) yields a probability distribution Pj of class labels for yj. We then assign yj the class label, say, c0, whose probability is the highest, i.e., c0 = argmaxc∈C{Pj(c)}.

The two common measures of a classifier M are:

+   - Accuracy: M should be highly accurate in its prediction of labels for Train_D. For example, M should have a high percentage of test tuples predicted correctly on Train_D, compared with the ground truth. To achieve a high accuracy, a classifier should be designed to avoid underfit or overfit problems.

+   - Performance: M should be efficient, i.e., the computational cost should be low. Its performance should also scale with the database size.

As discussed before, although AVG is efficient, it has a low accuracy. On the other hand, PW has a higher accuracy, but is extremely inefficient. We next examine several algorithms that are designed to satisfy both of these requirements.

# 16.3 Classification Algorithms

We now describe several important classification algorithms that are designed to handle uncertain data:

+   - Decision trees (Section 16.3.1);

+   - Rule-based classification (Section 16.3.2);

+   - Associative classification (Section 16.3.3);

+   - Density-based classification (Section 16.3.4);

+   - Nearest-neighbor-based classification (Section 16.3.5);

+   - Support vector classification (Section 16.3.6); and

+   - Naive Bayes classification (Section 16.3.7).

The above algorithms are derived from the classical solutions that classify exact data. For each algorithm, we will discuss its framework, and how it handles uncertain data efficiently.

# 16.3.1 Decision Trees

Overview: Decision tree classification is a well-studied technique [27,28]. A decision tree is a tree-like structure that consists of internal nodes, leaf nodes, and branches. Each internal node of a decision tree represents a test on an unseen test tuple’s feature (attribute), while each leaf node represents a class or a probability distribution of classes. Using a decision tree, classification rules can be extracted easily. A decision tree is easy to understand and simple to use. Moreover, its construction does not require any domain knowledge or parameter values.

In traditional decision tree classification algorithms (e.g., ID3 and C4.5) [27,28], a feature (an attribute) of a tuple is either categorical or numerical. Its values are usually assumed to be certain. Recent works [23,24,32,33] have extended this technique to support uncertain data. Particularly, the authors in [32,33] studied the problem of constructing decision trees for binary classification on