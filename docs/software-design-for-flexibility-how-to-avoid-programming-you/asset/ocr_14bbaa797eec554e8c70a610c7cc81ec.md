```
(cdr var-first))
terms)
dict succeed fail)
((grab-segment var-first terms)
dict succeed fail)))
maybe-grab)
```

The procedure grab-segment is where the segment matching and backtracking actually happen. The term list is broken into two parts: an initial segment (initial) and the rest of the terms (terms*). The initial segment (initial) starts out empty and terms* is the whole term list. The match tries to proceed with the segment variable bound to initial. If that fails, the failure continuation tries to match with an element moved from terms* to initial. This is repeated until either a match succeeds or the match of the entire term list:

```
(define (grab-segment var-first terms))
(define (grab dict succeed fail))
(let ((var (car var-first)))
(let slp ((initial '()) (terms*))
(define (continue)
(if null? terms*)
(fail)
(slp append initial (list car terms*))
(cdr terms*)))
(let ((dict* (do-substitute var initial dict))
(if dict*
(succeeded dict* continue (cdr var-first) terms*)
(continue))))
```

This appears to be all that is required to make a unifier with an experimental extension for segment variables. With segment variables we must get multiple matches. We can reject a match, forcing the program to backtrack, to get an alternative. Note that each dictionary entry is a list containing the name of the variable, the value, and the type of the variable.

We can use the unifier as a one-sided matcher. For example, there are exactly two ways to match the distributive law pattern to the we see:13