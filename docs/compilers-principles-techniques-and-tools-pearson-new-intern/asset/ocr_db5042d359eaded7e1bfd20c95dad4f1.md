# Convention Distinguishing Uses of a Nonterminal

In rules, we often have a need to distinguish among several uses of the same nonterminal in the head and/or body of a production; e.g., see Example 2.10. The reason is that in the parse tree, different nodes labeled by the same nonterminal usually have different values for their translations. We shall adopt the following convention: the nonterminal appears unsubscripted in the head and with distinct subscripts in the body. These are all occurrences of the same nonterminal, and the subscript is not part of its name. However, the reader should be alert to the difference between examples of specific translations, where this convention is used, and generic productions like $A \to X_1X_2,\ldots,X_n$, where the subscripted $X$’s represent an arbitrary list of grammar symbols, and are *not* instances of one particular nonterminal called $X$.

# 2.3.3 Simple Syntax-Directed Definitions

The syntax-directed definition in Example 2.10 has the following important property: the string representing the translation of the nonterminal at the head of each production is the concatenation of the translations of the nonterminals in the production body, in the same order as in the production, with some optional additional strings interleaved. A syntax-directed definition with this property is termed *simple*.

**Example 2.11:** Consider the first production and semantic rule from Fig. 2.10:

| PRODUCTION | SEMANTIC RULE | |
|---|---|---|
| $expr \to expr_1 + term$ | $expr.t = expr_1.t \Vert term.t \Vert '+'$ | (2.5) |

Here the translation $expr.t$ is the concatenation of the translations of $expr_1$ and $term$, followed by the symbol +. Notice that $expr_1$ and $term$ appear in the same order in both the production body and the semantic rule. There are no additional symbols before or between their translations. In this example, the only extra symbol occurs at the end. □

When translation schemes are discussed, we shall see that a simple syntax-directed definition can be implemented by printing only the additional strings, in the order they appear in the definition.

# 2.3.4 Tree Traversals

Tree traversals will be used for describing attribute evaluation and for specifying the execution of code fragments in a translation scheme. A *traversal* of a tree starts at the root and visits each node of the tree in some order.