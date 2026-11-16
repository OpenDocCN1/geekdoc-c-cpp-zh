```
(node (name ?name) (type answer)
     (answer ?value))
(not (answer ?))
=>
(printout t "I guess it is a " ?value crlf)
(assert
(answer (ask-yes-or-no "Am I correct?"))))
```

If the answer is something other than yes or no, then the bad-answer rule will cause another activation of the ask-if-answer-node-is-incorrect rule. If the answer is yes or no, then one of the two rules below will be fired. If the value of the answer node is verified, then the ask-try-again fact is asserted to indicate the user should be asked to continue. If the answer is wrong, then learning will occur and the replace-answer-node fact is asserted to indicate the name of the node to be replaced. In either case the current-node and answer facts are retracted:

```
(defrule answer-node-guess-is-correct
?node <- (current-node ?name)
(node (name ?name) (type answer))
?answer <- (answer yes)
=>
(assert (ask-try-again'))
(retract ?node ?answer))
```

```
(defrule answer-node-guess-is-incorrect
?node <- (current-node ?name)
(node (name ?name) (type answer))
?answer <- (answer no)
=>
(assert (replace-answer-node ?name))
(retract ?node ?answer))
```

The following three rules are used to determine whether the user wants to continue. The ask-try-again rule asks the “Try again?” question. Once again, the bad-answer rule will fire if other than a yes or no answer is given. If the answer is yes, the one-more-time rule will reset the current-node fact to the root node to begin the guessing process again. If the answer is no, the facts representing the decision tree are saved to the animal.dat file using the save-facts command:

```
(defrule ask-try-again
(ask-try-again)
(not (answer ?))
=>
(assert (answer (ask-yes-or-no "Try again?"))))
```

```
(defrule one-more-time
?phase <- (ask-try-again)
```