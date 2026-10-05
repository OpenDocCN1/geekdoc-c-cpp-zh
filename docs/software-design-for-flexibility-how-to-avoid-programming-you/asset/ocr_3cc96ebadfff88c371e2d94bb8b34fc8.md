Term-rewriting systems are powerful tools for creating domain-specific languages for manipulating expression-like information. If we have a syntactic system of expressions, where we may need to replace some subexpressions with “equivalent” subexpressions, we can often use a rule-based term-rewriting system to describe those transformations. For example, many compiler optimizations can be expressed as local rewrites of program fragments in a larger context. The essential features of a term-rewriting system are the use of a pattern matcher to identify the information to be transformed, and a template system for instantiating the replacement. There has been extensive research [72] into the problem of constructing convergent term-rewriting systems from equational theories (systems of “equivalent” expressions), but we won't get into that here. Also, there is a superficial similarity between the patterns matched against and the templates for instantiation, which may suggest the possibility of making bidirectional rules; we won't look at that. First we develop a simple unidirectional system, in which patterns are used to recognize inputs and templates are used to make outputs.

Here is an approximation to some algebraic simplification rules:

```
(define algebra-1
(rule-simplifier
 (list
  ;; Associative law of addition
  (rule '+ (? a) (+ (? b) (? c))
   '(+ (+ ,a ,b) ,c))
  ;; Commutative law of multiplication
  (rule '* (? b) (? a))
   (and (expr? a b)
       (* ,a ,b)))
  ;; Distributive law of multiplication over addition
  (rule '* (? a) (+ (? b) (? c))
   '(+ (* ,a ,b) ,c)))))
```

There are three rules in algebra-1. The first rule implements the associative law of addition, the second implements the commutative law of multiplication, and the third implements the distributive law of multiplication over addition.

Each rule is composed of two parts: a pattern to match a subexpression, and a consequent expression. If the pattern matches, the consequent is evaluated. If the value of the consequent is #f the rule is not applicable. Otherwise the result of the evaluation replaces