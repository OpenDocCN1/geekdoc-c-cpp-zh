
## Chapter 5

## The Generalized Vehicle Routing Problem (GVRP)

Problems associated with determining optimal routes for vehicles from one or several depots to a set of locations/customers are known as Vehicle Routing Problems (VRPs). They have many practical applications in the field of distribution and logistics. A wide body of literature on the problem exists (for an extensive bibliography, see Laporte and Osman [104], Laporte [107] and the book edited by Ball et al. [6]).

Given a set of vehicles, a set of locations containing the depot location as well as the distance between each pair of locations, the VRP consists of finding the minimum cost tour for each vehicle, such that all locations are visited, and each vehicle returns to the depot. Because of the simplicity of the VRP, variations of the VRP, built on the basic VRP with extra features, proved most attractive to many researchers

- The Capacitated VRP [201], in which each vehicle has finite capacity and each location has a finite demand.
- The VRP with Time Windows [24, 190], in which there is a specified temporal window of opportunity in which to visit each location.
- The VRP with Multiple Depots [19], which generalizes the idea of a depot, in such a way that there are several depots from which each customer can be served.
- The Multi-Commodity VRP [180] in which each location has an associated demand for different commodities and each vehicle has a set of compartments in which only one commodity can be loaded. The problem then becomes that of deciding which commodities to place in which compartments, in order to minimize distance traveled.
- The Generalized Vehicle Routing Problem (GVRP) [48] is the problem of designing optimal delivery or collection routes, from a given depot to a number of predefined, mutually exclusive and exhaustive node-sets (clusters), subject to capacity restrictions. The GVRP can be viewed as a particular type of location-routing problem (see, e.g. Laporte [101], Nagy and Salhi [129]) for which several algorithms, mostly heuristics, exist.

In this section, we are concerned with the GVRP introduced by Ghiani and Improta [48]. They proposed solution procedure by transforming the GVRP into a capacitated arc routing problem, for which an exact algorithm and several approximate procedures are reported in literature.

### 5.1 Definition and complexity of the GVRP

Let G = (V, A) be a directed graph, with V = {0, 1, 2, ..., n} the set of vertices and A = {(i, j) | i, j ∈ V, i ≠ j} the set of arcs. A nonnegative cost cij is associated with each arc (i, j) ∈ A. The set of vertices (nodes) is partitioned into m + 1 mutually exclusive nonempty subsets, called clusters, V0, V1, ..., Vm. The cluster V0 has only one vertex 0, which represents the depot, and the remaining n nodes, belonging to the remaining m clusters, represent geographically dispersed customers. Each cluster Vk, k ∈ {1, ..., m} has a nonnegative demand denoted by qk and q0 = 0. Each customer i ∈ V \ {0} has a certain demand, denoted by di, and the total demand of each cluster can be satisfied via any of its nodes. There are K identical vehicles, each with a capacity Q.

The GVRP consists of finding the minimum total cost tours, starting and ending at the depot, such that each cluster is visited exactly once, the entering and leaving nodes of each cluster are the same and the sum of all the demands of any tour (route) does not exceed the capacity Q of the vehicle.

An illustrative scheme of the GVRP is shown in the next figure together with one feasible tour.

![](img/8ee31706d554c7b9e05caa9ab83aec83_139_0.png)

Figure 5.1. An example of a feasible solution of the GVRP.

The GVRP reduces to the classical Vehicle Routing Problem (VRP), when all the clusters are singletons, and to the Generalized Traveling Salesman Problem (GTSP), when K = 1 and Q = ∞.

The GVRP is NP-hard because it includes the generalized traveling salesman problem as a special case for \(K = 1\) and \(Q = \infty\).

Several real-world situations can be modeled as a GVRP. The post-box collection problem, described in Laporte et al. [102], becomes an asymmetric GVRP if more than one vehicle is required. Furthermore, the GVRP is able to model the distribution by sea of goods of a number of customers situated in an archipelago as in Philippines, New Zealand, Indonesia, Italy, Greece and Croatia. In this application, a number of potential harbors are selected for every island and a fleet of ships is required to visit exactly one harbor for every island.

