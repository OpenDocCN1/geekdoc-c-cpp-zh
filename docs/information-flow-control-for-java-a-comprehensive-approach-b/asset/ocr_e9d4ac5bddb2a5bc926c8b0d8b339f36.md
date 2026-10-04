# CHAPTER 3. CONCURRENCY

# 3.2 Slicing Concurrent Java

The JMM defines the inter-thread semantics for accessing shared variables and therefore forms the basis for intra-thread slicing. The program order rule's intra-thread semantics effectively requires that program transformations adhere to the topological ordering imposed by data and control dependencies (see definitions in this chapter). Statements that are not ordered by these dependencies can safely be reordered⁵ Therefore, a more precise and control dependence analysis may enable more aggressive compiler optimizations. Additionally, the memory model requires that values written to shared variables in other threads are ordered by happens-before. The SDG needs to be extended to a concurrent system dependence graph (cSDG), a representation of concurrent programs where threads communicate via shared variables. These communications are represented as a special kind of dependence for shared variables that is traditionally called interference-dependence. The most basic form requires that the involved accesses are conflicting:

Definition 3.1 (Interference Dependence). A node $m$ is interference dependent [Kri98, HCD+99] on node $n$ ($n 	o m$), if

+   1. there is a variable $v$, such that $v \in Def(n)$ and $v \in Ref(m)$,

+   2. $n$ and $m$ must execute in different threads at runtime $	heta(n) 
eq 	heta(m)$, where a map $	heta$ maps a CFG node $n$ to a thread identifier to which $n$ belongs.

This definition is very conservative and will be shown in the subsequent sections, how to refine this to prune many of the spurious cases that previous approaches [HCD+99, Za99, RH04] suffer from.

Thread violation is traditionally modeled in analogy to procedure calls, if fork sites are connected via fork edges to the corresponding run() methods. As Java only supports thread invocation via calling Thread.start(), spawning a new thread executing its run() method and do not have explicit parameters, a fork site can only have one parameter for this pointer, as well as symmetric parameters for static variables. This parameter passing is modeled as for edges, in analogy to parameter-in-edges of method invocations. Changes in parameters are already modeled with interference⁷, so parameter-out edges are not ordered.

As an example, consider Figure 3.1, where a program fragment is depicted alongside its cSDG. The variables $x$ and $y$ are global, and thus as extra parameters at the thread's fork point. Note the fork edge between nodes 4 and 10 and the fork-edges between nodes 5 and 11, and 6 and 12. Node 15 defines the shared variable $x$, which is used at node 7 in the main thread, therefore an interference dependence is included from 15 to 7. The same goes for nodes 9 and 13, where the shared variable is redefined.

⁵Unless they are subject to another rule of the memory model.

⁶It may also be the case that two threads are different objects of the same class

⁷This is due to the obliviousness of Thread.join() of our model.

72