extends pmove by removing the piece at coords. The position specified by coords must contain an opponent's piece. The operation also sets a flag in the new change object saying that a piece was captured; the resulting pmove always satisfies captures-pieces?

# An executive

To separate the control structure from the rules of checkers we build a executive that captures the control structure without incorporating the specific content of the rules. In this kind of game there are two kinds of rule. One kind, which we will call an evolution rule, augments a pmove, possibly returning multiple derived pmoves. The other kind, an aggregate rule, acts on a set of pmoves, eliminating some that are not allowed or extending some to incorporate changes, as crowning the king.

Here is an executive that starts with some empty pmoves, one for each of the player's pieces, and evolves these into a collection of pmoves that represent finished pmoves. It applies the aggregate rules to the collection of finished pmoves, ultimately returning a collection of the legal moves.

An evolution rule is implemented as a procedure that transforms a given pmove into a collection of new pmoves, some of which may be finished (satisfy is-pmove-finished?). The executive recursively applies all of the evolution rules to the collection of pmoves until all of them are finished.

An aggregate rule is implemented as a procedure that accepts a collection of finished pmoves and produces a new collection. Each aggregate rule is applied once, and there are no ordering constraints between aggregate rules, so the executive can compose them together into a single procedure that the composite aggregate rule. If there are no aggregate rules, then the composite simply returns its argument.

```
(define execute-rules initial-pmoves evolution-rules
(aggregate-rules)
((reduce compose (lambda (x) x) aggregate-rules)
(append-map (lambda (pmove)
(evolve-pmove pmove evolution-rules))
initial-pmoves)))
```