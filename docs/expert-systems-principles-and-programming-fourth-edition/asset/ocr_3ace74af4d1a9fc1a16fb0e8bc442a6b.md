This program will end when a valid choice for the number of sticks taken has been entered. Once again, a control fact is used to retrigger a rule to allow invalid responses to be reentered. The bad-human-move rule will reassert the control fact (player-move h) to reactivate the get-human-move rule. The human player can then reenter the number of sticks to be taken from the pile.

# 8.10 THE PREDICATE FIELD CONSTRAINT

The predicate field constraint, ., is useful for performing predicate tests directly within patterns. In many ways it is similar to performing a test CE directly after a pattern, although in some cases, as will be discussed in Chapter 9, it is more efficient to use the predicate field constraint than it is to use a test CE. The predicate field constraint can be used just like a literal field constraint. It can stand by itself in a field or be used as one part of a more complex field using the ~, &, and I connective field constraints. The predicate field constraint is always followed by a function for evaluation. As with a test CE, this function should be a predicate function.

As an example, the get-human-move rule in the previous section used the following two patterns to check that the pile contained more than one stick:

```
(pile-size ?size)
(test (> ?size 1))
```

These two patterns could be replaced with the following single pattern:

```
(pile-size ?size&:(> ?size 1))
```

The predicate field constraint can be used by itself; however, there are few situations in which this is useful. Typically a variable is bound and then tested using the predicate field constraint. When reading a pattern it is useful to think of the predicate field constraint as meaning such that. For example, the field constraint shown previously,

```
?size&:(> ?size 1)
```

could be read as "bind ?size such that ?size is greater than 1."

One application of the predicate field constraint is error checking of data. For example, the following rule checks that a data item is numeric before adding it to a running total:

```
(defrule add-sum
  (data-item ?value&:(numberp ?value))
  ?old-total <- (total ?total)
  =>
  (retract ?old-total)
  (assert (total (+ ?total ?value))))
```