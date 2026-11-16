![](bbox=[0.13, 0.08, 0.87, 0.34])

Figure 15.8 A parse tree obtained using a LPCFG.

Because this is the only parse of the sentence, this is also the probability of the sentence.

Consider now the following sentence:

the man sleeps quiet.

Because P4(sleeps,quiet) = .00001, this sentence will have a much smaller probability.

A problem with LPCFG is that they require many more probabilities than PCFG. One way to handle this problem is to estimate the P4(v, n) for a rare (v, n) tuple by a probability that depends only on v.

The LPCFG we have shown is very simple. There are a number of ways of developing and learning LPCFGs. You are referred to the following texts and papers: [Charniak, 1993], [Charniak, 1997], [Manning and Schuetze, 2003], [Collins, 1997].

# 15.2 Semantic Interpretation

Parsing produces a tree that represents the linguistic components of a sentence such as the subject, verb, and object, and their relationships. The next step, namely semantic interpretation, represents the meaning of the sentence from the parse tree. By meaning we mean a statement that can be added to the knowledge base or a query that can be presented to the knowledge base. For example, suppose the domain of discourse is the blocks world in Section 4.2.2. Suppose further that the sentence is “block a is situated on block b.” Then the semantics of the sentence is on(a,b), and the semantic interpretation of the sentence must derive this logical formula from the sentence.