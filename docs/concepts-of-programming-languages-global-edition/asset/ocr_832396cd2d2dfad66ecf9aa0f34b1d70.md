positive information. For example, most people have 364 more unbirthdays than they have birthdays.

A simple alternative solution is to state in the goal that X must not be the same as Y, as in

```
sibling(X, Y) :- parent(M, X), parent(M, Y), not(X = Y).
```

In other situations, the solution is not so simple.

The Prolog not operator is satisfied in this case if resolution cannot satisfy the subgoal X = Y. Therefore, if the not succeeds, it does not necessarily mean that X is not equal to Y; rather, it means that resolution cannot prove from the database that X is the same as Y. Thus, the Prolog not operator is not equivalent to a logical NOT operator, in which NOT means that its operand is probably true. This nonequivalency can lead to a problem if we happen to have a goal of the form

```
not(not(some_goal)).
```

which would be equivalent to

```
some_goal.
```

if Prolog's not operator were a true logical NOT operator. In some cases, however, they are not the same. For example, consider again the member rules:

```
member(Element, [Element | _]) :- !.
member(Element, [_ | List]) :- member(Element, List).
```

To discover one of the elements of a given list, we could use the goal

```
member(X, [mary, fred, barb]).
```

which would cause X to be instantiated with mary, which would then be printed. But if we used

```
not(not(member(X, [mary, fred, barb]))).
```

the following sequence of events would take place: First, the inner goal would succeed, instantiating X to mary. Then, Prolog would attempt to satisfy the next goal:

```
not(member(X, [mary, fred, barb])).
```

This statement would fail because member succeeded. When this goal failed, X would be uninstantiated, because Prolog always uninstantiates all variables in all goals that fail. Next, Prolog would attempt to satisfy the outer not goal,