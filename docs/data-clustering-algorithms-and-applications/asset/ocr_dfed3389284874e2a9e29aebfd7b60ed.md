# 15.4.1.3 EDIT Distance

EDIT distance (ED) comes from the field of string comparison and measures the number of insert, delete, and replace operations that are needed to make two strings of possibly lengths identical to each other. Specifically, the EDIT distance between two strings $S_1$ and $S_2$ of length $m$ and $n$, respectively, is computed as follows:

+   (a) $D_{ED}(S_1, S_2) = m$, if $n = 0$
(b) $D_{ED}(S_1, S_2) = n$, if $m = 0$
(c) $D_{ED}(S_1, S_2) = D_{ED}(Rest(S_1), Rest(S_2))$, if $S_1 = S_2$
(d) $D_{ED}(S_1, S_2) = \min \begin{cases} D_{ED}(Rest(S_1), S_2) + 1 \ D_{ED}(S_1, Rest(S_2)) + 1 \end{cases}, \text{ otherwise}

Although ED for strings is a metric distance, the two ED-related distance measures DTW and Longest Common Sequence (LCSS) which will be described in the next section are not to follow the triangle inequality. Lei Chen [11] proposed two extensions to EDIT distance, namely Edit Distance with Real Penalty (ERP) to support local time shifting and Edit Distance on Real (EDR) to handle both local time shifting and noise in time series and trajectories. Both extensions have a high computational cost, so Chen proposes lower bounds, and indexing techniques to retrieve similar series more effectively. Both ERP and DTW can handle local time shifting and measure the distance between out-of-phase time series effectively. An advantage of ERP over DTW is that the former is a metric distance function, whereas the latter is not. DTW does not obey triangle inequality, and therefore, traditional access methods cannot be used to improve efficiency in DTW-applications.

# 15.4.1.4 Longest Common Sequence

The Longest Common Sequence (LCSS) is a variation of EDIT distance described in 15.4.1 [52]. LCSS allows time to stretch the time axis and does not match all elements, being less sensitive to outliers than $L_p$-norm and DTW. Specifically, the LCSS distance defined between two real-valued sequences $S_1$ and $S_2$ of length $m$ and $n$, respectively, is computed as follows:

+   (a) $D_{LCSS,\epsilon}(S_1, S_2) = 0$, if $n = 0$ or $m = 0$
(c) $D_{LCSS,\epsilon}(S_1, S_2) = 1 + D_{LCSS,\epsilon}(HEAD(S_1), HEAD(S_2))$ if $|S_1 - S_2| < \epsilon$ and $|n - m| < \delta$
(d) $\max \ \begin{cases} D_{LCSS,\epsilon}(HEAD(S_1), S_2) \ D_{LCSS,\epsilon}(S_1, HEAD(S_2)) \end{cases}, \text{ otherwise}

where $HEAD(S_1)$ is the subsequence $[S_{1,2}, \dots, S_{1,m-1}]$, $\delta$ is an integer that controls the maximum distance in the time axis between two matched elements, and $\epsilon$ is a real number $0 < \epsilon < 1$ that controls the maximum distance that two elements are allowed to be considered matched, as depicted in Figure 15.2.