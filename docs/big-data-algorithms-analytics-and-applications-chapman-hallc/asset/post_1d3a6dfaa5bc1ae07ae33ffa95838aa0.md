
A set of regions $R(QWL) = \{R(Q_0), R(Q_1), ..., R(Q_{|QWL|-1})\}$ is obtained. Let $R(Q_k)$ be a region belonging to $R(QWL)$; the amount of storage space allocated to $R(Q_k)$, $B(Q_k)$, is determined according to a proportional approach that considers (1) the nature of the data distribution of $R(Q_k)$ and geometrical issues of $R(Q_k)$ and (2) the latter parameters of $R(Q_k)$ in proportional comparison with the same parameters of all the regions in $R(QWL)$, as follows:

$B(Q_k) = \frac{\phi(R(Q_k)) + \Psi(R(Q_k)) \cdot \xi(R(Q_k))}{\sum_{i=0}^{|QWL|-1} \phi(R(Q_i)) + \sum_{i=0}^{|QWL|-1} \Psi(R(Q_i)) \cdot \xi(R(Q_i))} \cdot B$

such that [45] (1) $\Psi(R)$ is a Boolean characteristic function that, given a region $R$, allows us to decide if data in $R$ are uniform or skewed; (2) $\phi(R)$ is a factor that captures the skewness and the variance of $R$ in a combined manner; and (3) $\xi(R)$ is a factor that provides the ratio between the skewness of $R$ and its standard deviation, which, according to Reference 46, allows us to estimate the skewness degree of the data distribution of $R$. The previous formula can be extended to handle the overall allocation of $B$ across regions of $QWL$, thus achieving the formal definition of our proportional storage space allocation scheme, denoted by $\mathcal{W}(A,R(Q_0),R(Q_1),...,R(Q_{|QWL|-1}),B)$, via the following system:

$B(Q_0) = \frac{\phi(R(Q_0)) + \Psi(R(Q_0)) \cdot \xi(R(Q_0))}{\sum_{k=0}^{|QWL|-1} \phi(R(Q_k)) + \sum_{k=0}^{|QWL|-1} \Psi(R(Q_k)) \cdot \xi(R(Q_k))} \cdot B$

$...$

$B(Q_{|QWL|-1}) = \frac{\phi(R(Q_{|QWL|-1})) + \Psi(R(Q_{|QWL|-1})) \cdot \xi(R(Q_{|QWL|-1}))}{\sum_{k=0}^{|QWL|-1} \phi(R(Q_k)) + \sum_{k=0}^{|QWL|-1} \Psi(R(Q_k)) \cdot \xi(R(Q_k))} \cdot B \tag{16.1}$

$\sum_{k=0}^{|QWL|-1} B(Q_k) \approx B$

In turn, for each query region $R(Q_k)$ of $R(QWL)$, we further allocate the amount of storage space $B(Q_k)$ across the subqueries $q_{k,0}, q_{k,1}, q_{k,2}, ..., q_{k,m-1}$ obtained by decomposing $Q_k$ according to our decomposition process (see Section 16.8), via using the same allocation scheme (Equation 16.1). Overall, this approach allows us to obtain a storage space allocation for each subquery $q_{k,j}$ of $QWL$ in terms of the maximum sample number $N(q_{k,j}) = \frac{B(q_{k,j})}{32}$ that can be extracted from $q_{k,j}$, $B(q_{k,j})$ being the amount of storage space allocated to $q_{k,j}$.

It should be noted that the described approach allows us to achieve an extremely accurate level of detail in handling accuracy/privacy issues of the final synopsis data cube $A'$. To become convinced of this, recall that the granularity of OLAP client applications is that of queries (see Section 16.1.1), which is much greater than that of subqueries (specifically, the latter depends on the degree of accuracy grids) we use as the atomic unit of our reasoning. Thanks to this difference between granularity of input queries and accuracy grid cells, which, in our framework, is made “conveniently” high, we finally obtain a crucial information gain that allows us to efficiently accomplish the accuracy/privacy constraint.

### 16.9.2 Sampling Phase

Given an instance of our proportional allocation scheme (Equation 16.1), $\mathcal{W}$, during the second phase of algorithm computeSynDataCube, we sample the input data cube $A$ in order to obtain the synopsis data cube $A'$, in such a way as to satisfy the accuracy/privacy constraint with respect to the target query workload $QWL$. To this end, we apply a different strategy in dependence on the fact that query regions characterized by uniform or skewed distributions are handled, according to similar insights that have inspired our allocation technique (see Section 16.9.1). Specifically, for a skewed region $R(q_{k,i})$, given the maximum number of samples that can be extracted from $R(q_{k,i})$, $N(q_{k,i})$, we sample the $N(q_{k,i})$ outliers of $q_{k,i}$. It is worth noticing that, for skewed regions, the sum of outliers represents an accurate estimation of the sum of all the data cells contained within such regions. Also, it should be noted that this approach allows us to gain advantages with respect to approximate query answering as well as the privacy preservation of sensitive ranges of multidimensional data of skewed regions.

