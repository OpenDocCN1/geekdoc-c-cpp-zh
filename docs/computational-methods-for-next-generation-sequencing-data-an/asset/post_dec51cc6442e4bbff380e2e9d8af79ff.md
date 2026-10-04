
solution (step 18) otherwise and forbids for $k_i$ steps of moving the vertex, which leads to the previous local optimum (step 19). If the current algorithm state has not occurred previously, the algorithm adds it to the optStates and proceeds to the next iteration (steps 21–24). Otherwise, the algorithm reduces the current record $(A^*, B^*)$ to the solution where $|A^*| \le T$ and stops (steps 25–30).

The default value of $k_i$ is 1. It is still possible that for the solution $(A^*, B^*)$ found by Algorithm 2, we have $c(A^*, B^*) = 0$. If it happens, we increase $k_i$, by one and repeat Algorithm 2.

## 3.3 DECONVOLUTION OF VIRAL SAMPLES FROM POOLS

According to Examples 1 and 2, deconvolution requires computing of intersections and differences of pools. In Section 3.3.1, we formally define generalized intersections and differences of pools and show how to use them for pool deconvolution. The challenges of implementation of generalized intersections and differences are addressed in Section 3.3.2.

### 3.3.1 Deconvolution Using Generalized Intersections and Differences of Pools

Let $P$ be the pool of sets designed using a solution of the VPD problem found by Algorithm GOPDA and sequenced using NGS. As discussed, the obtained reads theoretically to be assigned to the samples of set-theoretical intersections and differences of pools (see Examples 1 and 2). However, owing to the high heterogeneity of viral populations and sampling bias, individual viral variants even subpopulations of viral variants sequenced from a certain sample mixed with different pools may be different in each pool (see an example on Figure 3.3). It

![](img/46aec008551cecb3bbf3aac2ee69b926_89_0.png)

**Figure 3.3** Phylogenetic tree representing a union of two pools: $P_1$ consisting of samples $S_1, S_2, S_3$ (shown in light grey) and $P_2$ consisting of samples $S_4, S_5$ (shown in dark grey). The intersection of two pools consists of the sample $S_1$ (upper right cluster in the tree); however, sequences sampled from $S_1$ in pools $P_1$ and $P_2$ are different. Source: Skums 2015 (29). Reproduced with permission of Oxford University Press.

hampers the usage of straightforward set-theoretical intersections and differences, and, therefore, "generalized" intersections and differences should be used instead. For a pool $P_i$, let $S(P_i)$ be a set of samples mixed in it. In particular, for simplicity of notations, we can assume that each individual sample $R_j$ is a special type of pool with $|S(R_j)| = 1$.

