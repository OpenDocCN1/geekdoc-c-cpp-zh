
## 10.5. SOFTWARE PIPELINING

**METHOD:** Execute the program in Fig. 10.26.

```c
main() {
    T₀ = maxⱼ [ (∑ₙ,ᵢ RTₙ(i,j)) / rᵢ ];
    for (T = T₀, T₀ + 1, …, until all nodes in N are scheduled) {
        RT = an empty reservation table with T rows;
        for (each n in N in prioritized topological order) {
            s₀ = maxₚ→ₙ in E (S(p) + dₚ);
            for (s = s₀, s₀ + 1, …, s₀ + T − 1)
                if (NodeScheduled(RT,T,n,s)) break;
            if (n cannot be scheduled in RT) break;
        }
    }
}

NodeScheduled(RT,T,n,s) {
    RT′ = RT;
    for (each row i in RTₙ)
        RT′[(s + i) mod T] = RT′[(s + i) mod T] + RTₙ[i];
    if (for all i, RT′(i) ≤ R) {
        RT = RT′;
        S(n) = s;
        return true;
    }
    else return false;
}
```

Figure 10.26: Software-pipelining algorithm for acyclic graphs

Algorithm 10.19 software pipelines acyclic data-dependence graphs. The algorithm first finds a bound on the initiation interval, T₀, based on the resource requirements of the operations in the graph. It then attempts to find a software-pipelined schedule starting with T₀ as the target initiation interval. The algorithm repeats with increasingly larger initiation intervals if it fails to find a schedule.

The algorithm uses a list-scheduling approach in each attempt. It uses a modular resource-reservation RT to keep track of the resource commitment in the steady state. Operations are scheduled in topological order so that the data dependences can always be satisfied by delaying operations. To schedule an operation, it first finds a lower bound s₀ according to the data-dependence constraints. It then invokes NodeScheduled to check for possible resource conflicts in the steady state. If there is a resource conflict, the algorithm tries to schedule the operation in the next clock. If the operation is found to conflict for $T$ consecutive clocks, because of the modular nature of resource-conflict detection, further attempts are guaranteed to be futile. At that point, the algorithm considers the attempt a failure, and another initiation interval is tried.

The heuristics of scheduling operations as soon as possible tends to minimize the length of the schedule for an iteration. Scheduling an instruction as early as possible, however, can lengthen the lifetimes of some variables. For example, loads of data tend to be scheduled early, sometimes long before they are used. One simple heuristic is to schedule the dependence graph backwards because there are usually more loads than stores.

### 10.5.8 Scheduling Cyclic Dependence Graphs

Dependence cycles complicate software pipelining significantly. When scheduling operations in an acyclic graph in topological order, data dependences with scheduled operations can impose only a lower bound on the placement of each operation. As a result, it is always possible to satisfy the data-dependence constraints by delaying operations. The concept of “topological order” does not apply to cyclic graphs. In fact, given a pair of operations sharing a cycle, placing one operation will impose both a lower and upper bound on the placement of the second.

Let $n_1$ and $n_2$ be two operations in a dependence cycle, $S$ be a software-pipeline schedule, and $T$ be the initiation interval for the schedule. A dependence edge $n_1 \to n_2$ with label $\langle\delta_1,d_1\rangle$ imposes the following constraint on $S(n_1)$ and $S(n_2)$:

$$(\delta_1 \times T) + S(n_2) - S(n_1) \ge d_1.$$

Similarly, a dependence edge $n_1 \to n_2$ with label $\langle\delta_2,d_2\rangle$ imposes constraint

$$(\delta_2 \times T) + S(n_1) - S(n_2) \ge d_2.$$

Thus,

$$S(n_1) + d_1 - (\delta_1 \times T) \le S(n_2) \le S(n_1) - d_2 + (\delta_2 \times T).$$

A *strongly connected component* (SCC) in a graph is a set of nodes where every node in the component can be reached by every other node in the component. Scheduling one node in an SCC will bound the time of every other node in the component both from above and from below. Transitively, if there exists a path $p$ leading from $n_1$ to $n_2$, then

$$S(n_2) - S(n_1) \ge \sum_{e \in p}(d_e - (\delta_e \times T)) \qquad (10.1)$$

Observe that

