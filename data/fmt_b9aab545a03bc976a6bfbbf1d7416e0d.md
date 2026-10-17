
### Definition 3.3 (Interference Dependence [RH04])
Let `P` be a program, or an object with field `$f$`, and `t1` and and22 be threads such that `$t_1 \neq t_2$`. If there exists an execution trace of `P` such that `$f$` is written to by statement `$s_m$` by a statement at point `n` executed by `t2` (with `$s_n$` occurring after `$s_m$`) and no write occurs between `$s_m$` and `$s_n$`, then `n` is interference dependent on `m`.

然而，从并发程序的不可判定性来看，这种定义可以保守地近似。注意，即使该定义是在新 Java 内存模型规范之前给出的，该定义也必须包含一个条款，说明 `$s_m$` 和 `$s_n$` 由 happens-before 语句排序，允许值在没有排序的情况下被看到，它并不能 *保证* 它们会被看到。为了保持保守，必须包含一个条款。

除了干扰之外，还发现了其他线程间依赖，用于切片，如果一个语句的开始或终止取决于另一个语句的开始或终止。对于类似 JVM 的语言，Hatcliff et al. [HCD*99] 定义了从对共享变量的访问到直接封闭临界区的 monitor 获取和释放语句的同步依赖。除了 Hatcliff et al. 引入了就绪依赖的建模，即 monitor 或 wait/notify 可能无限期地延迟任何此类语句的执行。

两项工作都将并发相关的依赖与弱控制依赖 [PC90] 结合起来（其中 Hatcliff et al. [HCD*99] 分解为标准控制依赖和发散依赖；对于后者他们提供了直观的定义）。Hatcliff et al. 指出（然而没有正确性证明）这组依赖被保证能产生正确的切片，其含义是

# CHAPTER 3. CONCURRENCY

```
int x;

main() {
  cons() || prod();
}

prod() {
  set();
}

void set() {
  x = ...;
}

cons() {
  int y = get();
  print(y);
}

int get() {
  return x;
}
```

![](img/27c6595637bae6b27613772d7079f8a2_91_0.png)

Figure 3.6: A counter example to Zhao's approach

基于模拟的正确性标准扩展了单线程情况下投影的经典概念，最初由 Weiser [Wei84] 提出。

## 3.4 Slicing the cSDG

已经提出了几种算法来切片并发 SDG。最通用且因此显然正确的算法是构建依赖的传递闭包。¹⁰ 然而，这种上下文无关的切片算法过于保守，因为没有考虑调用上下文。

nZhao [Zhao99, ZL04] 利用标准上下文敏感的两阶段算法 [Hir90] 来切片并发 SDG。然而，这可能产生不正确的切片，这首先由 Nanda [Nan01, NR06] 注意到。图 3.6 显示了一个最小的生产者-消费者示例，其中生产者和消费者之间存在干扰。对 *print* 节点的两阶段切片避免了 *prod:run* 的调用。在第一阶段，从 *print x* 开始遍历所有浅灰色节点。第二阶段从省略的参数-out 边开始，到返回语句并将该语句和头部标记为切片的一部分。Zhao 的算法将干扰遍历为静态依赖边，它也在第二阶段标记了 *set* 方法中的节点。然而，由于第二阶段不得上升到调用方法，*set* 的调用将不会被包含，即使它显然属于 *print* 语句的切片。

## 3.4. SLICING CSDG

**Algorithm 6** Iterative two-phase SummarySlicer

```
**Input:** The cSDG G, a slicing criterion s.
**Output:** The slice S for s.

W = {s} // a worklist
M = {s \mapsto$ true} // a map for marking the contents of W
// (true represents phase 1, false phase 2)

repeat
  W = W \cup {n} // remove next node n from W
  foreach m \mapsto$ n // handle all incoming edges of n
    if m wasn't visited yet edge or m was visited in phase 2 and we are in phase I ...
      // traversing an interference edge,
      if m \in M (\neg M(n) \wedge (M(m) \vee e = id))\n        // if we are in phase 1 or if e is not a call or param-in edge, add m to W
        if M(n) \notin e \in {call, param}
          W = W \cup {m}
      /* Now we determine how to mark m: */
      // If we are in phase 1 and e is a param-out edge, mark m with phase 2
      if M(n) \wedge e = po
        M = M \cup {m \mapsto$ false}
      // If we are in phase 2 and e is an interference edge, mark m with phase 1
      else if M(n) \wedge e = id
        M = M \cup {m \mapsto$ true}
      // Else mark m with the same phase as n
    else
      M = M \cup {m \mapsto$ M(n)}
until W = \varnothing
**return** dom M
```

# CHAPTER 3. CONCURRENCY

### 3.4.1 Iterative two-phase SummarySlicer

两阶段切片的一个直接扩展使该算法对切片 cDG 正确。作为补救措施，每次遍历一个干扰边时，其源节点（即另一个线程中的节点）被标记为合成切片标准，这意味着它将在切片算法的第一阶段中被处理，即使干扰边的目标节点是在第二阶段中处理的。它的高度优化的伪代码在 Algorithm 6 中给出。迭代两阶段切片最多遍历 SDG 中的每个节点和边两次，因此其最坏情况复杂度与 Horwitz 等人 [HH90] 的原始阶段切片算法相同。其运行时间可以最小化，如果所有要在第一阶段遍历的节点在那两个阶段之前从工作列表中移除，则可以最小化，因为在第一阶段找到的节点不需要再次检查。

