![](bbox=[0.05, 0.08, 0.62, 0.42])

Every internal node of a parse tree is labeled with a nonterminal symbol, every leaf is labeled with a terminal symbol. Every subtree of a parse tree describes one instance of an abstraction in the sentence.

# 3.3.1.7 Ambiguity

A grammar that generates a sentential form for which there are two or more distinct parse trees is said to be ambiguous. Consider the grammar shown in Example 3.3, which is a minor variation of the grammar shown in Example 3.2.

# EXAMPLE 3.3 — An Ambiguous Grammar for Simple Assignment Statements

```
〈assign〉 → 〈id〉 = 〈expr〉
〈id〉 → A | B | C
〈expr〉 → 〈expr〉 + 〈expr〉
　　　　| 〈expr〉 * 〈expr〉
　　　　| (〈expr〉)
　　　　| 〈id〉
```

The grammar of Example 3.3 is ambiguous because the sentence

`A = B + C * A`

has two distinct parse trees, as shown in Figure 3.2. The ambiguity occurs because the grammar specifies slightly less syntactic structure than does the grammar of