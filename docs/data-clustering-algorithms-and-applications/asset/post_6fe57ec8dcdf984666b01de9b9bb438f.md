
# Network Clustering

(protein) can have multiple functions. Kelley et al. [89] show that overlap is a significant feature of many social networks. Most of the partitioning algorithms explained in this chapter target a disjoint clustering of the network. Recently, there has been a growth in algorithms that can detect overlapping community structures.

Given a graph $\mathcal{G}=(V,E)$, a cover, $C=(c_1,c_2,\dots,c_k)$, is a set of clusters found by overlapping community detection [96], and each node is assigned to a community with a belonging factor $b_1,b_2,\dots,b_n$ [122]. It is assumed that $0 \le b_i \le 1$ and $\sum b_i=1$. Node assignment to clusters can be crisp or fuzzy [71]. In crisp assignment, each node belongs to a community or not; but in fuzzy assignment, the membership of a node in a cluster is expressed as a belonging factor [172].

Xie et al. [172] categorize algorithms for overlapping community detection into five categories based on how communities are identified.

- **Clique Percolation Algorithm (CPM)** assumes that a community consists of overlapping fully connected subgraphs and, hence, searches adjacent cliques in order to detect communities. CFinder is the implementation of CPM which has a polynomial time complexity in many large social networks [172]. Related works under this category use subgraph intensity threshold for weighted networks by Farkas et al. [55] and SCP by Kumpula et al. [95] that finds cliques of communities given given size. SCP is faster than CPM and allows weighted threshold in a single scale.

- **Line Graph and Link Partitioning** explores the idea of link partitioning and a node in the graph overlapping links connected to it are partitioned into more than one clusters. Some works in this context are presented in [3, 53, 52]. Despite being intuitively, there is no guarantee that it gives better detection than node-based methods [59] because it depends on an ambiguous definition of community.

- **Local Expansion and Optimization** is based on growing a natural [9] or partial community that relies on local benefit function characterizing the quality of a densely connected group of nodes, Baumes et al. [15] propose a two-step process: RankRemoval finds the seed community for the second Iterative Scan (IS). LFM, expands a community from random seed with respect to a fitness function. Havemann et al. proposed MON [75] that uses a modified fitness function of LFM. A thorough study of local expansion and optimization algorithms can be found in [172].

- **Fuzzy Detection** algorithms quantify a soft membership vector or belonging factor [70] for each node which represents the strength of association between pairs of nodes and communities. Nepuzuz et al. [122] model the problem as nonlinear constrained optimization that can be solved using simulated annealing methods. Zhang et al. [171] propose a spectral clustering-based algorithm that uses fuzzy cmeans (FCM) to obtain a soft assignment. Use of mixture models has been explored in this context and examples are SPAEM [143] and FOG [39]. OSM [98] and MOSES [110] are based on the Stochastic Block Model (SBM) [127] generative model. Detailed descriptions of above mentioned and related algorithms can be found in [17].

- **Agent Based and Dynamical** Algorithms extend the label propagation [139] to overlapping community detection. In COPRA [70] each node averages the belonging coefficients of neighbors in a social fashion to update their coefficients in each step. SLPA [173] follows pairwise interaction rules to spread labels between nodes based on a general speaker-listener-based information propagation process. Chen et al. [72] propose a game theoretic framework where a community is associated with a Nash equilibrium and each agent has a gain and loss function. The assumption is agents are selfish and for communities based on respective utilities. Berry et al. [17] propose a process that particles walk and compete with each other node, and particles represent different communities. A comprehensive study on this topic can be found in [172].

# Data Clustering: Algorithms and Applications

Many algorithms have been proposed in the literature to address the problem. CONGO [69] allows a node to split into multiple copies, extends Girvan-Newman's (GN) divisive clustering algorithm [68], and optimizes for associated high complexity it of speed. Xie et al. present:

- **Overlapping Markov Clustering (OMCL)** has been recently proposed by Parthasarathy et al. in [152]. Despite being intuitively, there is no guarantee that it gives better detection than node-based methods [59] because it depends on an ambiguous definition of community.

- **Regularized Markov Clustering (RMCL)** has been proposed by Shih et al. in [48]. This approach allows the number of.

- **Fuzzy Detection** algorithms quantify a soft membership vector or belonging factor [70] for each node which represents the strength of association between pairs of nodes and communities. Nepuzuz et al. [122] model the problem as nonlinear constrained optimization that can be solved using simulated annealing methods. Zhang et al. [171] propose a spectral clustering-based algorithm that uses fuzzy cmeans (FCM) to obtain a soft assignment. Use of mixture models has been explored in this context and examples are SPAEM [143] and FOG [39]. OSM [98] and MOSES [110] are based on the Stochastic Block Model (SBM) [127] generative model. Detailed descriptions of above mentioned and related algorithms can be found in [17].

# Probabilistic Methods 

In this section we talk about some:

- **Generative Models:** Many algorithms have been proposed in the literature to address the problem. CONGO [69] allows a node to split into multiple copies, extends Girvan-Newman's (GN) divisive clustering algorithm [68], and optimizes for associated high complexity it of speed. Xie et al. present:

- **Expectation Maximization (EM):** Many algorithms have been proposed in the literature to address the problem. CONGO [69] allows a node to split into multiple copies, extends Girvan-Newman's (GN) divisive clustering algorithm [68], and optimizes for associated high complexity it of speed. Xie et al. present:

- **Gaussian Mixture Model (GMM):** Many algorithms have been proposed in the literature to address the problem. CONGO [69] allows a node to split into multiple copies, extends Girvan-Newman's (GN) divisive clustering algorithm [68], and optimizes for associated high complexity it of speed. Xie et al. present:

- **Stochastic Block Model (SBM):** Many algorithms have been proposed in the literature to address the problem. CONGO [69] allows a node to split into multiple copies, extends Girvan-Newman's (GN) divisive clustering algorithm [68], and optimizes for associated high complexity it of speed. Xie et al. present:

- **Random Graph Model (RGM):** Many algorithms have been proposed in the literature to address the problem. CONGO [69] allows a node to split into multiple copies, extends Girvan-Newman's (GN) divisive clustering algorithm [68], and optimizes for associated high complexity it of speed. Xie et al. present:
