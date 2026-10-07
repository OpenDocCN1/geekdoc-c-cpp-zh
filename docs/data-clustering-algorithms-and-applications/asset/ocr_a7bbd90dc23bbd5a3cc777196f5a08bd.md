# 296 Data Clustering: Algorithms and Applications

The best-case complexity of MULIC has a lower bound of $\Omega(mKn)$ and its worst-case complexity has an upper bound of $O(mnk^2)$. The MULIC complexity is comparable to that of k-Modes of $O(mnkt)$, where $t$ is the number of iterations [47].

# 12.4.4 Model-Based Clustering

Model-based clustering assumes that objects match a model, or clusters objects that they match the distribution. The model may be user-specified and the parameter may change during the process. In bioinformatics, model-based clustering methods integrate background knowledge into gene expression, interactomes, and sequences [23, 66, 45, 51, 52]. Building models is an unsupervised; some assumptions may be false and the results will be inaccurate. Another disadvantage of model-based clustering (especially neural networks) is slow processing on large datasets.

# 12.4.4.1 BILCOM Empirical Bayesian (Mixed Categorical and Numerical)

BILCOM Bi-Level Clustering Of Mixed categorical and numerical data types is a model-based method [10]. This algorithm adapts an empirical Bayesian approach, with categorical data as the guide. In biological applications to genes, Gene Ontology (GO) annotations represent the categorical data and gene expression data numerical. Model-based clustering finds arbitrary gene expression clusters by incorporating background knowledge [1, 24, 45, 51, 52, 69, 20, 64].

The BILCOM performs clustering at two levels, where the first level clustering serves as a foundation for the second level, simulating a pseudo-Bayesian process. BILCOM is primarily applied to datasets from the domain. In these sets, categorical data represents semantic information on the objects, while numerical data represents experimental results. Categorical similarity is emphasized at the first level and numerical similarity at the second level. The first level output is given as input to the second level and the second level result is the output of BILCOM. Figure 12 shows clusters. The second level consists of substructures. Object A is assigned to different first and second level clusters, where the numerical similarity at the second level is stronger than the categorical similarity at the first level. On the other hand, object B is assigned to the same clusters because both categorical and numerical similarities support this classification. BILCOM considers categorical and numerical similarities of objects to the clusters to which it may be assigned.

Different types of data are used at first and second levels. The numerical data represents results results involving objects. For example, the numerical data used at the second level might look as follows: BILIRUBIN: 0.39; ALBUMIN: 2.1; PROTIME: 10. The categorical data represent what was observed to be true about the objects of the example. For example, the categorical data used at the first level might be existing information on objects looking as follows: SEX: male; STEROID: yes; FATIG: no.

The main disadvantage of BILCOM is that the user has to specify the number of clusters.

# 12.4.4.2 AutoClass (Mixed Categorical and Numerical)

AutoClass is a clustering algorithm for mixed datasets, which uses a Bayesian method for determining the optimal clusters based on prior distributions [71]. AutoClass finds the most likely classifications of objects in clusters, given a prior distribution for each attribute, symbolizing prior beliefs of the user. In the first step the user selects a probabilistic distribution for each of the $m$ attributes in the dataset. As an example, let the evidence on an object $X = \{age=28, blood-type=A, weight=73kg\}$; blood-type is a categorical attribute that is modeled with a Bernoulli distribu...

© 2014 Taylor & Francis Group, LLC