应用于图 3.6 中的示例程序，它将工作负载 W 初始化为 print 节点。该节点也被包含到 M 中，其中它映射到 true，表示它已在阶段 1 中遍历。它像 Zhao 的算法一样标记节点，遍历到它的返回语句的参数边，返回节点被标记为 false 以表示阶段 2。没有更多阶段 1 的节点可用，因此该节点被从工作列表中取出。它com incoming edges the method header get for phase 2 and the assignment to a.x for phase 1, as it is reached via interference. So this assignment node comes next, and its header node set is included into the slice marked with phase 1. Now we may ascend into the calling method and mark.run for phase 2. All remaining nodes in the worklist do not change the slice or marking. So the slice for the print statement is the whole graph, as expected.

Nanda 提出了第一个迭代两阶段切片算法，由两个嵌套循环组成。迭代两阶段切片在每个线程内部保持上下文敏感，但在通过干扰依赖跨越线程边界时破坏调用上下文，但这是 sound 但不完美的。

### 3.4.2 Time Travel

Krinke [Tri98] 首先注意到干扰依赖不是传递的，与数据依赖相反。通过迭代两阶段切片，可以通过干扰重新进入之前已离开的线程。然而，由于干扰是在不考虑可能控制流的情况下确定的，多次遍历干扰可能对应于在任何有效程序执行中都不可能存在的控制流。在实践中，重入的节点必须在之前离开该线程的节点之前执行。否则，这将对应于所谓的“时间旅行”情况，其中一个值依赖于将在未来执行的语句。

> 10Provided all necessary dependence types are included.

84

```
int x,y;

main() {
  x = 0;
  y = x;
  fork(thread_1);
  int p = x - 2;
  int q = p + 1;
  y = q + 3;
}

thread_1() {
  int a = y + 1;
  int b = a + 4;
  x = b / 2;
}
```

## 3.4. SLICING THE CSDG

![](img/27c6595637bae6b27613772d7079f8a2_94_0.png)

Figure 3.7: Slicing an example <CSDG>

As an example, consider the program and corresponding graph in Figure 3.7, where the shaded nodes are the slice for node 14 computed by the iterated phase slicer. thread_1 at node 13 towards node 9 and returns to node 15 via the interference edge from node 7. Notably, node 15 cannot influence the slicing criterion 14, because it cannot execute before 14. [Ram00,MOS01] as the exact order between threads is undecidable this order cannot be taken into account when computing interference dependencies. In contrast, intra-thread dependencies like data or control dependence take flow into account, making them transitive.

Slicing other Concurrency-Related Dependencies Intractivity is regarded for interference only, mainly due to incompatible programming primitives, Krinke's and Nanda's models do not consider synchronization primitives, thus they can only argue about interference dependence. Approaches with a finer-grained concurrency model like that by Cheng and Hatfield [Che93b, ICD99,RH04] leverage context-sensitive slicing, which ignores intractivity issues and is also of precision. Dewar et al. [DCH+*99] argue that it remains unclear whether the gain in precision of context-sensitivity outweighs the additional cost.

However, taking all concurrency-related dependencies into account, time travel may occur for all nodes of dependencies that cross thread boundaries, if control flow is ignored during dependence computation. In particular, [HCD+99, RH04] is intractive when crossing boundaries. Accordingly, some algorithms that prune time travels for interference dependence must be applied to get precise slices with ready dependence. The author is not aware of any work that identifies or targets this problem.

### 3.4.3 Slicers Disallowing Time Travel

To prune interference traversals that correspond to time travel situations, Krinke and Nanda [Kri03b, NR06] defined which paths in each thread's control flow

# CHAPTER 3. CONCURRENCY

graph correspond to a valid program execution. Their slicing algorithms are effectively symbolic deconstruction which marks all other paths as invalid such that they are not traversed during slicing.

The threaded control flow graph (TCFG) consists of the ICFGs of each thread that are connected at fork and join nodes, respectively. Note that Krinke [Kr03b] and Nanda [NR06] require threads to be disjoint, which is in general not the case for Java threads. However, one can always duplicate parts of the graph to achieve disjointness, which will be assumed in the sequel.

A interprocedural realizable path $P = n_1, \dots, n_k$ is an ordered sequence of nodes in the TCFG G that every projection of P to a thread $\theta$, created in $P$ is either empty or corresponds to an interprocedural realizable path in the thread.

The slice of a cSDG w.r.t. $c$, the criterion $p$, depends on $S(p)$, consists of all nodes on $q$ which painfully depends and there exists an interprocedural trace witness $W$ in the TCFG for each such $q$.

```
S(p) = \begin{cases} q = n_1, \dots, n_k, \ q = n_{d_1}, \dots, n_{d_{k-1}}, n_k, p = d_i, i \in \cd, dd, id\}, 1 \le i \le k, \ \text{P is an interprocedural realizable path in G} \ \text{where } n_i \text{ is a node in } P \text{ in the same order as } W \end{cases}
```
