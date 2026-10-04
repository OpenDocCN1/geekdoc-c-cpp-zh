# 4.8. IMPROVING INTERPROCEDURAL DECLASSIFICATION

![](bbox=[0.243, 0.126, 0.756, 0.281])

Figure 4.13: SDG for Figure 4.11 with summary declassification nodes

mental idea is to insert a new "summary" declassification node into the summary edge, which represents the effect of declassifications on paths in the procedure body.

Thus the example $x - y$

The constraints on $R(d)$ and $P(d)$ are chosen such that any legal flow through the procedure body is also a legal flow through $x \rightarrow d \rightarrow y$. In particular, if there is a declassification path from $x'$ to $y'$, there must not be a summary declassification node, as information flow might be transitive in that case. It is not trivial to determine $R(d)$ and $P(d)$ such that precision is maximized and correctness is maintained, as we will see later. However, these values have been fixed; 7 proceeds as usual.

Figure 4.13 shows the SDG with declassification nodes for the example in Figure 4.12. The actual-nodes 4 and 8 are connected to their corresponding node 15 with parameter-in edges. The formal-out node 15 is connected to corresponding actual-nodes 6 and 10 with parameter-out edges. The call nodes 3 and 7 are connected to the called procedure at its entry node with 12. The actual-in nodes 4 and 8 are connected via summary and declassification nodes 5 and 9 to the actual-out nodes 6 and 10. This Figure contains only one declassification at node 15 ($R(15) = confidential, P(15) = public$), for the path between node 15 and 15 the summary declassification nodes 5 and 9 will be set to $R(5) = R(9) = confidential$ and $P(5) = P(9) = \perp$. (The algorithm for this will be presented in the next section.)

Exploiting the summary declassification nodes, algorithm 7 will determine that node 1 is not in the backward slice of node 11 and thus cannot influence node 11, and $b)$ $confidential = P(8) \leq S(8) \leq S(8) \leq R(8) = confidential$ and $\perp = P(9) \leq S(9) \leq S(10) \leq R(11) = public$, no security violation is found in *check*. In the second slicing phase, there is no violation either: $S(13) \leq S(14) \leq R(15) = confidential$ and $public = P(15) \leq S(10) \leq R(11) =$

117