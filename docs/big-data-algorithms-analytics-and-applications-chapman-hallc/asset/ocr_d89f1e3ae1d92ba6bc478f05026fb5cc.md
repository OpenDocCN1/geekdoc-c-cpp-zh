as a regular quantization scheme. Equation 1.1 now transforms into

d(q, o_i) ≃ Σ_{r_j ∈ L(q,R) \ r_j ∈ L(o_i,R)}^{rank} |b_{qj} - b_y| . (1.3)

For each reference, B buckets are allocated. Each bucket contains a list of objects z, which contains the IDs of the objects that are located in the same bucket. Figure 1.3b shows the MIF for the partial ordered lists in Figure 1.1c. Then, these lists are compressed using delta encoding [29].

For searching, Equation 1.3 counts the discrepancy in quantized ranking from common reference objects between each object and the query. That is, each object o_i scores

s_i = |{ r_j ∈ L(q,R) such that (r_j ∈ L(o_i,R) and |b_{qj} - b_{qj}| ≤1 ) }| . (1.4)

Objects o_i are then sorted according to their decreasing s_i scores. This approximate ranking can be improved by DDC. For a K-NN query, we use a DDC on the K_c = Δ.K first objects in our sorted candidate list and call Δ > 1 the DDC factor.

# 1.4 DISTRIBUTED INDEXING

In this section, we show three different strategies to handle the PBI on a distributed environment. The first strategy is based on data division (Section 1.4.1), the second strategy is based on reference division (Section 1.4.2), and the third strategy is based on data and reference division (Section 1.4.3).

# 1.4.1 Data Based

# 1.4.1.1 Indexing

Given a data domain D of N objects, a reference set R of n points, and P processes, the reference set R is shared between all the processes. On the other hand, the data domain D is randomly divided into subdomains D1...Dp of equal sizes N/P among the processes. Each process p builds the partial ordered lists L̂(o_i,R) for all o_i ∈ D_p.

The ordered lists for these objects are saved locally in the appropriate data structure DP_p for each process. Accordingly, the workload of indexing is divided equally between the processes. Using this procedure, the complexity of indexing is reduced from O(N(n + nlogn)) to O N(n + nlogn)/P .

# 1.4.1.2 Searching

The data are equally divided among all the processes. Accordingly, when a query q is submitted, all the processes have to respond to this query. Algorithm 2 shows the