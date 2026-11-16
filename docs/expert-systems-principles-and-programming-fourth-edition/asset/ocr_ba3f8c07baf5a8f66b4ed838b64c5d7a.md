```
=>
(bind ?total (send ?sum get-total))
(send ?sum put-total
      (+ ?total (* ?height ?width))))
```

This version of the rule won't infinitely loop like the initial version. If we know that there will be only one instance of the SUM class, we can take the process one step further to simplify the rule:

```
(defrule sum-rectangles
  (object (is-a RECTANGLE)
          (height ?height) (width ?width))
=>
(bind ?total (send [sum] get-total))
(send [sum] put-total
      (+ ?total (* ?height ?width))))
```

Rather than pattern matching to retrieve the instance address of the [sum] instance in the ?sum variable, we can simply reference the instance by name on the RHS of the rule.

# The Pattern-Matching Attribute

It's possible to indicate that either a slot or a class cannot participate in pattern matching using the pattern-match attribute. If this attribute is set to reactive, which is the default, then the specified slot or class will be able to trigger pattern matching on the LHS of a rule. If the attribute is set to non-reactive, then the specified slot or class will not trigger pattern matching on the LHS of a rule. For example, if the SUM class were redefined to use the pattern-match attribute and the original sum-rectangles rule were used as follows:

```
(defclass SUM
  (is-a USER)
  (slot total (pattern-match non-reactive))))
```

```
(defrule sum-rectangles
  (object (is-a RECTANGLE)
          (height ?height) (width ?width))
?sum <- (object (is-a SUM) (total ?total))
=>
(send ?sum put-total
      (+ ?total (* ?height ?width))))
```

then the following error message would occur when defining the sum-rectangles rule:

```
[OBJRTBLBD2] No objects of existing classes can
satisfy total restriction in object pattern.
```