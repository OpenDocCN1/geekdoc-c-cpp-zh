
We must assume that any pair of `*(p++)` and `*(q++)` accesses may refer to the same memory location. Thus, all the reads and writes must execute in the original sequential order. Assuming that the target machine has the same characteristics as that described in Example 10.12, the data-dependence edges for this code are as shown in Fig. 10.25. Note, however, that we ignore the loop-control instructions that would have to be present, either computing and testing i, or doing the test based on the value of R1 or R2. □

```
//  R1, R2 = q, p
//  R3 = c
```

![](img/a29d16e454785bb105e96ef448ac07f6_752_0.png)

Figure 10.25: Data-dependence graph for Example 10.18

The iteration difference between related operations can be greater than one, as shown in the following example:

```
for (i = 2; i < n; i++)
    A[i] = B[i] + A[i-2];
```

Here the value written in iteration *i* is used two iterations later. The dependence edge between the store of *A[i]* and the load of *A[i − 2]* thus has a difference of 2 iterations.

The presence of data-dependence cycles in a loop imposes yet another limit on its execution throughput. For example, the data-dependence cycle in Fig. 10.25 imposes a delay of 4 clock ticks between load operations from consecutive iterations. That is, loops cannot execute at a rate faster than one iteration every 4 clocks.

The initiation interval of a pipelined loop is no smaller than

$$\max_{c\text{ a cycle in }G}\left\lceil\frac{\sum_{e\text{ in }c}d_e}{\sum_{e\text{ in }c}\delta_e}\right\rceil$$

clocks.

In summary, the initiation interval of each software-pipelined loop is bounded by the resource usage in each iteration. Namely, the initiation interval must be no smaller than the ratio of units needed of each resource and the units

METHOD: Execute the program in Fig. 10.26. □

```
main() {
    T0 = max_j [ Σ_{n,i} RT_n(i,j) / r_j ];
    for (T = T0, T0 + 1, ... , until all nodes in N are scheduled) {
        RT = an empty reservation table with T rows;
        for (each n in N in prioritized topological order) {
            s0 = max_{c=p→n in E} (S(p) + d_c);
            for (s = s0, s0 + 1, ... , s0 + T − 1)
                if (NodeScheduled(RT, T, n, s)) break;
            if (n cannot be scheduled in RT) break;
        }
    }
}

NodeScheduled(RT, T, n, s) {
    RT' = RT;
    for (each row i in RT_n)
        RT'[(s + i) mod T] = RT'[(s + i) mod T] + RT_n[i];
    if (for all i, RT'(i) ≤ R) {
        RT = RT';
        S(n) = s;
        return true;
    }
    else return false;
}
```

Figure 10.26: Software-pipelining algorithm for acyclic graphs

Algorithm 10.19 software pipelines acyclic data-dependence graphs. The algorithm first finds a bound on the initiation interval, T0, based on the resource requirements of the operations in the graph. It then attempts to find a software-pipelined schedule starting with T0 as the target initiation interval. The algorithm repeats with increasingly larger initiation intervals if it fails to find a schedule.

The algorithm uses a list-scheduling approach in each attempt. It uses a modular resource-reservation RT to keep track of the resource commitment in the steady state. Operations are scheduled in topological order so that the data dependences can always be satisfied by delaying operations. To schedule an operation, it first finds a lower bound s0 according to the data-dependence constraints. It then invokes NodeScheduled to check for possible resource conflicts in the steady state. If there is a resource conflict, the algorithm tries to schedule the operation in the next clock. If the operation is found to conflict for $T$ consecutive clocks, because of the modular nature of resource-conflict detection, further attempts are guaranteed to be futile. At that point, the algorithm considers the attempt a failure, and another initiation interval is tried.

The heuristic of scheduling operations as soon as possible tends to minimize the length of the schedule for an iteration. Scheduling an instruction as early as possible, however, can lengthen the lifetimes of some variables. For example, loads of data tend to be scheduled early, sometimes long before they are used. One simple heuristic is to schedule the dependence graph backwards because there are usually more loads than stores.

### 10.5.8 Scheduling Cyclic Dependence Graphs

Dependence cycles complicate software pipelining significantly. When scheduling operations in an acyclic graph in topological order, data dependences with scheduled operations can impose only a lower bound on the placement of each operation. As a result, it is always possible to satisfy the data-dependence constraints by delaying operations. The concept of “topological order” does not apply to cyclic graphs. In fact, given a pair of operations sharing a cycle, placing one operation will impose both a lower and upper bound on the placement of the second.

Let $n_1$ and $n_2$ be two operations in a dependence cycle, $S$ be a software-pipeline schedule, and $T$ be the initiation interval for the schedule. A dependence edge $n_1 \to n_2$ with label $\langle \delta_1, d_1\rangle$ imposes the following constraint on $S(n_1)$ and $S(n_2)$:

$$(\delta_1 \times T) + S(n_2) - S(n_1) \ge d_1.$$

Similarly, a dependence edge $n_1 \to n_2$ with label $\langle \delta_2, d_2\rangle$ imposes constraint

$$(\delta_2 \times T) + S(n_1) - S(n_2) \ge d_2.$$

Thus,

$$S(n_1) + d_1 - (\delta_1 \times T) \le S(n_2) \le S(n_1) - d_2 + (\delta_2 \times T).$$

A *strongly connected component* (SCC) in a graph is a set of nodes where every node in the component can be reached by every other node in the component. Scheduling one node in an SCC will bound the time of every other node in the component both from above and from below. Transitively, if there exists a path $p$ leading from $n_1$ to $n_2$, then

$$S(n_2) - S(n_1) \ge \sum_{e\in p}(d_e - (\delta_e \times T)) \qquad (10.1)$$

Observe that

- Around any cycle, the sum of the δ’s must be positive. If it were 0 or negative, then it would say that an operation in the cycle either had to precede itself or be executed at the same clock for all iterations.
- The schedule of operations within an iteration is the same for all iterations; that requirement is essentially the meaning of a “software pipeline.” As a result, the sum of the delays (second components of edge labels in a data-dependence graph) around a cycle is a lower bound on the initiation interval T.

From these two points, if path p is a cycle, then for any feasible initiation interval T, the value of the right side of Equation (10.1) is negative or zero. As a result, the strongest constraints on the placement of nodes are obtained from the simple paths — those paths that contain no cycles.

Thus, for each feasible T, computing the transitive effect of data dependences on each pair of nodes is equivalent to finding the length of the longest simple path from the first node to the second. Moreover, since cycles cannot increase the length of a path, we can use a simple dynamic-programming algorithm to find the longest paths without the “simple-path” requirement, and be sure that the resulting lengths will also be the lengths of the longest simple paths (see Exercise 10.5.7).

![](img/a29d16e454785bb105e96ef448ac07f6_756_0.png)

Figure 10.27: Dependence graph and resource requirement in Example 10.20

Example 10.20: Figure 10.27 shows a data-dependence graph with four nodes a, b, c, d. Attached to each node is its resource-reservation table; attached to each edge is its iteration difference and delay. Assume for this example that the target machine has one unit of each kind of resource. Since there are three uses of the first resource and two of the second, the initiation interval must be no less than 3 clocks. There are two SCC’s in this graph: the first is a trivial component consisting of the node a alone, and the second consists of nodes b, c, and d. The longest cycle, b, c, d, b, has a total delay of 3 clocks connecting nodes that are 1 iteration apart. Thus, the lower bound on the initiation interval provided by data-dependence cycle constraints is also 3 clocks.
