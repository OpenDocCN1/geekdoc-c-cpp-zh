To find the solution for non-trivial cases, we have to reduce this problem to a Max Flow problem. We assign the original vertex cost (the weight of taking that vertex) as capacity from source to that vertex for user A and capacity from that vertex to sink for user B. Then, we give ‘infinite’ capacity in between any edge in between sets A and B. See Figure 4.29.

![](bbox=[0.149, 0.153, 0.831, 0.313])

Figure 4.29: Reducing MWIS on Bipartite Graph to Max Flow Problem (from LA 3487 [11])

Then, we run $O(VE^2)$ Edmonds Karp’s algorithm on this Flow graph. After the Max Flow algorithm terminates, the solution is {s-component ∩ vertices in User A} + {t-component ∩ vertices in User B} where s-component (t-component) are the vertices still reachable to source vertex (sink vertex) after running Max Flow. In Figure 4.30, the solution is: {A1(20), A2(18), A4(54)} + {B3(47)} = 139. This value can also be obtained via: MWIS = Total Weight − Max Flow = 259 − 120 = 139.

![](bbox=[0.156, 0.461, 0.851, 0.615])

Figure 4.30: Solution for Figure 4.29 (from LA 3487 [11])

Programming Exercises related to Bipartite Graph:

+   - Maximum Cardinality Bipartite Matching (graph modeling + Max Flow)
+     1. UVa 670 - The Dog Task
+     2. UVa 753 - A Plug for Unix
+     3. UVa 10080 - Gopher II
+     4. UVa 10092 - The Problem with the Problemsetter
+     5. UVa 10735 - Euler Circuit
+     6. UVa 11045 - My T-Shirt Suits Me
+     7. UVa 11418 - Clever Naming Patterns
+     8. Top Coder Open 2003 Semifinal Round 4 - Division 1, Level 3 - RookAttack
+     9. Top Coder Open 2009: Qualifying 1 - Prime Pairs
+     10. LA 4407 - Gun Fight