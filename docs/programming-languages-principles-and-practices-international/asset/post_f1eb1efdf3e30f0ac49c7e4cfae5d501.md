
the structure of each interior node, and the derivation specifies which interior nodes are constructed. For example, the tree for the number 234 is specified by the grammar rules for *number* and the derivation of 234 as given in the previous section. Indeed, the first two steps of the derivation are:

```
number ⇒ number digit      (step 1)
    ⇒ number digit digit      (step 2)
```

and correspond to the construction of the two children of the root (step 1) and the two children of the left child of the root (step 2). Not surprisingly, there are exactly as many steps in the derivation of 234 as there are interior nodes in the parse tree.

All the terminals and nonterminals in a derivation are included in the parse tree. However, not all the terminals and nonterminals are necessary to determine completely the syntactic structure of an expression or sentence. For example, the structure of the number 234 can be completely determined from the tree shown in Figure 6.9.

![](img/062750ade02e28185b1fb8e8cf6dc89e_221_0.png)

Figure 6.9: Parse tree for determining structure of the number 234

As another example, Figure 6.10 shows how a parse tree for 3 + 4 * 5 can be condensed.

## Complete parse tree

## Condensed parse tree

![](img/062750ade02e28185b1fb8e8cf6dc89e_221_1.png)

![](img/062750ade02e28185b1fb8e8cf6dc89e_221_2.png)

Figure 6.10: Condensing parse tree for 3 + 4 * 5

*expr* ⇒ *expr* + *expr*  
⇒ *expr* + *expr* * *expr*  
(replace the second *expr* with *expr* * *expr*)  
⇒ *number* + *expr* * *expr*  
⋯

or the derivation:

*expr* ⇒ *expr* * *expr*  
⇒ *expr* + *expr* * *expr*  
(replace the first *expr* with *expr* + *expr*)  
⇒ *number* + *expr* * *expr*  
⋯

These, in turn, lead to the two distinct parse trees shown in Figure 6.12. (Dashed lines in the remaining trees in this chapter indicate missing nodes in the parse trees that are irrelevant to the current discussion.) This derivation can also lead to the two distinct abstract syntax trees shown in Figure 6.13.

![](img/062750ade02e28185b1fb8e8cf6dc89e_223_0.png)

**Figure 6.12:** Two parse trees for 3 + 4 * 5

![](img/062750ade02e28185b1fb8e8cf6dc89e_223_1.png)

**Figure 6.13** Two abstract syntax trees for 3 + 4 * 5, indicating the ambiguity of the grammar of Figure 6.4

A grammar such as that in Figure 6.4, for which two distinct parse (or syntax) trees are possible for the same string, is **ambiguous**. Ambiguity can also be expressed directly in terms of derivations. Even though many derivations may in general correspond to the same parse tree, certain special derivations that are constructed in a special order can only correspond to unique parse trees. One kind of

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

![](img/062750ade02e28185b1fb8e8cf6dc89e_225_0.png)

# Figure 6.15: Addition as either right- or left-associative

In the case of addition, this does not affect the result, but if we were to include subtraction, it surely would: 8 - 4 - 2 = 2 if “-” is left-associative, but 8 - 4 - 2 = 6 if “-” is right-associative. What is needed is to replace the rule:

```
expr → expr + expr
```

with either:

```
expr → expr + term
```

or:

```
expr → term + expr
```

The first rule is left-recursive, while the second rule is right-recursive. A left-recursive rule for an operation causes it to left-associate, as in the parse tree shown in Figure 6.16. Similarly, a right-recursive rule causes it to right-associate, as also shown in Figure 6.16.

| A left-recursive rule for an operation causes it to left-associate. | A right-recursive rule for an operation causes it to right-associate. |
|---|---|
| Parse tree with expr + term left-recursive | Parse tree with term + expr right-recursive |

# Figure 6.16: Parse trees showing results of left- and right-recursive rules

The revised grammar for simple integer arithmetic expressions that expresses both precedence and associativity is given in Figure 6.17.

```
expr → expr + term | term
term → term * factor | factor
factor → ( expr ) | number
number → number digit | digit
digit → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

**Figure 6.17** Revised grammar for simple integer arithmetic expressions

The grammar of Figure 6.17 is now unambiguous (a proof of this requires more advanced techniques from parsing theory). Moreover, the syntax trees generated by this grammar correspond to the semantics of the arithmetic operations as they are usually defined. Sometimes the process of rewriting a grammar to eliminate ambiguity causes the grammar to become extremely complex, and in such cases we prefer to state a disambiguating rule (see the if-statement discussion in Chapter 9).

## 6.5 EBNFs and Syntax Diagrams

We noted earlier that the grammar rule:

```
number → number digit | digit
```

generates a number as a sequence of digits:

```
number ⇒ number digit
       ⇒ number digit digit
       ⇒ number digit digit digit
       ⇒ digit . . . digit
       . . .
       ⇒ (arbitrary repetitions of digit)
```

Similarly, the rule:

```
expr → expr + term | term
```

generates an expression as a sequence of terms separated by “+’s”:

```
expr ⇒ expr + term
      ⇒ expr + term + term
      ⇒ expr + term + term + term
      . . .
      ⇒ term + . . . + term
```
