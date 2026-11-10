
Thus, an operation *n* in the *i*th iteration, counting from 0, is executed at clock *i* × *T* + *S*(*n*). Like all the other scheduling problems, software pipelining has two kinds of constraints: resources and data dependences. We discuss each kind in detail below.

### Modular Resource Reservation

Let a machine's resources be represented by R = [r₁, r₂, …], where rᵢ is the number of units of the *i*th kind of resource available. If an iteration of a loop requires nᵢ units of resource *i*, then the average initiation interval of a pipelined loop is at least maxᵢ(nᵢ/rᵢ) clock cycles. Software pipelining requires that the initiation intervals between any pair of iterations have a constant value. Thus, the initiation interval must have at least maxᵢ[nᵢ/rᵢ] clocks. If maxᵢ(nᵢ/rᵢ) is less than 1, it is useful to unroll the source code a small number of times.

**Example 10.17:** Let us return to our software-pipelined loop shown in Fig. 10.20. Recall that the target machine can issue one load, one arithmetic operation, one store, and one loop-back branch per clock. Since the loop has two loads, two arithmetic operations, and one store operation, the minimum initiation interval based on resource constraints is 2 clocks.

![](img/2a44b9071782fade81f3050c3b718341_750_0.png)

Figure 10.24: Resource requirements of four consecutive iterations from the code in Example 10.13

Figure 10.24 shows the resource requirements of four consecutive iterations across time. More resources are used as more iterations get initiated, culminating in maximum resource commitment in the steady state. Let $RT$ be the resource-reservation table representing the commitment of one iteration, and let $RT_s$ represent the commitment of the steady state. $RT_s$ combines the commitment from four consecutive iterations started $T$ clocks apart. The commitment of row 0 in the table $RT_s$ corresponds to the sum of the resources committed in $RT[0]$, $RT[2]$, $RT[4]$, and $RT[6]$. Similarly, the commitment of row 1 in the table corresponds to the sum of the resources committed in $RT[1]$, $RT[3]$, $RT[5]$, and $RT[7]$. That is, the resources committed in the $i$th row in the steady state are given by

$$RT_s[i] = \sum_{\{t \mid (t \bmod 2)=i\}} RT[t].$$

We refer to the resource-reservation table representing the steady state as the *modular resource-reservation table* of the pipelined loop.

To check if the software-pipeline schedule has any resource conflicts, we can simply check the commitment of the modular resource-reservation table. Surely, if the commitment in the steady state can be satisfied, so can the commitments in the prolog and epilog, the portions of code before and after the steady-state loop. □

In general, given an initiation interval $T$ and a resource-reservation table of an iteration $RT$, the pipelined schedule has no resource conflicts on a machine with resource vector $R$ if and only if $RT_s[i] \le R$ for all $i = 0,1,\ldots,T-1$.

### Data-Dependence Constraints

Data dependencies in software pipelining are different from those we have encountered so far because they can form cycles. An operation may depend on the result of the same operation from a previous iteration. It is no longer adequate to label a dependence edge by just the delay; we also need to distinguish between instances of the same operation in different iterations. We label a dependence edge $n_1 \to n_2$ with label $(\delta,d)$ if operation $n_2$ in iteration $i$ must be delayed by at least $d$ clocks after the execution of operation $n_1$ in iteration $i-\delta$. Let $S$, a function from the nodes of the data-dependence graph to integers, be the software pipeline schedule, and let $T$ be the initiation interval target. Then

$$(\delta \times T) + S(n_2) - S(n_1) \ge d.$$

The iteration difference, $\delta$, must be nonnegative. Moreover, given a cycle of data-dependence edges, at least one of the edges has a positive iteration difference.

**Example 10.18:** Consider the following loop, and suppose we do not know the values of $p$ and $q$.

```c
for (i = 0; i < n; i++)
    *(p++) = *(q++) + c;
```

