represents a parse tree which has the non-terminal symbol A at its root and the string x along the “bottom” of the tree. (That is, x is the string made up of all the symbols at the endpoints of the tree’s branches, read from left to right.) Note that this could be a partial parse tree—something that could be a part of a larger tree. That is, we do not require A to be the start symbol of the grammar and we allow x to contain both terminal and non-terminal symbols. The string x, which is along the bottom of the tree, is referred to as the **yield** of the parse tree. Sometimes, we need to show more explicit detail in the tree.

![](bbox=[0.35, 0.28, 0.65, 0.45])

represents a parse tree in which the yield is the string xyz. The string y is the yield of a smaller tree, with root B, which is contained within the larger tree. Note that any of the strings x, y, or z could be the empty string.

We will also need the concept of the **height** of a parse tree. The height of a parse tree is the length of the longest path from the root of the tree to the tip of one of its branches.

Like the version for regular languages, the Pumping Lemma for context-free languages shows that any sufficiently long string in a context-free language contains a pattern that can be repeated to produce new strings that are also in the language. However, the pattern in this case is more complicated. For regular languages, the pattern arises because any sufficiently long path through a given DFA must contain a loop. For context-free languages, the pattern arises because in a sufficiently large parse tree, along a path from the root of the tree to the tip of one of its branches, there must be some non-terminal symbol that occurs more than once.

> Theorem 4.7 (Pumping Lemma for Context-Free Languages). Suppose that L is a context-free language. Then there is an integer K such that any string w ∈ L(G) with |w| ≥ K has the property that w can be written in the form w = uvxyz where
> • x and z are not both equal to the empty string;
> • |vyz| < K;
> • For any n ∈ N, the string uv^n x y^n z is in L.

Proof. Let G = (V, Σ, P, S) be a context-free grammar for the language L. Let N be the number of non-terminal symbols in G, plus 1. That is,