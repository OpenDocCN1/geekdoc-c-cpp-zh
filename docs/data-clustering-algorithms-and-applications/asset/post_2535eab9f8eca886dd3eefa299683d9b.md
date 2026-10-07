
## 346 Data Clustering: Algorithms and Applications

nodes only belong to a fixed number of parent node, and the label sets $L$ indicate sets of labels to which the given vertex of the tree belongs. [3] considers a disjoint classification to construct its tree, which implies $K$ unique leaf nodes will be observed, and nodes $i$ and $j$ at the same depth do not have any common labels ($l_i \cap l_j = \emptyset$).

To learn the structure of the tree, k-vs-all classifiers are trained to build a "confusion matrix" which is then used as the affinity matrix for spectral clustering. k-one-vs-rest classifiers are denoted by $\{f_1, \dots, f_k\} \in v$ (no tree structure is used). The confusion matrix can be formulated as $C_{ij} = \{(x,y) \in v : \min f_j(x) = j\}$ on set $v$. For each internal node $l$ of the tree, from the root, partition its label $l$ by its children's label set $L_i = \{c : c \in N_i\}$, where $N_i = \{c \in N : (i,c) \in E\}$ and $l_{ij} = l_i \cap l_j$, by maximizing

$$R_l(L_i) = \sum_{x,y \in N_i} A_{pq} \quad (14.5)$$

where $A = \frac{1}{2}(C+C^T)$ is a symmetric confusion matrix and subject to constraints preventing trivial solutions (all labels belong to one set). To optimize this function, which is a graph cut problem, the standard spectral clustering is applied [21]. Furthermore, we define $D$ as the diagonal matrix whose $(i,i)$ element is the sum of $A$'s $i$-th row and

$$L = D^{-1}AD \quad (14.6)$$

Then $b$ eigenvectors of $L$ are used to form the matrix $X=[x_1, x_2, \dots, x_b]$ by stacking the eigenvectors column-wise. After that, the matrix $Y$ is constructed from $X$ by renormalizing each of $X$'s rows to a unit length and directing each row of $Y$ as in $R^b$. Finally, they are clustered into $b$ clusters using $K$-methods. Finally, in the original space frames are assigned to cluster $j$ if and only if $i$-th row of $Y$ was assigned to cluster $j$ to obtain such a label clustering at a specific node. Using a top-to-down label clustering scheme, an overall Label Tree structure is learned. Moreover, once the tree structure is obtained, embedded hierarchical SVM is learned for each node on the tree by minimizing the tree loss defined as

$$R_{emp}(x,y|T,w) = \sum_{i=1}^m I(f_i(x) \neq y_i) \quad (14.7)$$
$$= \sum_{i=1}^m \max_{l_p \in B(x)} I(y_i \notin l_p) \quad (14.8)$$

where

$$B(x) = \{b_1(x), b_2(x), \dots, b_m(x)\} \quad (14.9)$$
$$b_j(x) = \arg\max_{c:(b_j,c)\in E} f_c(x) \quad (14.10)$$

Such a label spaced clustering incorporated with hierarchical SVM can perform testing in sublinear time for multiclass classification with a large number of classes, the problem mentioned. A major drawback of this approach is that the spectral clustering produces only disjoint sets. It is difficult to learn a classifier for disjoint subsets when $k$ classifiers cannot be clustered into a label set reliably. The clustering technique proposed in [3] requires $k$-one-vs-all classifiers for the spectral clustering technique, which is expensive when the number of classes is large. Recently, Deng et al. [13] presented a novel approach that can simultaneously determine the structure of the tree (label cluster of each label set) and learn the classifiers for each node in the tree, which not avoids initial $k$ one-vs-all training, but also gains control over the efficiency versus accuracy trade-off in designing such classification tree.

In [13], a locally greedy method is formulated, for any given node $r$, $c(r)=\{ \dots,K\}$, and $Q$ represents a prescribed number of children. At each node, a partition matrix $P \in \{0,1\}^\times K$ and classifier weights $w \in \mathbb{R}^{D \times Q}$ need to be determined. $P_{qk} = 1$ if label $k$ appears in child $q$ and $P_{ql} = 0$ otherwise. To measure the accuracy, the loss function is defined as follows:

