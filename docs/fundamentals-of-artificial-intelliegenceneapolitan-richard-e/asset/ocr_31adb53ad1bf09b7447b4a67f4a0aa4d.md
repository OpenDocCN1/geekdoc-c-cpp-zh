# EXERCISES

# Section 15.1

Exercise 15.1 Show that any context-free grammar can be transformed into a grammar in Chomsky normal form.

Exercise 15.2 Using the CFG in Table 15.1, parse these sentences and show the resultant parse trees:

+   1. A big man loves the monkey.
+   2. The fat monkey can read the right book.
+   3. The man loves the left and the monkey loves the right.

Exercise 15.3 Modify Algorithm 15.1 so that it produces a parse tree.

Exercise 15.4 Implement Algorithm 15.1 and use it to parse the sentences in Exercise 15.2

Exercise 15.5 Show two different parse trees for each of the sentences in Example 15.2.

Exercise 15.6 Using the grammar in Table 15.3, show the table produced by the CYK algorithm when parsing each of the following sentences:

+   1. y y x x x
+   2. x x y x x
+   3. x y y y y.

Exercise 15.7 Implement the CYK algorithm.

Exercise 15.8 Show that the time complexity of the CYK algorithm is \(\theta(mn^3)\), where \(m\) is the number of rules and \(n\) is the number of words in the sentence.

Exercise 15.9 Using the PCFG in Table 15.4, compute probabilities of the sentences in Exercise 15.2.

Exercise 15.10 Using the LPCFG in Table 15.5, obtain the parse tree and compute the probability of this sentence:

The man sleeps quiet.

# Section 15.2

Exercise 15.11 Augment the grammar in Table 15.1 with semantics, and use the augmented grammar to obtain semantics for the sentences in Exercise 15.2.