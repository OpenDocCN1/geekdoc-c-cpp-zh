# Table 9.4 An Example of Order Crossover

| Parents | Other Parent Template | Children |
|---|---|---|
| p1: 2 1 3¹ | 9 5 4 | 2⁸ 7 6 | 6 8 7 1 3 2 from p2 | c1: 6 8 7¹ | 9 5 4 | 2¹ 3 2 |
| p2: 5 3 2 | 6 8 9 | 7 1 4 | 5 4 7 2 1 3 from p1 | c2: 5 4 7 | 6 8 9 | 2 1 3 |

values in the other parent, omitting values that are not already present, in the order in which those values appear in the other parent, starting from the other parent’s pick. These values are called its **template**. Table 9.4 illustrates this. Notice that child c1 has value [9 5 4]" for the pick just as parent p1. The pick for parent p2 is [6 8 9]. The template from this parent is constructed by starting at site 6 and in sequence listing all cities that are not in [9 5 4]. This is done with wrap-around. So the template is [6 8 7 1 3 2]. These values are copied in order into the non-pick area of child c2.

If the graph is not complete, we would need to check whether the new child represents an actual tour, and if it does not reject the crossover.

As far as mutations, we cannot just mutate a site by changing a given vertex to another vertex because a vertex would then appear twice. We could mutate by interchanging two vertices or reversing the order of a subset of vertices. However, if the graph is not complete, we must make certain that the result represents an actual tour.

# 9.2.3.2 Nearest Neighbor Crossover

The **Nearest Neighbor Algorithm (NNA)** for TSP is an example of a greedy algorithm. A greedy algorithm arrives at a solution by making a sequence of choices, each of which simply looks best at the moment. NNA starts with an arbitrary vertex to initiate a tour, and then repeatedly adds the closest unvisited vertex to the partial tour until a tour is completed. NNA assumes the graph is complete; otherwise it may not result in a tour. The algorithm follows.

```
**Algorithm 9.2** Nearest_Neighbor

**Procedure** _Generate_Tour(**var** _tour_);
_tour_ = [_v_i] where _v_i is chosen at random;
**repeat**
add unvisited vertex to _tour_
that is closest to current last vertex in _tour_;
**until** all vertices are in _tour_;
```

Figure 9.3 (a) shows an instance of TSP where the undirected edges represent that there is a directed edge with the given weight in both directions, Figure 9.3 (b) shows the shortest tour, Figure 9.3 (c) shows the tour obtained