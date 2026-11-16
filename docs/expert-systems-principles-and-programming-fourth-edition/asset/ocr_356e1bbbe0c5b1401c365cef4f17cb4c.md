This time, however, placing the expression within the pattern allows it to be evaluated during pattern matching because the two variables ?x1 and ?y1 are both contained within the enclosing pattern of the expression:

```
(defrule point-not-on-x-y-diagonals
  (point (x ?x1)
         (y ?y1 :and (<> ?x1 ?y1)
              (<> ?x1 (- 0 ?y1))))
=>
  (assert (non-diagonal-point (x ?x1) (y ?y1))))
```

# 9.16 BUILT-IN PATTERN-MATCHING CONSTRAINTS

The built-in pattern-matching constraints are examples more efficient than an equivalent expression that must be evaluated. For example, a rule such as:

```
(defrule primary-color
  (color ?x& :or (eq ?x red)
           (eq ?x green)
           (eq ?x blue)))
=>
  (assert (primary-color ?x)))
```

should not be used when pattern-matching constraints can be used to accomplish the same results, as shown here:

```
(defrule primary-color
  (color ?x&red|green|blue)
  =>
  (assert (primary-color ?x)))
```

# 9.17 GENERAL RULES VERSUS SPECIFIC RULES

It is not always obvious whether many specific rules will perform more efficiently than fewer, more general rules. Specific rules tend to isolate much of the pattern-matching process in the pattern network, reducing the amount of work in the join network. General rules often provide more opportunity for sharing in the pattern and join networks. A single rule can also be more maintainable than a larger group of specific rules. General rules, though, need to be written carefully. Since they tend to perform the work of several rules, it is much easier to write an inefficient general rule than an inefficient specific rule. To illustrate the difference between the two techniques, consider the following deftemplate and four rules that will update a fact containing the grid coordinates of an object that can move north, south, east, or west. The location fact contains the x and y coordinates of the object. A move north increases the value of the y coordinate; a move east increases the value of the x coordinate.