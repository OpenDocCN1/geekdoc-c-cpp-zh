# Data Clustering: Algorithms and Applications

2.2.4.1 Challenges and Opportunities

2.2.4.2 LUFS: An Unsupervised Selection Framework for Linked Data

2.2.4.3 Conclusion and Future Work for Linked Data

2.3 Discussions and Challenges

2.3.1 The Chicken or the Egg Dilemma

2.3.2 Model Selection: K and l

2.3.3 Scalability

2.3.4 Stability

Bibliography

# 2. Introduction

The growth of high-throughput technologies nowadays leads to exponential growth in the harvested data with respect to dimensionality and sample size. As a consequence, storing and processing these datasets becomes Challenging. Figure (2.1) shows the trend of this growth for UCI Machine Learning Repository. This augmentation made manual processing of these datasets either impossible or impractical. Therefore, data mining and machine learning tools are required to automate pattern recognition and knowledge discovery process. However the high level of noise associated with collected samples. Usually, noise is either due to noise in the collected data or to the source of this data. For instance, in medical images, this kind of noise is caused by the device effect. On the other hand, text datasets from the Internet are noisy by nature because they are usually informally written and suffer from grammatical mistakes, misspelling, and improper punctuation. Undoubtedly, extracting useful knowledge from high and noisy datasets is a painful task.

Dimensionality reduction is one popular technique to reduce noise (i.e., irrelevant) and redundant attributes (aka features). Dimensionality reduction techniques can be categorized into many types: feature extraction and feature selection. In the feature extraction approach, features are projected into a new space with lower dimensionality. Examples of the feature extraction technique include Principal Component Analysis (PCA), Linear Discriminant Analysis (LDA), and Singular Value Decomposition (SVD), to name a few. On the other hand, the feature selection approach aims to select a subset of features that minimize redundancy and maximize relevance to the target (i.e., class label). Popular feature selection techniques include Information Gain, Relief, Chi Squares, Fisher Score, and Lasso, to name a few.

Both dimensionality reduction approaches are capable of improving performance, lowering computational complexity, building better generizable models, and increasing robustness. However, feature selection is superior in terms of better readability and interpretability because it maintains the original feature values in the reduced space, while feature extraction transforms the data from the original space into a new space with lower dimensionality, which cannot be linked to the features in the original space. Therefore, there is no physical meaning for the transformed features from the feature extraction technique.

Feature selection is broadly categorized into four models: filter model, wrapper model, embedded model, and hybrid model. As mentioned above, feature selection subsets of highly discriminant features. In other words, it selects features that are capable of discriminating samples that belong to different classes. Thus, we need to have labeled samples as training samples in order