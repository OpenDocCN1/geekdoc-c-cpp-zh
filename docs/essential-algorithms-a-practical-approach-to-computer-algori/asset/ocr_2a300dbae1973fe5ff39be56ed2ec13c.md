# Chapter 17  Complexity Theory 431

+   - Partitioning—Given a set of integers, find a way to divide the values into two sets with the same total value. (Variations use more than two sets.)

+   - Satisfiability (SAT)—Given a boolean expression containing variables, find an assignment of true and false to make the expression true. (The earlier section “Reductions” for more details).

+   - Shortest path—Given a graph (not necessarily planar) network, find the shortest path between two nodes.

+   - Subset sum—Given a set of integers, find a subset with a given total value.

+   - Three-partition problem—Given a set of integers, find a way to divide the set into triples that all have the same total value.

+   - Three-satisfiability (3SAT)—Given a boolean expression in conjunctive normal form, find an assignment of true and false to make the variables make the expression true. (The earlier section “3SAT” for more details).

+   - Traveling salesman problem (TSP)—Given a list of cities and the distances between them, find the shortest possible route that visits all the cities and returns to the starting city.

+   - Unbounded knapsack—Similar to the knapsack problem, except that you can select any item multiple times.

+   - Vehicle routing—Given a set of customer locations and a fleet of vehicles, find the most efficient routes for the vehicles to visit all the customer locations. (This problem has many variations. For example, the route might require delivery only or pick and delivery, items might need to be delivered in last-picked-up-next-delivered order, vehicles might have differing capacities, and so on.)

+   - Vertex cover—Given a graph, find a minimal set of vertices that every link in the graph touches one of the selected vertices.

# Summary

This chapter provided a brief introduction to complexity theory. It explained what complexity classes are and described some of the more important ones, including P and NP. You don't necessarily need to know the fine details of every complexity class, but you should certainly understand P and NP. You should also be familiar with perhaps the most profound question in computer science: Does P equal NP?

Later sections in this chapter explain how to use polynomial time reductions to show that one problem is at least as hard as another. Those sorts of reductions are useful for studying complexity theory, but the concept of reducing one