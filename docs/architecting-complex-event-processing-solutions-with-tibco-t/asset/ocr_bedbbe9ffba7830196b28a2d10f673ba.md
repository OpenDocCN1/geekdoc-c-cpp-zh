Figure 5-17 shows the Rete network after T1 is introduced. Since T1 appears in the type filter result set, and this set is the only input to C1, the conditions of C1 are actually evaluated as the node attempts to join T1 with itself! Of course the join fails, but the computational resources were still expended.

Figure 5-18 shows the network after the introduction of T2. The appearance of T2 in the type filter result set triggers the evaluation of C1—three times! It will try to join T2 to itself and will try both combinations of T1 and T2. Only one of these combinations will produce the sought-after conclusion.

It is worth noting what happens as additional transactions are introduced into this network: Every possible combination of the transactions will be tried by C1. The computational complexity is thus n², where n is the number of transactions present in working memory. This isn't exactly the kind of computational complexity you want in your solutions.

As these two examples illustrate, the way in which you construct the conditional clauses in a rule has a significant impact on the amount of work done as the Rete network evaluates the rule conditions. The more you think about how the rule conditions are transformed into the Rete network for execution, the more efficient your solution will be.

![](bbox=[0.25, 0.72, 0.8, 0.93])

Figure 5-17: ACEPSTConditionsAnded First Transaction Processing