We must assume that any pair of `*(p++)` and `*(q++)` accesses may refer to the same memory location. Thus, all the reads and writes must execute in the original sequential order. Assuming that the target machine has the same characteristics as that described in Example 10.12, the data-dependence edges for this code are as shown in Fig. 10.25. Note, however, that we ignore the loop-control instructions that would have to be present, either computing and testing *i*, or doing the test based on the value of R1 or R2.

```asm
// R1, R2 = q, p
// R3 = c
```

![](img/2a44b9071782fade81f3050c3b718341_752_0.png)

Figure 10.25: Data-dependence graph for Example 10.18

The iteration difference between related operations can be greater than one, as shown in the following example:

```c
for (i = 2; i < n; i++)
    A[i] = B[i] + A[i-2];
```

Here the value written in iteration *i* is used two iterations later. The dependence edge between the store of *A[i]* and the load of *A[i − 2]* thus has a difference of 2 iterations.

The presence of data-dependence cycles in a loop imposes yet another limit on its execution throughput. For example, the data-dependence cycle in Fig. 10.25 imposes a delay of 4 clock ticks between load operations from consecutive iterations. That is, loops cannot execute at a rate faster than one iteration every 4 clocks.

The initiation interval of a pipelined loop is no smaller than

$$\max_{c\text{ a cycle in }G}\left\lceil\frac{\sum_{e\in c}d_e}{\sum_{e\in c}\delta_e}\right\rceil$$

clocks.

In summary, the initiation interval of each software-pipelined loop is bounded by the resource usage in each iteration. Namely, the initiation interval must be no smaller than the ratio of units needed of each resource and the units available on the machine. In addition, if the loops have data-dependence cycles, then the initiation interval is further constrained by the sum of the delays in the cycle divided by the sum of the iteration differences. The largest of these quantities defines a lower bound on the initiation interval.

### 10.5.6 A Software-Pipelining Algorithm

The goal of software pipelining is to find a schedule with the smallest possible initiation interval. The problem is NP-complete, and can be formulated as an integer-linear-programming problem. We have shown that if we know what the minimum initiation interval is, the scheduling algorithm can avoid resource conflicts by using the modular resource-reservation table in placing each operation. But we do not know what the minimum initiation interval is until we can find a schedule. How do we resolve this circularity?

We know that the initiation interval must be greater than the bound computed from a loop’s resource requirement and dependence cycles as discussed above. If we can find a schedule meeting this bound, we have found the optimal schedule. If we fail to find such a schedule, we can try again with larger initiation intervals until a schedule is found. Note that if heuristics, rather than exhaustive search, are used, this process may not find the optimal schedule.

Whether we can find a schedule near the lower bound depends on properties of the data-dependence graph and the architecture of the target machine. We can easily find the optimal schedule if the dependence graph is acyclic and if every machine instruction needs only one unit of one resource. It is also easy to find a schedule close to the lower bound if there are more hardware resources than can be used by graphs with dependence cycles. For such cases, it is advisable to start with the lower bound as the initial initiation-interval target, then keep increasing the target by just one clock with each scheduling attempt. Another possibility is to find the initiation interval using a binary search. We can use as an upper bound on the initiation interval the length of the schedule for one iteration produced by list scheduling.

### 10.5.7 Scheduling Acyclic Data-Dependence Graphs

For simplicity, we assume for now that the loop to be software pipelined contains only one basic block. This assumption will be relaxed in Section 10.5.11.

**Algorithm 10.19:** Software pipelining an acyclic dependence graph.

**INPUT:** A machine-resource vector R = [r₁, r₂, . . .], where rᵢ is the number of units available of the ith kind of resource, and a data-dependence graph G = (N, E). Each operation n in N is labeled with its resource-reservation table RTₙ; each edge e = n₁ → n₂ in E is labeled with ⟨δₑ, dₑ⟩ indicating that n₂ must execute no earlier than dₑ clocks after node n₁ from the δₑ-th preceding iteration.

**OUTPUT:** A software-pipelined schedule S and an initiation interval T.
