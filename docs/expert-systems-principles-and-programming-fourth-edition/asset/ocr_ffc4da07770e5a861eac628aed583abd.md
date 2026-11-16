```
(printout t "?question " " ?values ")
(bind ?answer (read)))
(return ?answer))
```

Note that you can't replace a defunction with a generic function of the same name and vice versa, so in order to define the check-input defmethod you'd have to delete the check-input defunction. The check-input defmethod that we've just defined will work identically to our original defunction. If we don't define any more methods, there's really no reason to use generic functions rather than the original defunction. So let's examine another portion of the Stick program. Recall from Section 8.9 that three rules were used to determine the number of sticks removed by the human player:

```
(defrule get-human-move
(player-move h)
(pile-size ?size)
(test (> ?size 1))
=>
(printout t
"How many sticks do you wish to take? "
(assert (human-takes (read))))
```

```
(defrule good-human-move
?whose-turn <- (player-move h)
(pile-size ?size)
?number-taken <- (human-takes ?choice)
(test (and (integerp ?choice)
(>= ?choice 1)
(<= ?choice 3)
(< ?choice ?size)))
=>
(retract ?whose-turn ?number-taken)
(printout t "Human made a valid move" crlf)
(assert (player-move h))
```

```
(defrule bad-human-move
?whose-turn <- (player-move h)
(pile-size ?size)
?number-taken <- (human-takes ?choice)
(test (or (not (integerp ?choice))
(< ?choice 1)
(> ?choice ?size)))
=>
(printout t "Human made an invalid move" crlf)
(retract ?whose-turn ?number-taken)
(assert (player-move h)))
```