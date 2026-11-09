# UVa 410 - Station Balance

Given \(1 \le C \le 5\) chambers which can store 0, 1, or 2 specimens, \(1 \le S \le 2C\) specimens, and \(M\): a list of mass of the \(S\) specimens, determine in which chamber we should store each specimen in order to minimize IMBALANCE. See Figure 3.3 for visual explanation.

\(A = (\sum_{j=1}^{S} M_j)/C\), i.e. \(A\) is the average of all mass over \(C\) chambers.

\(\mathrm{IMBALANCE} = \sum_{i=1}^{C} |X_i - A|\), i.e. sum of differences between the mass in each chamber w.r.t \(A\).

where \(X_i\) is the total mass of specimens in chamber \(i\).

![](bbox=[0.263, 0.241, 0.716, 0.388])

Figure 3.3: Visualization of UVa 410 - Station Balance

This problem can be solved using a greedy algorithm. But first, we have to make several observations. If there exists an empty chamber, at least one chamber with 2 specimens must be moved to this empty chamber! Otherwise the empty chambers contribute too much to IMBALANCE! See Figure 3.4.

![](bbox=[0.263, 0.535, 0.719, 0.619])

Figure 3.4: UVa 410 - Observation 1

Next observation: If \(S > C\), then \(S-C\) specimens must be paired with one other specimen already in some chambers. The Pigeonhole principle! See Figure 3.5.

![](bbox=[0.263, 0.714, 0.718, 0.786])

Figure 3.5: UVa 410 - Observation 2

Now, the key insight that can simplify the problem is this: If \(S < 2C\), add dummy \(2C-S\) specimens with mass 0. For example, \(C = 3, S = 4, M = \{5, 1, 2, 7\} \Rightarrow C = 3, S = 6, M = \{5, 1, 2, 7, 0, 0\}\). Then, sort these specimens based on their mass such that \(M_1 \le M_2 \le \ldots \le M_{2C-1} \le M_{2C}\). In this example, \(M = \{5, 1, 2, 7, 0, 0\} \rightarrow \{0, 0, 1, 2, 5, 7\}\).