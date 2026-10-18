# Bandwidth Management in Cellular Networks 143

\begin{tabular}{cccccccc}
c'(a_i, a_j) & a_0 & a_1 & a_2 & a_3 & a_4 & a_5 & a_6 \\
a_0 & 7 & 1 & 1 & 1 & 1 & 1 & 1 \\
a_1 & 1 & 7 & 1 & 1 & 1 & 1 & 1 \\
a_2 & 1 & 1 & 7 & 1 & 1 & 1 & 1 \\
a_3 & 1 & 1 & 1 & 7 & 1 & 1 & 1 \\
a_4 & 1 & 1 & 1 & 1 & 7 & 1 & 1 \\
a_5 & 1 & 1 & 1 & 1 & 1 & 7 & 1 \\
a_6 & 1 & 1 & 1 & 1 & 1 & 1 & 7 \\
\end{tabular}

We now apply step 1 of the algorithm Derive-Assignment(P, P') to find the as-
assignment for P from the solution to P' in Table 3.13. The derived assignment for P
is shown in Table 3.14. Note that the same set of channels assigned to node N(Y(0))
has also been assigned to all the cells in Y(0) = {2, 6, 11, 19}. This assignment
leaves four blocked calls (15 - 11 = 4) in cell 16 and at the same time it also
produces many redundant channels in other cells (e.g., cell 2 has 40 redundant chan-
nels).

We now apply step 2 of the algorithm Derive-Assignment(P, P'), to get the as-
assignment as shown in Table 3.15. Note in the assignment of Table 3.14 the four
blocked calls in cell 16. However, MFAR operation finds that channels 0, 5, 10, and
15 can be assigned to cell 16 if the assignment of channels 0, 5, 10, and 15 from
cells 2 and 19 is undone. Note that there are more than four redundant channels in
both cells 2 and 19. The assignments of channels 0, 5, 10 and 15 in cell 16 have been
underlined and those of cells 2 and 19 have been marked by asterisks (*).