Contrary to this, for a uniform region $R(q_{k,j})$, given the maximum number of samples that can be extracted from $R(q_{k,j})$, $N(q_{k,j})$, let (1) $\bar{C}_{R(q_{k,j})}$ be the average of values of data cells contained within $R(q_{k,j})$; (2) $U(R(q_{k,j}),\bar{C}_{R(q_{k,j})})$ be the set of data cells $C$ in $R(q_{k,j})$ such that $\mathrm{value}(C) > \bar{C}_{R(q_{k,j})}$, where $\mathrm{value}(C)$ denotes the value of $C$; and (3) $\bar{C}_{U(R(q_{k,j}),\bar{C}_{R(q_{k,j})})}$ be the average of values of data cells in $U(R(q_{k,j}),\bar{C}_{R(q_{k,j})})$. We adopt the strategy of extracting $N(q_{k,j})$ samples from $R(q_{k,j})$ by selecting them as the $N(q_{k,j})$ closer-to-$\bar{C}_{U(R(q_{k,j}))}$ data cells $C$ in $R(q_{k,j})$ such that $\mathrm{value}(C) > \bar{C}_{R(q_{k,j})}$. Just like previous considerations given for skewed regions, it should be noted that the described sampling strategy for uniform regions allows us to meaningfully trade off the need for efficiently answering range-SUM queries against the synopsis data cube and the need for limiting the number of samples to be stored within the synopsis data cube.

In order to satisfy the accuracy/privacy constraint, the sampling phase aims at accomplishing (decomposed) accuracy and privacy constraints separately, based on a two-step approach. Given a query region $R(Q_k)$, we first sample $R(Q_k)$ in such a way as to satisfy the accuracy constraint, and then, we check if samples extracted from $R(Q_k)$ also satisfy, beyond the accuracy constraint, the privacy constraint. As mentioned in Section 16.7, this strategy follows a best-effort approach aiming at minimizing computational overheads due to computing the synopsis data cube, and it is also the conceptual basis of guidelines for setting the thresholds $\Phi_Q$ and $\Phi_I$.

Moreover, our sampling strategy aims at obtaining a tunable representation of the synopsis data cube $A'$, which can be progressively refined until the accuracy/privacy constraint

not satisfy the satisfiability condition, and (2) $Q^F$ is the query of $QWL^P$ having the greater negative distance from the satisfiability condition, that is, $Q^F$ is the query of $QWL^P$ that is in most need of new samples; (3) move enough samples from $Q^T$ to $Q^F$ in such a way as to satisfy the accuracy/privacy constraint on $Q^F$ while, at the same time, ensuring that $Q^T$ does not violate the constraint; and (4) repeat steps 1, 2, and 3 until the current representation of $A'$ satisfies, as much as possible, the accuracy/privacy constraint with respect to $QWL$, within the maximum number of iterations bounded by $L_{A,QWL}$.

Regarding step 3, moving $\rho$ samples from $Q^T$ to $Q^F$ means (1) removing $\rho$ samples from $R(Q^T)$, thus obtaining an additional space, named $B(\rho)$; (2) allocating $B(\rho)$ to $R(Q^F)$; and (3) resampling $R(Q^F)$ by considering the additional number of samples that have become available—in practice, this means extracting from $R(Q^F)$ further $\rho$ samples.

Let $S^*(Q_i)$ be the number of samples of a query $Q_i \in QWL$ satisfying the accuracy/privacy constraint. From the formal definitions of $E_Q(Q_i)$ (see Section 16.5), $I(Q_i)$, $\bar{I}(Q_i)$, and $E_I(Q_i)$ (see Section 16.6), and the satisfiability condition, it could be easily demonstrated that $S^*(Q_i)$ is given by the following formula: $S^*(Q_i) = \frac{1 - \Phi_{O_i}}{1 - \Phi_{P_i}} |Q_i|$.

Let $S_{eff}(Q^F)$ and $S_{eff}(Q^T)$ be the numbers of samples effectively extracted from $R(Q^F)$ and $R(Q^T)$, respectively, during the previous sampling phase. Note that $S_{eff}(Q^F) < S^*(Q^F)$ and $S_{eff}(Q^T) \geq S^*(Q^T)$. It is easy to prove that the number of samples to be moved from $Q^T$ to $Q^F$ such that $Q^F$ satisfies the accuracy/privacy constraint and $Q^T$ does not violate the constraint, denoted by $S_{mov}(Q^T, Q^F)$, is finally given by the following formula: $S_{mov}(Q^T, Q^F) = S_{eff}(Q^T) - S^*(Q^T)$, under the constraint $S_{mov}(Q^T, Q^F) \leq S_{eff}(Q^T) - S^*(Q^T)$.

Without going into detail, it is possible to demonstrate that, given (1) an arbitrary data cube $A$, (2) an arbitrary query workload $QWL$, (3) an arbitrary pair of thresholds $\Phi_O$ and $\Phi_P$, and (4) an arbitrary storage space $B$, it is not always possible to make $QWL$ satisfiable via the refinement process. From this evidence, our idea of using a best-effort approach makes sense perfectly.

### 16.9.4 The computeSynDataCube Algorithm

Main greedy algorithm computeSynDataCube is described by the pseudocode listed in Figure 16.3, wherein (1) allocateStorageSpace implements the proportional storage space allocation scheme (Equation 16.1), (2) sampleDataCube implements the sampling strategy, (3) check tests the satisfiability of the target query workload against the current representation of the synopsis data cube, and (4) refineSynDataCube is in charge of refining the current representation of the synopsis data cube.

```
computeSynDataCube(A,QWL,Φ_O,Φ_P,B,L_{A,QWL})
W ← allocateStorageSpace(A,QWL,B)
A' ← sampleDataCube(A,Φ_O,W)
while (check(A',QWL,Φ_O,Φ_P) && L_{A,QWL} > 0)
    (A',currSwapMemorySize) ← refineSynDataCube(A',QWL,Φ_O,Φ_P,W,L_{A,QWL})
    L_{A,QWL} ← L_{A,QWL} - currSwapMemorySize
return A'
```
