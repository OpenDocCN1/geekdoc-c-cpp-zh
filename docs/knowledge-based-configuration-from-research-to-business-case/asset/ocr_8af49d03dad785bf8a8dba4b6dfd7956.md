![](bbox=[0.22, 0.14, 0.75, 0.34])

# FIGURE 7.3

A diagnosis Δ is a subset of C (AC = C ∪ B) such that B ∪ C − Δ is consistent. Δ is minimal if no subset of Δ fulfills the diagnosis property. B again represents the background knowledge. An example diagnosis is Δ1 = {c1}.

# Definition (Diagnosis Task).

A diagnosis task can be defined by the tuple (C, AC) where AC = B ∪ C, B is the background knowledge, and C is the set of constraints to be analyzed.

Before discussing potential algorithms that support the calculation of minimal diagnoses, we introduce the definition of a diagnosis that represents a solution to a given diagnosis task (C, AC). The basic idea of diagnosis determination is depicted in Figure 7.3.

# Definition (Diagnosis).

A diagnosis for a given diagnosis task (C,AC) is a set of constraints Δ ⊆ C such that B ∪ C − Δ is consistent. A diagnosis Δ is minimal if there does not exist a diagnosis Δ′ ⊂ Δ with the diagnosis property. Finally, a minimal diagnosis Δ is denoted as minimal cardinality diagnosis if there does not exist a minimal diagnosis Δ′ with |Δ′| < |Δ|.

A widespread approach to the determination of diagnoses (hitting sets) is the construction of a HSDAG. The algorithm is known as hitting set directed acyclic graph algorithm, which has been introduced by Reiter (1987).

# 7.4.1 Hitting Set Directed Acyclic Graph (HSDAG)

The HSDAG algorithm supports the determination of minimal diagnoses. Since the algorithm performs diagnosis search typically in breadth-first fashion, it supports the determination of minimal cardinality diagnoses (i.e., minimal diagnoses with the lowest possible number of included constraints). However, the algorithm is complete; after returning minimal cardinality diagnoses, it returns all other diagnoses contained in the consideration set C. HSDAG structures can be established by repeatedly activating a conflict detection algorithm (e.g., SimpleConflictDetection or QuickXPlain) and to analyze the different possibilities to resolve the returned conflict. Since this is a simple implementation of a breadth-first search strategy, we do not provide an algorithm here.

For example, in Figure 7.4 the first minimal conflict set returned by the conflict detection algorithm is CS1 : {c1, c4, c5}. If we resolve the conflict CS1, by deleting the constraint c4, another conflict set will be identified – CS2 : {c1, c2, c5}.