We define the generalized intersection of pools $P_1$ and $P_2$ as the pool $P_1 \cap P_2 = S(P_1) \cap S(P_2)$, consisting of sequences from $P_1 \cup P_2$ that belong to the samples from $S(P_1) \cap S(P_2)$. The generalized difference $P_1 \setminus P_2$ can then be defined as follows: $P_1 \setminus P_2$ is the pool with $S(P_1 \setminus P_2) = S(P_1) \setminus S(P_2)$ that contains sequences of the set $P_1 \setminus (P_1' \cap P_2)$.

Individual samples can be inferred by pools of generalized intersections and differences using Algorithm IS. By definition, generalized differences may be reduced to generalized intersections. For calculations of generalized intersections, we propose the scheme described in Algorithm GI, which is based on clustering techniques.

# Algorithm PD: Deconvolution algorithm
Require: the set of pools $P = \{P_1, \dots, P_m\}$
Ensure: the set of individual samples $R = \{R_1, \dots, R_n\}$

```
1: procedure IS($P$)
2: define two queues $Q$ and $R'$ as follows: $Q$ contains all pools and $R' = \emptyset$.
3: while $Q \neq \emptyset$ do
4: $P' \leftarrow$ first element of $Q$
5: if $|S(P')| = 1$ then
6: $R' \leftarrow R' \cup \{P'\}$
7: end
8: $Q \leftarrow Q \setminus P'$
9: for $P'' \in Q$ do
10: if $S(P') \cap S(P'') \neq \emptyset$ then
11: $Q \leftarrow Q \cup \{P' \cap P''\}$
12: if $S(P') \setminus S(P'') \neq \emptyset$ then
13: $Q \leftarrow Q \cup \{P' \setminus P''\}$
14: end
15: if $S(P'') \setminus S(P') \neq \emptyset$ then
16: $Q \leftarrow Q \cup \{P'' \setminus P'\}$
17: end
18: break
19: end if
20: end for
21: end while
22: return $n$ elements of $R'$
23: end procedure
```

# Algorithm GI: Generalized Intersection
**Require:** $P_1, P_2$, parameter $W \ge 1$
**Ensure:** The generalized intersection $P_1 \cap P_2$

1: **procedure** $GI(P_1, P_2)$
2: $k \leftarrow |S(P_1) \cup S(P_2)|$
3: Partition the union $P_1 \cup P_2$ into $k$ clusters using Maximum Likelihood $k$-Clustering described in the next subsection.
4: **return** the union of clusters which contains reads from both pools $P_1$ and $P_2$.
5: **end procedure**

Theoretically, Algorithm GI may be used with $W=1$. Viral populations of highly mutated viruses, such as HCV and HIV, may differ in heterogeneity. Extreme cases, host heterogeneity of certain samples may be comparable. If samples belong to the same pool, it can lead to effect when $W=1$, highly heterogeneous samples may be partitioned into multiple clusters while samples with lower heterogeneity will be joined into one. Clustering will lead to incorrect detection of generalized intersections and loss of samples not separated from other samples. To avoid this effect, higher values of $W$ should be used. In our experiments, the default value $W=2$. If certain samples are not found by Algorithm IS (i.e., the corresponding data are empty), we increase the value of $W$ by one and repeat Algorithm IS.

## 3.3.2 Maximum Likelihood $k$-Clustering

In this section, we formulate the clustering problem and describe our solution, which is based on probabilistic $k$-means approach (see Reference 37).

**Sample Clustering**. Given a set $R$ of NGS reads drawn from a mix of $k'$ viral samples, partition $R$ into $k'$ subsets of reads from a single sample.

The presence of numerous sequence variants in each viral sample, extreme heterogeneity of viral populations, and a large number of reads make sample problem challenging. Although a commonly used clustering objective is to minimize intracluster distances or distance to cluster centers (e.g., the $k$-means algorithm), we propose to use statistically sound objective of maximizing likelihood. Our model estimates the probability of a certain read being emitted by a cluster (centroid).

Our algorithm represents a multiple sequence alignment of a given set of reads $R$ as a matrix with columns corresponding to consensus positions and rows corresponding to aligned reads. Our model assumes that each read in a cluster is emitted by a particular genotype (centroid). The proposed clustering finds genotypes $g_1, \dots, g_k$, which most likely emit the set of reads, (ii) estimates probability $p_{tr}$ that read $r$ is emitted by a genotype $g_t$, and (iii) assigns a read $r$ to a cluster that most likely emits $r$.

Formally, given a set of reads $C$, a genotype $g(C)$ of $C$ is a matrix with each column corresponding to a consensus position and five rows each corresponding to one of the alleles $\{a, c, t, g, d\}$. Each entry $f_m(e), e\in\{a, c, t, g, d\}$ is the frequency of allele $e$ in $m$th position among all variants $C$, $\sum_{e\in\{a,c,t,g,d\}}f_m(e)=1$. In particular, every read can be considered as a genotype with a single 1 and 4 zeroes in each column. Given a set of reads $R$, a $k$-genotype is $G^*=\{g_1, \dots, g_k\}$ of $k$ distinct genotypes that most likely read $R$:

```
$G^* = \arg\max Pr(R|G), \quad |G|=k$$
```

where $Pr(R|G)$ is the probability to observe $R$ given a set of genotypes $G$, which is calculated as a product of probabilities to observe each read from $R$. The probability to observe read $r$ equals to $Pr(r)=\prod_{i=1}^l f_i Pr(r|g=g_i)$, where

```
$Pr(r|g=g_i)=\prod_{m=1}^l f_{im}(r_m), \quad (3.10)$
```

and $f_{im}(r_m)$ is the frequency of $m$th character of $r$, in the $m$th position of genotype $g_i$. Then the log-likelihood of the set of allele frequencies $\mathcal{F}=\{f_{im}(e)|i=1,\dots,k; m=1,\dots,l; e\in\{a,c,t,g,d\}\}$ to

where $o_r$ is the observed data $p_{i,r}$, that is, the number of times the read $r$ originated from the genotype $g_i$, and solve the easier optimization problem of maximizing the log-likelihood of the hidden model

```
$$\ell_{hid}(F)=\sum_{r\in R}\sum_{i=1}^k p_{i,r} \log (f_i Pr(r|g_i)).$$
```

Our clustering method is described in Algorithm kGEM. The initial set of genotypes $G^{(0)}$ is selected as follows: from the most frequent read, we iteratively select the read maximizing the minimum Hamming distance to the previously selected reads and add to $G^{(0)}$ the corresponding genotype.

## 3.4 PERFORMANCE OF POOLING METHODS ON SIMULATED DATA

### 3.4.1 Performance of the Viral Sample Pool Design Algorithm

The pool generation algorithm was evaluated using three sets of simulated data.

-1. Complete graphs.
Pools were generated for complete graphs with $n=4,\dots,102$ vertices without the threshold of pools' size. For every test instance, exactly $m=\lceil\log(n)\rceil+1$ pools were constructed, coinciding with the theoretically justified estimation. Hence VSPD algorithm produces optimal solutions for complete graphs.
