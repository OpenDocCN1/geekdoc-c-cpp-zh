# 6. Quantifiers.

These are operations that introduce variables. In Example 1, for all is the quantifier for x; it is called the universal quantifier. The statement:

```
For all x, natural(x) natural(successor(x))
```

means that for every x in the universe, if x is a natural number, then the successor of x is also a natural number. A universal quantifier is used to state that a relationship among predicates is true for all things in the universe named by the variable x.

There is also the existential quantifier, there exists, as in the following statement:

```
there exists x, natural(x).
```

This statement means that there exists an x such that x is a natural number. An existential quantifier is used to state that a predicate is true of at least one thing in the universe, indicated by the variable x.

A variable introduced by a quantifier is said to be bound by the quantifier. It is possible for variables also to be free, that is, not bound by any quantifier.

# 7. Punctuation Symbols.

These include left and right parentheses, the comma, and the period. (Strictly speaking, the period isn’t necessary, but we include it since most logic programming systems use it.) Parentheses are used to enclose arguments and also to group operations. Parentheses can be left out in accordance with common conventions about the precedence of connectives, which are usually assumed to be the same as in most programming languages. (Thus, the connectives in order of decreasing precedence are not, and, or, →, and ↔.)

In predicate calculus, arguments to predicates and functions can only be terms—that is, combinations of variables, constants, and functions. Terms cannot contain predicates, quantifiers, or connectives. In Example 1, terms that appear include constants 0, 21, 2, the variable x, and the term successor(x), consisting of the function successor with argument x. Some examples of additional terms that can be written are successor(0) and successor(successor(successor(x))).

# EXAMPLE 2

The following are logical statements in English:

+   A horse is a mammal.
+   A human is a mammal.
+   Mammals have four legs and no arms, or two legs and two arms.
+   A horse has no arms.
+   A human has arms.
+   A human has no legs.