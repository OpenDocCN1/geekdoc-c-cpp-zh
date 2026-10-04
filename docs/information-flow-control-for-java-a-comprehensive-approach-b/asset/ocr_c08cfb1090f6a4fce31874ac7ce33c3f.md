# CHAPTER 7. EVALUATION

its features to Jif and point out directions where a closer integration of other work on information flow control is required.

# 7.3.3 Flow-, Context- and Object-Sensitivity

Program dependence graphs can be constructed to allow flow, context- and object-sensitive analysis. For flow-sensitive analysis derivatives of SSA-form have been presented in literature, and even an SSA-form for heap objects [FKS00] was proposed. Two-phasing of the system dependence graph [HRB90] is context-sensitive, due to edges which sum transitive dependence between method parameters. For object-sensitive results, the field structure of parameters need to be represented across the references and modifications in this method and transitively called methods (see chapter 2). A precise analysis of these parameters requires points-to-analysis. Evaluations on points-to last decade have improved the performance and scalability enormously and thus, flow-, context- and object-sensitive analyses for realistic programs are feasible [MRR02, LH03, LL03, WL04, LH08], which again sustains the precision of dependence graphs.

Another benefit of slicing based information flow control is that when the graph is built, the checker is independent of the actual source language, which facilitates building of reusable checkers. The Valsoft infrastructure contends for C and Java so all these languages can be checked with the same infrastructure when the dependence graph is annotated with security levels.

# Noninterference

Theorem 4.1 on page 92 states that for two nodes, n a in the dependence graph if n BackwardSlice(a) ∨ label(n) ≤ label(a) then the noninterference criterion is satisfied between n and a. If there exists a path n→a and label(n) ⊈ label(a) then a (potential) security violation has been found. While the proof is independent of the specific language or slicing criterion, it is that a more precise slice will have fewer false rates. This flow-, context- and object-sensitive slicing as described earlier also verify precise results that out compared by Jif’s system, without the additional burden of annotating classes and methods with polymorphic security types.

As data and control flow are formally defined in terms of reaching definitions res. [FOW87], program slicing is no less formal than type systems, in the contrary, it has been shown that dependence graphs accurately represent proof of the semantics of a graph (see section 2.2). Even, a machine-checked proof of the correctness of our flow control mechanism is possible [qui].

Information flow checking in dependence graphs is similar to type systems but not the same: Denning-style labels are attached to nodes in the graph, not to variables. So even if the annotations in line 13 and 14 of Figure 46 on page 96 look similar to a type declaration, the semantics is totally different; another definition of the same variables might get a completely different label or