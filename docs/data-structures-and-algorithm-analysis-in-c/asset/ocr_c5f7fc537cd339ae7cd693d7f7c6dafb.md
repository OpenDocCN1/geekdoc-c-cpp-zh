![](bbox=[0.05, 0.08, 0.95, 0.3])

Figure 9.47 Graphs after two units of flow added along s,b,d,a,c,t using correct algorithm

There is no augmenting path in this graph, so the algorithm terminates. Note that the same result would occur if at Figure 9.46, the augmenting path s, a, c, t, was chosen which allows one unit of flow, because then a subsequent augmenting path could be found.

It is easy to see that if the algorithm terminates, then it must terminate with a maximum flow. Termination implies that there is no path from s to t in the residual graph. So cut the residual graph, putting the vertices reachable from s on one side and the unreachables (which include t) on the other side. Figure 9.48 shows the cut. Clearly any edges in the original graph G that cross the cut must be saturated; otherwise, there would be residual flow remaining on one of the edges, which would then imply an edge that crosses the cut (in the wrong disallowed direction) in Gr. But that means that the flow in G is exactly equal to the capacity of a cut in G; hence, we have a maximum flow.

If the edge costs in the graph are integers, then the algorithm must terminate; each augmentation adds a unit of flow, so we eventually reach the maximum flow, though there

![](bbox=[0.05, 0.7, 0.95, 0.88])

Figure 9.48 The vertices reachable from s in the residual graph form one side of a cut; the unreachables form the other side of the cut