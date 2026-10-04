
## 3.3. DEPENDENCE ANALYSIS FOR CONCURRENT PROGRAMS

**Algorithm 5** $(i, j) \in computeInterference()$

```
foreach (i, j) \in \{(i, j) : 0 \leq i, j \leq maxThreadNumber : i \neq j\n  foreach field f where is used in i and defined in j\n  statement g \in thread(i): f \in Ref(s)\n  statement s \in thread(j): f \in Def(s)\n  if f is static or g are aliased\n    addInterference(s, g)
```

only with thread number 0 can be the source of interference to other threads. In line (21), an entry of the face is written, therefore refers to that array in fThreads.run interference dependent on it; namely the condition in line (31) and line (36). Another definition can be found in line (44) for the field value. Again, this statement has interference dependence to line (36).

Other refined definitions of interference for Java can be imagined, and Rangwanath presents the following:

**Definition 3.3** (Interference Dependence [RH04]). Let P be a program, or an object with field $f$, and t1 and and22 be threads such that $t_1 \neq t_2$. If there exists an execution trace of P such that $f$ is written to by statement $s_m$ by a statement at point $n$ executed by $t_2$ (with $s_n$ occurring after $s_m$) and no write occurs between $s_m$ and $s_n$, then $n$ is interference dependent on $m$.

However, it is immediately clear from the undecidability for concurrent programs that such a definition can be conservatively approximated. Note that even though this definition was given before the specification of the New Java memory model, this definition must contain a clause stating that $s_m$ and $s_n$ are ordered by a happens-before statement allows values to be seen without ordering, it does not *guarantee* them to be seen. To remain conservative, a clause must be included.

Apart from interference, other inter-thread dependences have been found for slicing if the start or termination of one statement depends on the start or termination of another. For a JVM-like language, Hatcliff et al. [HCD*99] define synchronization dependence from an access to a shared variable to both the monitor acquisition and release statements of the directly enclosing critical region. Apart from Hatcliff et al. introduce readiness dependence modeling that a monitor or wait/notify may delay the execution of any such statement indefinitely.

Both works concurrency-related dependences with weak control dependence [PC90] (where Hatcliff et al. [HCD*99] decompose into standard control dependence and divergence dependence; for the latter they provide an intuitive definition). Hatcliff et al. state (however without correctness proof) that this set of dependences is guaranteed to produce a correct slice in the sense

## CHAPTER 3. CONCURRENCY

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

of a simulation-based correctness criterion extends the classic notion of projection in the single-threaded case, as originally presented by Weiser [Wei84].

## 3.4 Slicing the cSDG

Several algorithms have been proposed to slice concurrent SDGs. The most general and thus trivially correct algorithm is building the transitive closure of dependencies.¹⁰ This context-insensitive slicing algorithm is, however, far too conservative, as calling contexts are not taken into account.
nZhao [Zhao99, ZL04] leveraging the standard context-sensitive two-phase algorithm [Hir90] for slicing concurrent SDGs. However, this may yield incorrect slices, which was first noticed by Nanda [Nan01, NR06]. Figure 3.6 shows a minimal producer-consumer example with interference between the producer and the consumer. Two-phase slicing of the *print* node avoids the invocation of *prod:run*. In the first phase, all light gray nodes are traversed from *print x*. The second phase starts at the omitted parameter-out edge to the return statement and marks this and the header as part of the slice. Zhao's algorithm traverses interference as if it were a static dependence edge, it also marks nodes in the *set* method in the second phase. however, since the second phase must not ascend into calling methods, the invocation of *set* will not be included, even though it clearly belongs to the slice of the *print* statement.

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

## CHAPTER 3. CONCURRENCY

### 3.4.1 Iterative two-phase SummarySlicer

A straightforward extension of two-phase slicing makes this algorithm correct for slicing cDGs. As a remedy, each an interference edge is traversed, its source node (i.e. the node in the other thread) is marked as an synthetic slicing criterion, which means that it will be processed in the first phase of the slicing algorithm, even if the target node of the interference edge was processed in the second phase. A highly optimized pseudocode for it is given in Algorithm 6. The iterative two-phase slicing traverses each node and edge in the SDG at most twice, and thus has the worst case complexity as the original phase slicing algorithm by Horwitz et al. [HH90]. Its running time can be minimized, if all nodes that are to be traversed in the first phase are removed from the worklist before those two phase, as nodes found in the first phase will not need to be checked again.

Applied to the example program in Figure 3.6, it initializes its workload W to the print node. This node is also included into a M where it maps to true, meaning that it has been traversed in phase 1. It marks the nodes as Zhao's algorithm, traversing the parameter edge to the return statement of it, the return node is marked with false to indicate phase 2. No more nodes in phase 1 are available, so this node is taken from the worklist. Itcom incoming edges the method header get for phase 2 and the assignment to a.x for phase 1, as it is reached via interference. So this assignment node comes next, and its header node set is included into the slice marked with phase 1. Now we may ascend into the calling method and mark.run for phase 2. All remaining nodes in the worklist do not change the slice or marking. So the slice for the print statement is the whole graph, as expected.

Nanda had presented the first algorithm for iterative two-phase slicing consisting of two nested loops. Iterative two-phase slicing preserves context-sensitivity in each thread in isolation but breaks the calling contexts when crossing thread boundaries via interference dependence, but this is sound but not perfect.

### 3.4.2 Time Travel

Krinke [Tri98] first noticed that interference dependence is not transitive, in contrast to data dependence. With iterated two-phase slicing, it is possible to reenter a thread via interference that was previously left interference. However, as interference is determined without taking possible control flow into account, traversing interference several times may correspond to control flow that is impossible in any valid program execution. In practice, the node of reentrance must execute before the node that thread was previously left. Otherwise, this would correspond to a so-called "time travel" situation, where a value is dependent on a statement that will be executed in the future.

> 10Provided all necessary dependence types are included.

84
