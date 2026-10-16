derivation that has this property is a leftmost derivation, where the leftmost remaining nonterminal is singled out for replacement at each step. For example, the derivations in Figures 6.3 and 6.5 are leftmost, but the derivation at the beginning of this section (deriving the same string as Figure 6.5) is not. Each parse tree has a unique leftmost derivation, which can be constructed by a preorder traversal of the tree. Thus, the ambiguity of a grammar can also be tested by searching for two different leftmost derivations of the same string. If such leftmost derivations exist, then the grammar must be ambiguous, since each such derivation must correspond to a unique parse tree. For example, the ambiguity of the grammar of Figure 6.4 is also demonstrated by the two leftmost derivations for the string 3 + 4 * 5 as given in Figure 6.14.

Leftmost Derivation 1
(Corresponding to
Tree 1 of Figure 6.13)

Leftmost Derivation 2
(Corresponding to
Tree 2 of Figure 6.13)

expr ⇒ expr + expr
expr ⇒ expr * expr
⇒ number + expr
⇒ expr + expr * expr
⇒ digit + expr
⇒ number + expr * expr
⇒ 3 + expr
⇒ ... (etc.)
⇒ 3 + expr * expr
⇒ 3 + number * expr
⇒ ... (etc.)

Figure 6.14 Two leftmost derivations for 3 + 4 * 5, indicating the ambiguity of the grammar of Figure 6.4

Ambiguous grammars present difficulties, since no clear structure is expressed. To be useful, either the grammar must be revised to remove the ambiguity or a disambiguating rule must be stated to establish which structure is meant.

Which of the two parse trees (or leftmost derivations) is the correct one for the expression 3 + 4 * 5? If we think of the semantics to be attached to the expression, we can understand what this decision means. The first syntax tree of Figure 6.13 implies that the multiplication operator * is to be applied to the 4 and 5 (resulting in the value 20), and this result is added to 3 to get 23. The second syntax tree, on the other hand, says to add 3 and 4 first (getting 7) and then multiply by 5 to get 35. Thus, the operations are applied in a different order, and the resulting semantics are quite different.

If we take the usual meaning of the expression 3 + 4 * 5 from mathematics, we would choose the first tree of Figure 6.13 over the second, since multiplication has precedence over addition. This is the usual choice in programming languages, although some languages (such as APL) make a different choice. How could we express the fact that multiplication should have precedence over addition? We could state a disambiguating rule separately from the grammar, or we could revise the grammar. The usual way to revise the grammar is to write a new grammar rule (called a “term”) that establishes a “precedence cascade” to force the matching of the “*” at a lower point in the parse tree:

```
expr → expr + expr | term
term → term * term | ( expr ) | number
```

We have not completely solved the ambiguity problem, however, because the rule for an expr still allows us to parse 3 + 4 + 5 as either (3 + 4) + 5 or 3 + (4 + 5). In other words, we can make addition either right- or left-associative, as shown in Figure 6.15.