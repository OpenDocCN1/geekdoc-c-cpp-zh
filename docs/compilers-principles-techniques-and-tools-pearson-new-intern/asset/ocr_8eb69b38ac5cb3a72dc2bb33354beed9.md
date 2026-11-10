4.4. TOP-DOWN PARSING

+   a) The grammar of Exercise 4.2.1.
+    b) The grammar of Exercise 4.2.2(a).
+    c) The grammar of Exercise 4.2.2(c).
+    d) The grammar of Exercise 4.2.2(e).
+    e) The grammar of Exercise 4.2.2(g).

! Exercise 4.3.3: The following grammar is proposed to remove the “dangling-else ambiguity” discussed in Section 4.3.2:

```
stmt          -> if expr then stmt
              |  matchedStmt
matchedStmt   -> if expr then matchedStmt else stmt
              |  other
```

Show that this grammar is still ambiguous.

# 4.4 Top-Down Parsing

Top-down parsing can be viewed as the problem of constructing a parse tree for the input string, starting from the root and creating the nodes of the parse tree in preorder (depth-first, as discussed in Section 2.3.4). Equivalently, top-down parsing can be viewed as finding a leftmost derivation for an input string.

Example 4.27 : The sequence of parse trees in Fig. 4.12 for the input id+id*id is a top-down parse according to grammar (4.2), repeated here:

```
E     ->   T E'
E'    ->   + T E' | ε
T     ->   F T'
T'    ->   * F T' | ε              (4.28)
F     ->   ( E ) | id
```

This sequence of trees corresponds to a leftmost derivation of the input. ☐

At each step of a top-down parse, the key problem is that of determining the production to be applied for a nonterminal, say A. Once an A-production is chosen, the rest of the parsing process consists of “matching” the terminal symbols in the production body with the input string.

The section begins with a general form of top-down parsing, called recursive-descent parsing, which may require backtracking to find the correct A-production to be applied. Section 2.4.2 introduced predictive parsing, a special case of recursive-descent parsing, where no backtracking is required. Predictive parsing chooses the correct A-production by looking ahead at the input a fixed number of symbols, typically we may look only at one (that is, the next input symbol).