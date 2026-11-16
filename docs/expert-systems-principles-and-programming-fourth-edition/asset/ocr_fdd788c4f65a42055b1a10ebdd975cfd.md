```
CLIPS> (watch compilations).
CLIPS> (load "rules.clp").
Defining defrule: sharing-1 +j+j++j+j
Defining defrule: sharing-2 =j=j=j+j
TRUE
CLIPS>
```

The +j in the output indicates that a join is being added, whereas =j indicates that a join is being shared. Thus when rule sharing-1 is added four new joins are created. When rule sharing-2 is added, it shares its first three joins with rule sharing-1 and creates a new join for its last pattern. Notice that CLIPS has used four joins to represent the rule, as opposed to the three joins that would normally be required. For implementation reasons it is convenient to have only one pattern per join; so instead of using one join for the first two patterns, CLIPS uses two joins.

# 9.12 THE IMPORTANCE OF PATTERN ORDER

Programmers new to rule-based languages often have misconceptions about the importance of ordering the patterns in rules correctly for both speed and memory efficiency. Since the Rete algorithm saves the state from one cycle to the next, it is very important to make sure that rules do not generate large numbers of partial matches. For example, consider the following simple program:

```
(deffacts information
    (find-match a c e g)
    (item a)
    (item b)
    (item c)
    (item d)
    (item e)
    (item f)
    (item g))
```

```
(defrule match-1
    (find-match ?x ?y ?z ?w)
    (item ?x)
    (item ?y)
    (item ?z)
    (item ?w)
    =>
    (assert (found-match ?x ?y ?z ?w)))
```

This program will reset very quickly. A watch facts command followed by a reset command will verify this. Now consider the following program:

```
(deffacts information
    (find-match a c e g)
```