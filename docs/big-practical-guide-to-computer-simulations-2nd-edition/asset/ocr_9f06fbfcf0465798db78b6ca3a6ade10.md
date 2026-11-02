to a component, no further component identification procedure is started. Finally node 5 is encountered. It is the seed of a new component with ID 1. Since it has no neighbors, i.e., the condition in line 23 of the code is immediately FALSE, no other nodes will be added to the component. At this point, the main loop terminates and the full component identification procedure is completed.

![](bbox=[0.07, 0.28, 0.98, 0.78])

Fig. 6.29 Average size S of the largest component of a random graphs, normalized by the number n of nodes, as a function of the average connectivity c. Here, n = 10000. The average was taken over 1000 independent random graph instances for each value of c. The lines are guides to the eyes only.

As an example application of how the determination of components is used in conjunction with graph models, we study Erdős–Rényi (ER) random graphs. These are graphs, which here have n nodes and m edges, which connect randomly and independently chosen pairs of nodes. Thus,