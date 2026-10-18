```
(d) $D_{ED}(S_1,S_2) = \min \begin{cases} D_{ED}(\text{Rest}(S_1),\text{Rest}(S_2)) + 1 \\ D_{ED}(\text{Rest}(S_1),S_2) + 1 \\ D_{ED}(S_1,\text{Rest}(S_2)) + 1. \end{cases}$ otherwise
```

Although ED for strings is proven to be a metric distance, the two ED-related time series distance measures DTW and Longest Common Subsequence (LCSS) that will be described in the next subsection are proven not to follow the triangle inequality. Lei Chen [7] proposed two extensions to EDIT distance, namely Edit distance with Real Penalty (ERP) to support local time shifting and Edit Distance on Real sequence (EDR) to handle both local time shifting and noise in time series and trajectories. Both extensions have a high computational cost, so Chen proposes various lower bounds, indexing and pruning techniques to retrieve similar time series more efficiently. Both ERP and DTW can handle local time shifting and measure the distance between two out-of-phase time series effectively. An advantage that ERP has over DTW is that the former is a metric distance function, whereas the latter is not. DTW does not obey triangle inequality, and therefore traditional index methods cannot be used to improve efficiency in DTW-based applications. On the other hand, ERP is proven to be a metric distance function [7], and therefore traditional access methods can be used. EDR, as a distance function, proves to be more robust than Euclidean distance, DTW, and ERP and more accurate than LCSS as will be described in the next subsection. EDR is not a metric, thus the author proposes three non-constraining pruning techniques (mean value Q-grams, near triangle inequality, and histograms) to improve retrieval efficiency.

# 13.3.4 Longest Common Subsequence (LCSS)

The Longest Common Subsequence (LCSS) distance is a variation of EDIT distance described in 13.3.3 [37]. LCSS allows time series to stretch in the time axis and does not match all elements, thus being less sensitive to outliers than $L_p$-norms and DTW. Specifically, the LCSS distance between two real-valued sequences $S_1$ and $S_2$ of length $m$ and $n$ respectively is computed as follows:

+   (a) $LCSS_{\delta,\epsilon}(S_1,S_2) = 0$, if $n = 0$ or $m = 0$

+   (c) $LCSS_{\delta,\epsilon}(S_1,S_2) = 1 + LCSS_{\delta,\epsilon}(\text{HEAD}(S_1),\text{HEAD}(S_2))$ if $|S_{1,m} - S_{2,m}| < \epsilon$ and $|m - n| \le \delta$

+   (d) $\max \begin{cases} LCSS_{\delta,\epsilon}(\text{HEAD}(S_1),S_2) \\ LCSS_{\delta,\epsilon}(S_1,\text{HEAD}(S_2)) \end{cases}$, otherwise

where $\text{HEAD}(S_1)$ is the subsequence $[S_{1,1},S_{1,2},...,S_{1,m-1}]$, $\delta$ is an integer that controls the maximum distance in the time axis between two matched elements, and $\varepsilon$ is a real number $0 < \varepsilon < 1$ that controls the maximum distance that two elements are allowed to have to be considered matched.

Apart from being used in time series classification, LCSS distance is often used in domains like speech recognition and text pattern mining. Its main drawback is that it often is needed to scale are transform the one sequence to the other. A detailed study of LCSS variations and algorithms is presented in [5].

# 13.4 k-NN

The well-known and popular traditional $k$-NN classifier is not different when it comes to time series classification. The most challenging part in this setting is again the choice of the distance or