- Around any cycle, the sum of the δ's must be positive. If it were 0 or negative, then it would say that an operation in the cycle either had to precede itself or be executed at the same clock for all iterations.
- The schedule of operations within an iteration is the same for all iterations; that requirement is essentially the meaning of a “software pipeline.” As a result, the sum of the delays (second components of edge labels in a data-dependence graph) around a cycle is a lower bound on the initiation interval $T$.

From these two points, if path $p$ is a cycle, then for any feasible initiation interval $T$, the value of the right side of Equation (10.1) is negative or zero. As a result, the strongest constraints on the placement of nodes is obtained from the *simple* paths — those paths that contain no cycles.

Thus, for each feasible $T$, computing the transitive effect of data dependences on each pair of nodes is equivalent to finding the length of the longest simple path from the first node to the second. Moreover, since cycles cannot increase the length of a path, we can use a simple dynamic-programming algorithm to find the longest paths without the “simple-path” requirement, and be sure that the resulting lengths will also be the lengths of the longest simple paths (see Exercise 10.5.7).

![](img/2a44b9071782fade81f3050c3b718341_756_0.png)

Figure 10.27: Dependency graph and resource requirement in Example 10.20

**Example 10.20:** Figure 10.27 shows a data-dependence graph with four nodes *a, b, c, d*. Attached to each node is its resource-reservation table; attached to each edge is its iteration difference and delay. Assume for this example that the target machine has one unit of each kind of resource. Since there are three uses of the first resource and two of the second, the initiation interval must be no less than 3 clocks. There are two SCC’s in this graph: the first is a trivial component consisting of the node *a* alone, and the second consists of nodes *b, c,* and *d*. The longest cycle, *b, c, d, b*, has a total delay of 3 clocks connecting nodes that are 1 iteration apart. Thus, the lower bound on the initiation interval provided by data-dependence cycle constraints is also 3 clocks.

Placing any of $b$, $c$, or $d$ in a schedule constrains all the other nodes in the component. Let $T$ be the initiation interval. Figure 10.28 shows the transitive dependences. Part (a) shows the delay and the iteration difference $\delta$, for each edge. The delay is represented directly, but $\delta$ is represented by “adding” to the delay the value $-\delta T$.

Figure 10.28(b) shows the length of the longest simple path between two nodes, when such a path exists; its entries are the sums of the expressions given by Fig. 10.28(a), for each edge along the path. Then, in (c) and (d), we see the expressions of (b) with the two relevant values of $T$, that is 3 and 4, substituted for $T$. The difference between the schedule of two nodes $S(n_2)-S(n_1)$ must be no less than the value given in entry $(n_1,n_2)$ in each of the tables (c) or (d), depending on the value of $T$ chosen.

For instance, consider the entry in Fig. 10.28 for the longest (simple) path from $c$ to $b$, which is $2-T$. The longest simple path from $c$ to $b$ is $c\to d\to b$. The total delay is 2 along this path, and the sum of the $\delta$’s is 1, representing the fact that the iteration number must increase by 1. Since $T$ is the time by which each iteration follows the previous, the clock at which $b$ must be scheduled is at least $2-T$ clocks after the clock at which $c$ is scheduled. Since $T$ is at least 3, we are really saying that $b$ may be scheduled $T-2$ clocks before $c$, or later than that clock, but not earlier.

Notice that considering nonsimple paths from $c$ to $b$ does not produce a stronger constraint. We can add to the path $c\to d\to b$ any number of iterations of the cycle involving $d$ and $b$. If we add such cycles, we get a path length of $2-T+k(3-T)$, since the total delay along the path is 3, and the sum of the $\delta$’s is 1. Since $T\geq 3$, this length can never exceed $2-T$; i.e., the strongest lower bound on the clock of $b$ relative to the clock of $c$ is $2-T$, the bound we get by considering the longest simple path.

For example, from entries $(b,c)$ and $(c,b)$, we see that

$$S(c)-S(b)\geq 1$$
$$S(b)-S(c)\geq 2-T.$$

That is,

$$S(b)+1\leq S(c)\leq S(b)-2+T.$$

If $T=3$,

$$S(b)+1\leq S(c)\leq S(b)+1.$$

Put equivalently, $c$ must be scheduled one clock after $b$. If $T=4$, however,

$$S(b)+1\leq S(c)\leq S(b)+2.$$

That is, $c$ is scheduled one or two clocks after $b$.

Given the all-points longest path information, we can easily compute the range where it is legal to place a node due to data dependences. We see that there is no slack in the case when $T=3$, and the slack increases as $T$ increases. $\square$
