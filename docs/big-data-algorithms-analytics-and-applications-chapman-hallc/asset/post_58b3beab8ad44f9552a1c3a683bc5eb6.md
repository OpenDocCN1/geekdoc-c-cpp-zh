
there exist two queries \(Q_i\) and \(Q_j\) belonging to QWL such that \(R(Q_i) \cap R(Q_j) \neq \varnothing\). Given a query workload \(QWL = \{Q_0, Q_1, \ldots, Q_{|QWL|-1}\}\), the region set of QWL, denoted by \(R(QWL)\), is defined as the collection of regions of queries belonging to QWL, as follows: \(R(QWL) = \{R(Q_0), R(Q_1), \ldots, R(Q_{|QWL|-1})\}\).

## 16.4 DEALING WITH OVERLAPPING QUERY WORKLOADS

When overlapping query workloads are considered, we adopt a unifying strategy that allows us to handle nonoverlapping and overlapping query workloads in the same manner. As we will better discuss in Section 16.9, this approach involves several benefits in all the phases of our privacy-preserving OLAP technique. In this respect, given an overlapping query workload QWL, our aim is to obtain a nonoverlapping query workload QWL' from QWL such that QWL' is equivalent to QWL, that is, (1) QWL' provides the same information content as QWL, and (2) QWL can be totally reconstructed from QWL'. To this end, for each query \(Q_i\) of QWL without any intersection with other queries in QWL, we simply add \(Q_i\) to QWL' and remove \(Q_i\) from QWL. Contrary to this, for each query \(Q_i\) of QWL having at least one non-null intersection with other queries in QWL, we (1) extract from \(Q_i\) two new subsets of queries (defined next), denoted by \(\tau_1(Q_i)\) and \(\tau_2(Q_i)\); (2) add \(\tau_1(Q_i)\) and \(\tau_2(Q_i)\) to QWL'; and (3) remove \(Q_i\) from QWL. Specifically, \(\tau_1(Q_i)\) contains the subqueries of \(Q_i\) defined by intersection regions of \(Q_i\) and \(\tau_2(Q_i)\) contains the subqueries of \(Q_i\) defined by regions of \(Q_i\) obtained via prolonging the ranges of subqueries in \(\tau_1(Q_i)\) along the dimensions of \(Q_i\). As an example, consider Figure 16.1, where the nonoverlapping query workload QWL' extracted from an overlapping query workload \(QWL = \{Q_0, Q_1, Q_2\}\) is depicted. Here, we have the following:

- \(\tau_1(Q_0) = \{q_{0,0}\}\) — note that \(q_{0,0} \equiv Q_0 \cap Q_1\);
- \(\tau_2(Q_0) = \{q_{0,0}, q_{0,1}, q_{0,2}\}\);
- \(\tau_1(Q_1) = \{q_{1,0}, q_{2,0}\}\) — note that \(q_{2,0} \equiv Q_2 \cap Q_1\);
- \(\tau_2(Q_1) = \{q_{1,0}, q_{1,1}, q_{1,2}, q_{1,3}, q_{1,4}, q_{1,5}\}\);
- \(\tau_1(Q_2) = \{q_{2,0}\}\);
- \(\tau_2(Q_2) = \{q_{2,0}, q_{2,1}, q_{2,2}\}\).

