the clusters $l$ and $r$. The $\lambda_{klr}$ variables are used to define $|K|$ directed trees, one for each of the clusters in the graph.

This new model of the GMSTP has several nice properties, that can be used to develop exact solution procedures [142, 150], metaheuristic algorithms [76, 77], heuristic algorithms [143] and also heuristic and exact procedures for the PC-GMSTP [192, 54]. Among the described integer programming formulations, the local-global formulation is the most compact, in terms of number of variables and number of constraints.

Note that, although the presented formulations are defined for the GMSTP, these formulations are also valid for the PC-GMSTP. We only need to add the price of selecting a node from a cluster to the objective function.

The relationships between the polyhedrons, defined by the linear relaxations of the described GMSTP formulations, are depicted in the following figure:

![](bbox=[0.25, 0.35, 0.75, 0.6])

Figure 2.4. Relationship between the polyhedrons defined by the linear relaxations of the corresponding GMSTP formulations.

# ## 2.4 Approximation results for the GMSTP

Throughout this section, we will discriminate between so-called *positive results*, which establish the existence of some approximation algorithms, and so-called *negative results* which disprove the existence of good approximating results for some combinatorial optimization problems, under the assumption that $\mathcal{P} \neq \mathcal{NP}$.

We start with some basic results of approximation theory that follow the descriptions of Goemans [57] and Schuurman and Woeginger [183].