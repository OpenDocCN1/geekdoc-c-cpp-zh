+   7. Let \( M = (Q, \Sigma, \Lambda, q_0, \delta, F) \) be a pushdown automaton. Define \( L'(M) \) to be the language \( L'(M) = \{w \in \Sigma^* \mid \text{it is possible for } M \text{ to start in state } q_0, \text{ read all of } w, \text{ and end in an accepting state}\} \). \( L'(M) \) differs from \( L(M) \) in that for \( w \in L'(M) \), we do not require that the stack be empty at the end of the computation.
+   
+   a) Show that there is a pushdown automaton \( M' \) such that \( L'(M') = L'(M) \).
+   
+   b) Show that a language \( L \) is context-free if and only if there is a pushdown automaton \( M \) such that \( L = L'(M) \).
+   
+   c) Identify the language \( L'(M) \) for each of the automata in Exercise 1.

+   8. Let \( L \) be a regular language over an alphabet \( \Sigma \), and let \( K \) be a context-free language over the same alphabet. Let \( M = (Q, \Sigma, q_0, \delta, F) \) be a DFA that accepts \( L \), and let \( N = (P, \Sigma, \Lambda, p_0, \delta, E) \) be a pushdown automaton that accepts \( K \). Show that the language \( L \cap K \) is context-free by constructing a pushdown automaton that accepts \( L \cap K \). The pushdown automaton can be constructed as a “cross product” of \( M \) and \( N \) in which the set of states is \( Q \times P \). The construction is analogous to the proof that the intersection of two regular languages is regular, given at the end of Section 3.6.

# 4.5 Non-context-free Languages

We have seen that there are context-free languages that are not regular. The natural question arises, are there languages that are not context-free? It’s easy to answer this question in the abstract: For a given alphabet \( \Sigma \), there are uncountably many languages over \( \Sigma \), but there are only countably many context-free languages over \( \Sigma \). It follows that most languages are not context-free. However, this answer is not very satisfying since it doesn’t give us any example of a specific language that is not context-free.

As in the case of regular languages, one way to show that a given language \( L \) is not context-free is to find some property that is shared by all context-free languages and then show that \( L \) does not have that property. It turns out that there is a similar Pumping Lemma for context-free languages. The proof of this lemma uses parse trees. In the proof, we will need a way of representing abstract parse trees, without showing all the details of the tree. The picture

![](bbox=[0.4, 0.83, 0.6, 0.95])