Therefore, \(QWL' = \tau_1(Q_0) \cup \tau_2(Q_0) \cup \tau_1(Q_1) \cup \tau_2(Q_1) \cup \tau_1(Q_2) \cup \tau_2(Q_2)\).

## 16.5 METRICS FOR MODELING AND MEASURING ACCURACY

As accuracy metrics for answers to queries of the target query workload QWL, we make use of the relative query error between exact and approximate answers, which is a measure of quality for approximate query answering techniques in OLAP that is well recognized in literature (e.g., Reference 24).

Formally, given a query \(Q_k\) of QWL, we denote as \(A(Q_k)\) the exact answer to \(Q_k\) (i.e., the answer to \(Q_k\) evaluated over the original data cube \(A\)) and as \(\hat{A}(Q_k)\) the approximate answer to \(Q_k\) (i.e., the answer to \(Q_k\) evaluated over the synopsis data cube \(A'\)). Therefore, the relative query error \(E_O(Q_k)\) between \(A(Q_k)\) and \(\hat{A}(Q_k)\) is defined as follows:

\[
E_O(Q_k) = \frac{|A(Q_k) - \hat{A}(Q_k)|}{\max\{|A(Q_k)|, 1\}}.
\]

\(E_O(Q_k)\) can be extended to the whole query workload QWL, thus introducing the average relative query error \(E_O(QWL)\) that takes into account the contributions of relative query errors of all the queries \(Q_k\) in QWL, each of them weighted by the volume of the query, \(\|Q_k\|\), with respect to the whole volume of queries in QWL, that is, the volume of QWL, \(\|QWL\|\). \(\|QWL\|\) is defined as follows:

\[
\|QWL\| = \sum_{k=0}^{|QWL|-1} \|Q_k\|, \quad Q_k \in QWL.
\]

cell, thus inferring sensitive knowledge that is even more useful. Also, by exploiting OLAP hierarchies and the well-known ROLL-UP operator, it is possible to discover aggregations of ranges of data at higher degrees of such hierarchies. It should be noted that the singleton aggregation model, \(I(Q_k)\), indeed represents an instance of our privacy OLAP notion targeted to the problem of preserving the privacy of range-SUM queries (the focus of our chapter). As a consequence, \(I(Q_k)\) is essentially based on the conventional SQL aggregation operator AVG. Despite this, the underlying theoretical model we propose is general enough to be straightforwardly extended to deal with more sophisticated privacy OLAP notion instances, depending on the particular class of OLAP queries considered. Without loss of generality, given a query \(Q_k\) belonging to an OLAP query class \(C\), in order to handle the privacy preservation of \(Q_k\) we only need to define the formal expression of the related singleton aggregation \(I(Q_k)\) (like the previous one for the specific case of range-SUM queries). Then, the theoretical framework we propose works in the same way.

Secondly, we study how OLAP client applications can discover sensitive aggregations from the knowledge about approximate answers and, similarly to the previous case, from the knowledge about data cube and query metadata. Starting from the knowledge about the synopsis data cube \(A'\) and the knowledge about the answer to a given query \(Q_k\) belonging to the query workload QWL, it is possible to derive an estimation on \(I(Q_k)\), denoted by \(\hat{I}(Q_k)\), as follows:

\[
\hat{I}(Q_k) = \frac{\hat{A}(Q_k)}{S(Q_k)},
\]

such that \(S(Q_k)\) is the number of samples effectively extracted from \(R(Q_k)\) to compute \(A'\) (note that \(S(Q_k) \ll |Q_k|\)). The relative difference between \(I(Q_k)\) and \(\hat{I}(Q_k)\), named relative inference error and denoted by \(E_i(Q_k)\), gives us metrics for the privacy of \(\hat{A}(Q_k)\), which is defined as follows:

\[
E_i(Q_k) = \frac{|I(Q_k) - \hat{I}(Q_k)|}{\max\{|I(Q_k)|,1\}}.
\]

Indeed, while OLAP client applications are aware about the definition and metadata of both the target data cube and queries of the query workload QWL, the number of samples \(S(Q_k)\) (for each query \(Q_k\) in QWL) is not disclosed to them. As a consequence, in order to model this aspect of our framework, we introduce the user-perceived singleton aggregation, denoted by \(\hat{I}_u(Q_k)\), which is the effective singleton aggregation perceived by external applications based on the knowledge made available to them. \(\hat{I}_u(Q_k)\) is defined as follows:

\[
\hat{I}_u(Q_k) = \frac{\hat{A}(Q_k)}{\|Q_k\|}.
\]

Based on \(\hat{I}_u(Q_k)\), we derive the definition of the relative user-perceived inference error \(E_i^U(Q_k)\), as follows:

\[
E_i^U(Q_k) = \frac{|I(Q_k) - \hat{I}_u(Q_k)|}{\max\{|I(Q_k)|,1\}}.
\]

Since \(S(Q_k) \ll \|Q_k\|\), it is trivial to demonstrate that \(\hat{I}_u(Q_k)\) provides a better estimation of the singleton aggregation of \(Q_k\) than that provided by \(\hat{I}(Q_k)\), as \(\hat{I}_u(Q_k)\) is evaluated with respect to all the items contained within \(R(Q_k)\) (i.e., \(\|Q_k\|\)), whereas \(\hat{I}(Q_k)\) is evaluated with respect to the effective number of samples extracted from \(R(Q_k)\) [i.e., \(S(Q_k)\)]. In other words, \(\hat{I}_u(Q_k)\) is an upper bound for \(\hat{I}(Q_k)\). Therefore, in our framework, we consider \(\hat{I}(Q_k)\) to compute the synopsis data cube, whereas we consider \(\hat{I}_u(Q_k)\) to model inference issues on the OLAP client application side.

\(E_i^U(Q_k)\) can be extended to the whole query workload QWL by considering the average relative inference error \(\bar{E}_i(QWL)\) that takes into account the contributions of relative inference errors \(E_i(Q_k)\) of all the queries \(Q_k\) in QWL. Similarly to what was done for the average relative query error \(\bar{E}_Q(QWL)\), we model \(\bar{E}_i(QWL)\) as follows:

\[
\bar{E}_i(QWL)= \sum_{k=0}^{|QWL|-1} \frac{\|Q_k\|}{\|QWL\|} \cdot E_i(Q_k),
\]

that is,

\[
\bar{E}_i(QWL)= \sum_{k=0}^{|QWL|-1} \frac{\|Q_k\|}{\sum_{j=0}^{|QWL|-1}\|Q_j\|} \cdot \frac{|I(Q_k)-\hat{I}_u(Q_k)|}{\max\{|I(Q_k)|,1\}},
\]

under the constraint

\[
\sum_{k=0}^{|QWL|-1} \frac{\|Q_k\|}{\|QWL\|}=1.
\]

Note that, \(\bar{E}_i(QWL)\) is defined in dependence on \(\hat{I}_u(Q_k)\) rather than \(\hat{I}(Q_k)\). For the sake of simplicity, here and in the remaining part of the chapter, we assume \(E_i(Q_k) \equiv E_i^U(Q_k)\).

The concepts and definitions allow us to introduce the singleton aggregation privacy-preserving model \(\mathcal{X}=\langle I(\cdot), \hat{I}(\cdot), \hat{I}_u(\cdot)\rangle\), which is a fundamental component of the privacy-preserving OLAP framework we propose. \(\mathcal{X}\) properly realizes our privacy OLAP notion.

Given a query \(Q_k \in QWL\) against the target data cube \(A\), in order to preserve the privacy of \(Q_k\) under our privacy OLAP notion, we must maximize the inference error \(E_i(Q_k)\) while minimizing the query error \(E_Q(Q_k)\). While the definition of \(E_i(Q_k)\) can be reasonably considered as an invariant of our theoretical model, the definition of \(E_Q(Q_k)\) strictly depends on \(\mathcal{X}\). Therefore, given a particular class of OLAP queries \(\mathcal{C}\), in order to preserve the privacy of queries of kind \(\mathcal{C}\), we only need to appropriately define \(\mathcal{X}\). This nice amenity states that the privacy-preserving OLAP framework we propose is orthogonal to the particular class of queries considered and can be straightforwardly adapted to a large family of OLAP query classes.

## 16.7 ACCURACY AND PRIVACY THRESHOLDS

Similarly to related proposals that appeared in literature recently [20], in our framework, we introduce the accuracy threshold \(\Phi_Q\) and the privacy threshold \(\Phi_I\). \(\Phi_Q\) and \(\Phi_I\) give us an upper bound for the average query error \(\bar{E}_Q(QWL)\) and a lower bound for the average relative inference error \(\bar{E}_i(QWL)\) of a given query workload QWL against the synopsis data cube \(A'\). As stated in Section 16.1.1, \(\Phi_Q\) and \(\Phi_I\) allow us to meaningfully model and treat the accuracy/privacy constraint by means of rigorous mathematical/statistical models.

In our application scenario, \(\Phi_Q\) and \(\Phi_I\) are cooperatively negotiated by the data warehouse server and OLAP client applications. The issue of determining how to set these parameters is a nontrivial engagement. Intuitively enough, regarding the accuracy of answers, it is possible to (1) refer to the widely accepted query error threshold belonging to the interval [15, 20]% that, according to results of a plethora of research experiences in the context of approximate query answering techniques in OLAP (e.g., see Reference 44), represents the current state of the art and (2) use it as a baseline to trade off the parameter \(\Phi_Q\). Regarding the privacy of answers, there are no immediate guidelines to be considered since privacy-preserving techniques for advanced data management (like OLAP) are relatively new; hence, we cannot refer to any widely accepted threshold like what happens
