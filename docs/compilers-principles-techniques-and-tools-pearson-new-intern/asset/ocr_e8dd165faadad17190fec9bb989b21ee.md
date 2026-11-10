# 5.4. SYNTAX-DIRECTED TRANSLATION SCHEMES

```
A → X {R.i = f(X.x)} R {A.a = R.s}
R → Y {R_1.i = g(R.i, Y.y)} R_1 {R.s = R_1.s}
R → ε {R.s = R.i}
```

Notice that the inherited attribute R.i is evaluated immediately before a use of R in the body, while the synthesized attributes A.a and R.s are evaluated at the ends of the productions. Thus, whatever values are needed to compute these attributes will be available from what has been computed to the left.

# 5.4.5 SDT's for L-Attributed Definitions

In Section 5.4.1, we converted S-attributed SDD's into postfix SDT's, with actions at the right ends of productions. As long as the underlying grammar is LR, postfix SDT's can be parsed and translated bottom-up.

Now, we consider the more general case of an L-attributed SDD. We shall assume that the underlying grammar can be parsed top-down, for if not it is frequently impossible to perform the translation in connection with either an LL or an LR parser. With any grammar, the technique below can be implemented by attaching actions to a parse tree and executing them during preorder traversal of the tree.

The rules for turning an L-attributed SDD into an SDT are as follows:

+   1. Embed the action that computes the inherited attributes for a nonterminal A immediately before that occurrence of A in the body of the production. If several inherited attributes for A depend on one another in an acyclic fashion, order the evaluation of attributes so that those needed first are computed first.
+   2. Place the actions that compute a synthesized attribute for the head of a production at the end of the body of that production.

We shall illustrate these principles with two extended examples. The first involves typesetting. It illustrates how the techniques of compiling can be used in language processing for applications other than what we normally think of as programming languages. The second example is about the generation of intermediate code for a typical programming-language construct: a form of while-statement.

**Example 5.18:** This example is motivated by languages for typesetting mathematical formulas. Eqn is an early example of such a language; ideas from Eqn are still found in the TeX typesetting system, which was used to produce this book.

We shall concentrate on only the capability to define subscripts, subscripts of subscripts, and so on, ignoring superscripts, built-up fractions, and all other mathematical features. In the Eqn language, one writes a sub i sub j to set the expression `a_{i_j}`. A simple grammar for *boxes* (elements of text bounded by a rectangle) is