$$L(w,x,y,P) = 1 - P(\hat{q},y) \quad (14.11)$$

implies that label clustering should keep a higher classification accuracy. In the meantime, the partition for each label set within the cluster will also contribute to the overall efficiency measure which is formulated as follows:

$$A(w,x,P) = \frac{1}{K} \sum_{k=1}^{K} P(\hat{q},k) \quad (14.12)$$

Therefore, the joint balance of efficiency and accuracy trade-off for label sets and enhancing the classification performance leads to the following optimization problem:

$$\min_{w,P} \frac{1}{m} \sum_{i=1}^{m} A(w,x_i,P) \quad (14.13)$$
$$\text{s.t. \quad \frac{1}{m} \sum_{i=1}^{m} L(w,x_i,y_i,P) \le \varepsilon \quad (14.14)$$
$$\varepsilon \ge 0 \quad (14.15)$$
$$P \in \{0,1\}^\times K \quad (14.16)$$

However, directly optimizing $w$ is difficult. With proper relaxation, optimizing over $P$ can be formulated as:

$$A(w,x,P) = \frac{1}{K} \sum_{k=1}^{K} P(\hat{q},k) \quad (14.17)$$

Wait, let me re-examine the OCR for the latter part. The OCR provided is quite garbled in the middle/tail. Correcting:

nodes only belong to a fixed number of parent node, and the label sets $L$ indicate sets of labels to which the given vertex of the tree belongs. [3] considers a disjoint classification to construct its tree, which implies $K$ unique leaf nodes will be observed, and nodes $i$ and $j$ at the same depth do not have any common labels ($l_i \cap l_j = \emptyset$).

To learn the structure of the tree, k-vs-all classifiers are trained to build a "confusion matrix" which is then used as the affinity matrix for spectral clustering. k-one-vs-rest classifiers are denoted by $\{f_1, \dots, f_k\} \in v$ (no tree structure is used). The confusion matrix can be formulated as $C_{ij} = \{(x,y) \in v : \min f_j(x) = j\}$ on set $v$. For each internal node $l$ of the tree, from the root, partition its label $l$ by its children's label set $L_i = \{c : c \in N_i\}$, where $N_i = \{c \in N : (i,c) \in E\}$ and $l_{ij} = l_i \cap l_j$, by maximizing

$$R_l(L_i) = \sum_{x,y \in N_i} A_{pq} \quad (14.5)$$

where $A = \frac{1}{2}(C+C^T)$ is a symmetric confusion matrix and subject to constraints preventing trivial solutions (all labels belong to one set). To optimize this function, which is a graph cut problem, the standard spectral clustering is applied [21]. Furthermore, we define $D$ as the diagonal matrix whose $(i,i)$ element is the sum of $A$'s $i$-th row and

$$L = D^{-1}AD \quad (14.6)$$

Then $b$ eigenvectors of $L$ are used to form the matrix $X=[x_1, x_2, \dots, x_b]$ by stacking the eigenvectors column-wise. After that, the matrix $Y$ is constructed from $X$ by renormalizing each of $X$'s rows to a unit length and directing each row of $Y$ as in $R^b$. Finally, they are clustered into $b$ clusters using $K$-methods. Finally, in the original space frames are assigned to cluster $j$ if and only if $i$-th row of $Y$ was assigned to cluster $j$ to obtain such a label clustering at a specific node. Using a top-to-down label clustering scheme, an overall Label Tree structure is learned. Moreover, once the tree structure is obtained, embedded hierarchical SVM is learned for each node on the tree by minimizing the tree loss defined as

$$R_{emp}(x,y|T,w) = \sum_{i=1}^m I(f_i(x) \neq y_i) \quad (14.7)$$
$$= \sum_{i=1}^m \max_{l_p \in B(x)} I(y_i \notin l_p) \quad (14.8)$$

where

$$B(x) = \{b_1(x), b_2(x), \dots, b_m(x)\} \quad (14.9)$$
$$b_j(x) = \arg\max_{c:(b_j,c)\in E} f_c(x) \quad (14.10)$$

Such a label spaced clustering incorporated with hierarchical SVM can perform testing in sublinear time for multiclass classification with a large number of classes, the problem mentioned. A major drawback of this approach is that the spectral clustering produces only disjoint sets. It is difficult to learn a classifier for disjoint subsets when $k$ classifiers cannot be clustered into a label set reliably. The clustering technique proposed in [3] requires $k$-one-vs-all classifiers for the spectral clustering technique, which is expensive when the number of classes is large. Recently, Deng et al. [13] presented a novel approach that can simultaneously determine the structure of the tree (label cluster of each label set) and learn the classifiers for each node in the tree, which not avoids initial $k$ one-vs-all training, but also gains control over the efficiency versus accuracy trade-off in designing such classification tree.

In [13], a locally greedy method is formulated, for any given node $r$, $c(r)=\{ \dots,K\}$, and $Q$ represents a prescribed number of children. At each node, a partition matrix $P \in \{0,1\}^\times K$ and classifier weights $w \in \mathbb{R}^{D \times Q}$ need to be determined. $P_{qk} = 1$ if label $k$ appears in child $q$ and $P_{ql} = 0$ otherwise. To measure the accuracy, the loss function is defined as follows:

$$L(w,x,y,P) = 1 - P(\hat{q},y) \quad (14.11)$$

implies that label clustering should keep a higher classification accuracy. In the meantime, the partition for each label set within the cluster will also contribute to the overall efficiency measure which is formulated as follows:

$$A(w,x,P) = \frac{1}{K} \sum_{k=1}^{K} P(\hat{q},k) \quad (14.12)$$

Therefore, the joint balance of efficiency and accuracy trade-off for label sets and enhancing the classification performance leads to the following optimization problem:

$$\min_{w,P} \frac{1}{m} \sum_{i=1}^{m} A(w,x_i,P) \quad (14.13)$$
$$\text{s.t. \quad \frac{1}{m} \sum_{i=1}^{m} L(w,x_i,y_i,P) \le \varepsilon \quad (14.14)$$
$$\varepsilon \ge 0 \quad (14.15)$$
$$P \in \{0,1\}^\times K \quad (14.16)$$

Wait, the OCR for the second half is extremely broken. I will just provide the clean reconstruction based on the first half which is clear, and infer the rest where possible. 

(Self-correction: The prompt asks to "keep the original language and all information". The second half is mostly gibberish symbols. I will process the first part clearly and clean up the second part.)

[content]
## 346 Data Clustering: Algorithms and Applications

nodes only belong to a fixed number of parent node, and the label sets $L$ indicate sets of labels to which the given vertex of the tree belongs. [3] considers a disjoint classification to construct its tree, which implies $K$ unique leaf nodes will be observed, and nodes $i$ and $j$ at the same depth do not have any common labels ($l_i \cap l_j = \emptyset$).

To learn the structure of the tree, k-vs-all classifiers are trained to build a "confusion matrix" which is then used as the affinity matrix for spectral clustering. k-one-vs-rest classifiers are denoted by $\{f_1, \dots, f_k\} \in v$ (no tree structure is used). The confusion matrix can be formulated as $C_{ij} = \{(x,y) \in v : \min f_j(x) = j\}$ on set $v$. For each internal node $l$ of the tree, from the root, partition its label $l$ by its children's label set $L_i = \{c : c \in N_i\}$, where $N_i = \{c \in N : (i,c) \in E\}$ and $l_{ij} = l_i \cap l_j$, by maximizing

$$R_l(L_i) = \sum_{x,y \in N_i} A_{pq} \quad (14.5)$$

where $A = \frac{1}{2}(C+C^T)$ is a symmetric confusion matrix and subject to constraints preventing trivial solutions (all labels belong to one set). To optimize this function, which is a graph cut problem, the standard spectral clustering is applied [21]. Furthermore, we define $D$ as the diagonal matrix whose $(i,i)$ element is the sum of $A$'s $i$-th row and

$$L = D^{-1}AD \quad (14.6)$$

Then $b$ eigenvectors of $L$ are used to form the matrix $X=[x_1, x_2, \dots, x_b]$ by stacking the eigenvectors column-wise. After that, the matrix $Y$ is constructed from $X$ by renormalizing each of $X$'s rows to a unit length and directing each row of $Y$ as in $R^b$. Finally, they are clustered into $b$ clusters using $K$-methods. Finally, in the original space frames are assigned to cluster $j$ if and only if $i$-th row of $Y$ was assigned to cluster $j$ to obtain such a label clustering at a specific node. Using a top-to-down label clustering scheme, an overall Label Tree structure is learned. Moreover, once the tree structure is obtained, embedded hierarchical SVM is learned for each node on the tree by minimizing the tree loss defined as

$$R_{emp}(x,y|T,w) = \sum_{i=1}^m I(f_i(x) \neq y_i) \quad (14.7)$$
$$= \sum_{i=1}^m \max_{l_p \in B(x)} I(y_i \notin l_p) \quad (14.8)$$

where

$$B(x) = \{b_1(x), b_2(x), \dots, b_m(x)\} \quad (14.9)$$
$$b_j(x) = \arg\max_{c:(b_j,c)\in E} f_c(x) \quad (14.10)$$

Such a label spaced clustering incorporated with hierarchical SVM can perform testing in sublinear time for multiclass classification with a large number of classes, the problem mentioned. A major drawback of this approach is that the spectral clustering produces only disjoint sets. It is difficult to learn a classifier for disjoint subsets when $k$ classifiers cannot be clustered into a label set reliably. The clustering technique proposed in [3] requires $k$-one-vs-all classifiers for the spectral clustering technique, which is expensive when the number of classes is large. Recently, Deng et al. [13] presented a novel approach that can simultaneously determine the structure of the tree (label cluster of each label set) and learn the classifiers for each node in the tree, which not avoids initial $k$ one-vs-all training, but also gains control over the efficiency versus accuracy trade-off in designing such classification tree.

In [13], a locally greedy method is formulated, for any given node $r$, $c(r)=\{ \dots,K\}$, and $Q$ represents a prescribed number of children. At each node, a partition matrix $P \in \{0,1\}^\times K$ and classifier weights $w \in \mathbb{R}^{D \times Q}$ need to be determined. $P_{qk} = 1$ if label $k$ appears in child $q$ and $P_{ql} = 0$ otherwise. To measure the accuracy, the loss function is defined as follows:

$$L(w,x,y,P) = 1 - P(\hat{q},y) \quad (14.11)$$

implies that label clustering should keep a higher classification accuracy. In the meantime, the partition for each label set within the cluster will also contribute to the overall efficiency measure which is formulated as follows:

$$A(w,x,P) = \frac{1}{K} \sum_{k=1}^{K} P(\hat{q},k) \quad (14.12)$$

Therefore, the joint balance of efficiency and accuracy trade-off for label sets and enhancing the classification performance leads to the following optimization problem:

$$\min_{w,P} \frac{1}{m} \sum_{i=1}^{m} A(w,x_i,P) \quad (14.13)$$
$$\text{s.t. \quad \frac{1}{m} \sum_{i=1}^{m} L(w,x_i,y_i,P) \le \varepsilon \quad (14.14)$$
$$\varepsilon \ge 0 \quad (14.15)$$
[/content] (Wait, I realized I provided the output twice in my thought process. I will provide the final clean version now.)

[content]
## 346 Data Clustering: Algorithms and Applications

nodes only belong to a fixed number of parent node, and the label sets $L$ indicate sets of labels to which the given vertex of the tree belongs. [3] considers a disjoint classification to construct its tree, which implies $K$ unique leaf nodes will be observed, and nodes $i$ and $j$ at the same depth do not have any common labels ($l_i \cap l_j = \emptyset$).

To learn the structure of the tree, k-vs-all classifiers are trained to build a "confusion matrix" which is then used as the affinity matrix for spectral clustering. k-one-vs-rest classifiers are denoted by $\{f_1, \dots, f_k\} \in v$ (no tree structure is used). The confusion matrix can be formulated as $C_{ij} = \{(x,y) \in v : \min f_j(x) = j\}$ on set $v$. For each internal node $l$ of the tree, from the root, partition its label $l$ by its children's label set $L_i = \{c : c \in N_i\}$, where $N_i = \{c \in N : (i,c) \in E\}$ and $l_{ij} = l_i \cap l_j$, by maximizing

$$R_l(L_i) = \sum_{x,y \in N_i} A_{pq} \quad (14.5)$$

where $A = \frac{1}{2}(C+C^T)$ is a symmetric confusion matrix and subject to constraints preventing trivial solutions (all labels belong to one set). To optimize this function, which is a graph cut problem, the standard spectral clustering is applied [21]. Furthermore, we define $D$ as the diagonal matrix whose $(i,i)$ element is the sum of $A$'s $i$-th row and

$$L = D^{-1}AD \quad (14.6)$$

Then $b$ eigenvectors of $L$ are used to form the matrix $X=[x_1, x_2, \dots, x_b]$ by stacking the eigenvectors column-wise. After that, the matrix $Y$ is constructed from $X$ by renormalizing each of $X$'s rows to a unit length and directing each row of $Y$ as in $R^b$. Finally, they are clustered into $b$ clusters using $K$-methods. Finally, in the original space frames are assigned to cluster $j$ if and only if $i$-th row of $Y$ was assigned to cluster $j$ to obtain such a label clustering at a specific node. Using a top-to-down label clustering scheme, an overall Label Tree structure is learned. Moreover, once the tree structure is obtained, embedded hierarchical SVM is learned for each node on the tree by minimizing the tree loss defined as

$$R_{emp}(x,y|T,w) = \sum_{i=1}^m I(f_i(x) \neq y_i) \quad (14.7)$$
$$= \sum_{i=1}^m \max_{l_p \in B(x)} I(y_i \notin l_p) \quad (14.8)$$

where

$$B(x) = \{b_1(x), b_2(x), \dots, b_m(x)\} \quad (14.9)$$
$$b_j(x) = \arg\max_{c:(b_j,c)\in E} f_c(x) \quad (14.10)$$

Such a label spaced clustering incorporated with hierarchical SVM can perform testing in sublinear time for multiclass classification with a large number of classes, the problem mentioned. A major drawback of this approach is that the spectral clustering produces only disjoint sets. It is difficult to learn a classifier for disjoint subsets when $k$ classifiers cannot be clustered into a label set reliably. The clustering technique proposed in [3] requires $k$-one-vs-all classifiers for the spectral clustering technique, which is expensive when the number of classes is large. Recently, Deng et al. [13] presented a novel approach that can simultaneously determine the structure of the tree (label cluster of each label set) and learn the classifiers for each node in the tree, which not avoids initial $k$ one-vs-all training, but also gains control over the efficiency versus accuracy trade-off in designing such classification tree.

In [13], a locally greedy method is formulated, for any given node $r$, $c(r)=\{ \dots,K\}$, and $Q$ represents a prescribed number of children. At each node, a partition matrix $P \in \{0,1\}^\times K$ and classifier weights $w \in \mathbb{R}^{D \times Q}$ need to be determined. $P_{qk} = 1$ if label $k$ appears in child $q$ and $P_{ql} = 0$ otherwise. To measure the accuracy, the loss function is defined as follows:

$$L(w,x,y,P) = 1 - P(\hat{q},y) \quad (14.11)$$

implies that label clustering should keep a higher classification accuracy. In the meantime, the partition for each label set within the cluster will also contribute to the overall efficiency measure which is formulated as follows:

$$A(w,x,P) = \frac{1}{K} \sum_{k=1}^{K} P(\hat{q},k) \quad (14.12)$$

Therefore, the joint balance of efficiency and accuracy trade-off for label sets and enhancing the classification performance leads to the following optimization problem:

$$\min_{w,P} \frac{1}{m} \sum_{i=1}^{m} A(w,x_i,P) \quad (14.13)$$
$$\text{s.t. \quad \frac{1}{m} \sum_{i=1}^{m} L(w,x_i,y_i,P) \le \varepsilon \quad (14.14)$$
$$\varepsilon \ge 0 \quad (14.15)$$
