# 7.2. EVALUATING INTERFERENCE DEPENDENCE

![](bbox=[0.176, 0.126, 0.823, 0.463])

Figure 7.1: Evaluation of context-sensitive slicing with object trees

for three variants of graph and slicing algorithm. The first variant (dd) takes the SDG presented in chapter 2 together with context-sensitive two-phase slicing; the second (cis) uses the same graph but applies context-insensitive slicing (i.e. the transitive closure of dependencies); and the third variant applies context-sensitive slicing to an interprocedural program dependence graph, where data dependencies for fields may span method boundaries. Remember that we could not apply context-sensitive slicing on this graph as it is not compatible to an SDG. The results show that context-sensitive slices are on average 13% smaller than context-insensitive slices. The differences between the context-insensitive variants are, as expected, negligible. On average, slicing the graph with object trees resulted in smaller slices (the difference is about one basis point) with method-sensitive data dependencies.

# 7.2 Evaluating Interference Dependence

Apart from usual data dependencies our SDG contains interference dependence caused by memory access in threads. To compare the effectiveness of our algorithm of chapter 3, which computes a safe approximation of interference dependence, we measured the number of interference edges and compared this number with the one reported in Ranganathan and Hatcliff [RH04] and type-based approaches as used in [HCD7:99]. Table 7.2 shows the result of our analysis: We examined the same programs as in [RH04], i.e. a suite of benchmarks from