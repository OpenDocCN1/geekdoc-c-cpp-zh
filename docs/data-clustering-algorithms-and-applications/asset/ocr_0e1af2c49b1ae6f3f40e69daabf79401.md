# Feature Selection for Clustering: A Review

53

# Algorithm 10 LUFS

**Input:** $\{X, R, \alpha, \beta, \lambda, c, K, k\}$
**Output:** $k$ most relevant features

+   1: Obtain the social dimension indicator matrix $H$
2: Set $F = H(H^T)^{-\frac{1}{2}}$
3: Construct $S$ through RBF kernel
4: Set $L = D - S$
5: Set $A = XLX^T + \alpha(I_n - FF^T)X^T$
6: Set $B = XX^T + \lambda I$
7: Set $t = 0$ and initialize $D_0$ as an identity matrix
8: while not convergent
9: Set $W_t = [q_1, \dots, q_c]$ where $q_1, \dots, q_c$ are the eigenvectors of $C_t$ corresponding to the first $c$ smallest eigenvalues
11: Update the diagonal $D_{t+1}$, where the $i$-th diagonal element is $\frac{1}{\|W_t(i,:)\|^2}$
12: Set $t = t + 1$
13: end
14: Sort each feature according to $\|W(i,:)\|_2$ in **descending** order and select the top-$k$ ranked ones;

data in an unsupervised scenario, and many works are needed to further exploit linked data for feature selection.
Since LUFS can be categorized as an embedded method, analogous to conventional data, how to develop filter, wrapper, and hybrid models for linked data is an interesting problem for future research. Furthermore, LUFS employs social dimension to capture link information, a further investigation into sophisticated methods of exploiting link will lead to novel approaches and help us develop a deeper understanding of how to improve the performance of feature selection. Finally the availability of various link formation can lead to links with heterogeneous strengths. Therefore how to incorporate atomic selection into feature selection is another promising direction for linked data.

# 2.3 Discussions and Challenges

Here are several challenges and concerns that we need to mention and discuss briefly in this chapter about feature selection for clustering.

# 2.3.1 The Chicken or the Egg Dilemma

In feature selection for clustering, there is a dilemma in which one to start with or which one serves the demands of the other. Do we utilize feature selection to improve clustering quality? Or, do we use clustering as an indicator of relevant features? In fact, this leads to the chicken or egg dilemma. Which comes first, clustering or feature selection? If the answer to the latter is yes, then is the not in feature selection literature. We usually use feature selection, as mentioned earlier, to improve learning quality, reduce computational time, and reduce required storage. Thus, the answer to the first question is, indeed, we use feature selection to improve clustering quality. Accordingly, we should select the features that preserve cluster structure. However, some current methods initialize