```
(bind ?answer (read))
(while (and (neq ?answer yes) (neq ?answer no))
  (printout t ?question " (yes or no) ")
  (bind ?answer (read)))
(return ?answer))
```

```
(defrule ask-decision-node-question
  ?node <- (current-node ?name)
  (node (name ?name)
        (type decision)
        (question ?question))
  (not (answer ?))
  =>
  (assert (answer (ask-yes-or-no ?question)))))
```

The second pattern matches against the current node only if it is a decision node. The third pattern checks that the question hasn't already been answered. In the RHS of the rule, the ask-yes-or-no defunction repeatedly asks the question until an answer of either yes or no is supplied. One of the following two rules will be fired in response to the answer:

```
(defrule proceed-to-yes-branch
  ?node <- (current-node ?name)
  (node (name ?name)
        (type decision)
        (yes-node ?yes-branch))
  ?answer <- (answer yes)
  =>
  (retract ?node ?answer)
  (assert (current-node ?yes-branch))))
```

```
(defrule proceed-to-no-branch
  ?node <- (current-node ?name)
  (node (name ?name)
        (type decision)
        (no-node ?no-branch))
  ?answer <- (answer no)
  =>
  (retract ?node ?answer)
  (assert (current-node ?no-branch))))
```

In both rules, the current-node fact is retracted and then updated with a new assertion that depends on the answer to the question. The answer fact will be retracted so that the ask-decision-node-question rule will be activated again.

The next rule asks whether an answer node has made the correct guess. It acts similarly to the ask-decision-node-question rule:

```
(defrule ask-if-answer-node-is-correct
  ?node <- (current-node ?name)
```