Several applications of the GTSP (Laporte et al. [105]) may be extended naturally to the GVRP. In addition, several other situations can be modeled as a GVRP, including

- The Traveling Salesman Problem (TSP) with profits (Feillet et al. [36]).
- A number of Vehicle Routing Problem (VRP) extensions: the VRP with selective backhauls, the covering VRP, the periodic VRP, the capacitated general windy routing problem, etc.
- The design of tandem configurations for automated guided vehicles (Baldacci et al. [5]).

### 5.2 An efficient transformation of the GVRP into a capacitated arc routing problem

As we have seen in Section 3.2, transforming generalized network design problems into classical combinatorial optimization problems for which there exist efficient solution methods, seems to be a very promising approach.

In the case of the GVRP, Ghiani and Improta [48] showed that the problem can be transformed into a capacitated arc routing problem (CARP) and Baldacci et al. [5] proved that the reverse transformation is also valid.

Given an undirected graph \(G = (V, E)\), a depot located at a vertex \(v_0 \in V\) where a given fleet of vehicles are based, a subset \(R \subseteq E\) of edges called *required* if they are serviced by a vehicle, a nonnegative cost \(c_e\) associated with each edge \(e \in E\), and a positive demand \(d_e\) attached to each edge \(e \in R\) then the CARP consists of finding a set of shortest tours such that:

- each route starts and ends at the depot;
- each required edge is traversed at least once and is serviced by exactly one vehicle;
- the total demand serviced by any vehicle does not exceed vehicle capacity \(Q\).

CARP was introduced by Golden and Wong [55] and the problem finds many interesting applications including street garbage collection, postal delivery, winter gritting, routing of electric meter readers, etc. The same authors proved that the problem is strongly NP-hard. However, there exist efficient polynomial algorithms for solving special classes of the CARP for special structures of graph, demand or costs, see Assad et al. [4]. Due to the complexity of the CARP, several approximation procedures (see Assad and Golden [3], Eiselt et al. [33, 34]) and heuristic algorithms (see Chapelat et al. [17], Hertz et al. [74], etc.) to solve the problem have been developed.

In what follows, we will describe the efficient transformation of the GVRP into the CARP, introduced by Ghiani and Improta [48].

For the sake of simplicity, we assume that the GVRP is symmetric (i.e. cij = cji for all customers i, j ∈ V ). It is easy to show that the assumption mentioned is not restrictive and every GVRP can be transformed into an instance of our problem.

Assad and Golden [3] and Eiselt [33] proved that, in the case of every feasible solution of the CARP, every vertex is entered by an even number of copies of edges. For the sake of simplicity, the parity condition is formulated using the word “edge” instead of “copy of an edge”.

Let us denote by GR the subgraph induced by edges in R, by Nh the set of nodes of the h-th connected component of GR, h = 1, ..., m and by NR the set of nodes vi such that an edge (vi, vj) exists in R, i.e. VR = ∪h={1,...,m} Nh.

In this case, the transformation of the GVRP into a CARP is defined as follows:

- 1. A loop of “very expensive” required edges is created with the vertices v(h), ..., v(r(h))h of the cluster Vh for h = 1, ..., m, where r(h) denotes the number of customers belonging to cluster Vh. The following edges (v(i)h, v(i mod r(h))+1h) with i = 1, ..., r(h) and cost equal to a large positive number M, are inserted into R. In particular, if r(h) = 1, a required loop v(h)1, v(h)1 is introduced. These loops create m connected components of required edges. The remaining edges are non-required.
- 2. The non-required intra-cluster edges are removed.
- 3. The cost of each inter-cluster edge is increased by M/2 if an endpoint coincides with the depot, or by M otherwise.
- 4. Strictly positive demands, having sum equal to dh are assigned to the edges of the loop corresponding to Vh, h = 1, ..., m.

In the next figure, we illustrate the described transformation procedure and show the corresponding CARP solution on the transformed graph belonging to the feasible solution of the GVRP shown in Figure 5.1.

The following results hold:

Proposition 5.1. (Ghiani and Improta [48]) The optimal solution to the CARP on the transformed graph corresponds to the GVRP optimal solution on the original graph.
