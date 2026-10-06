# 220 Cloud Computing and Digital Media

SELECT ?a ?b ?lat ?long WHERE {
1 ?a dbpia:wilink dbpia:actor.
2 ?a dbpia:spouse ?b.
3 ?a dbpia:placeOfBirth ?c.
4 ?b dbpia:wilink dbpia:actor.
5 ?b dbpia:placeOfBirth ?c.
6 ?d:pos:lat.
7 ?c owl:sameAs ?d.
8 ?d:pos:long ? long. }
(a)

![](bbox=[0.186, 0.289, 0.775, 0.455])

**9.8** Query pattern graph generated from Q7. Part (a) shows the query, while part (b) shows the query’s graph representation in correspondence.

In this chapter, we study an optimal MRJ selection strategy based on a cost model to achieve minimum time span of query processing. For clear illustration, we first classify MRJs into two types: Pjoin (Pairwise Join) and Mjoin (Multiway Join). We define them as:

> **DEFINITION 10:** Given G(V,E,L₁,L_n), Pjoin(V') is a join operation on a set of Predicate files PF(v), v' ∈ V', V' ⊆ V, where G are connected by edges labeling with the same variable(s).

> **DEFINITION 11:** Given G(V,E,L₁,Ln), Mjoin(V') is a join operation on a set of Predicate files PF(v), v' ∈ V', V' ⊆ V, where G are connected by edges labeling with more than one variables.

For example, in Figure 9.8, picking of nodes 1–3 forms a Pjoin; whereas picking of nodes 5–8 forms an Mjoin. In a fact, for a vertex that has been picked in G, we make sure that at least one unmarked vertex is picked. Thus, after all vertices in G have been marked, we shall have enough MRJs to answer the original query. Apparently, there are many possible combinations of Pjoin and Mjoin to answer the query, while each combination implies an execution graph defined as follows.