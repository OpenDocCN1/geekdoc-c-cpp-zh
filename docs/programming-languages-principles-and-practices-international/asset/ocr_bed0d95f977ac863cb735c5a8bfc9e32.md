and then use it to compute heads, tails, and constructed lists, depending on how we instantiate the variables on the left-hand side:

```
 ?- cons(0, [1, 2, 3], A).
A = [0, 1, 2,3]

 ?- cons(X, Y, [1, 2, 3]).
X = 1
Y = [2,3]
```

Thus, we can use variables in a term as either input or output parameters, and Prolog clauses can be “run” backward as well as forward—something the procedural interpretation of Horn clauses did not tell us!

Indeed, unification can be used to shorten clauses such as cons further. Since the = operator is there only to force unification, we can let resolution cause the unification automatically by writing the patterns to be unified directly in the parameters of the head. Thus, the following definition of cons has precisely the same meaning as the previous definition:

```
cons(X, Y, [X|Y]).
```

The appearance of the pattern [X|Y] in place of the third variable automatically unifies it with a variable used in that place in a goal. This process could be referred to as pattern-directed invocation. The functional languages ML and Haskell studied in Chapter 3 have a similar mechanism, and both the runtime systems and the type checkers of these two languages use forms of unification similar to Prolog’s.

Now let’s write an append procedure:

```
append(X, Y, Z) :- X = [], Y = Z.
append(X,Y,Z)   :-
    X = [A|B], Z = [A|W], append(B, Y, W).
```

The first clause states that appending any list to the empty list just gives that list. The second clause states that appending a list whose head is A and tail is B to a list Y gives a list whose head is also A and whose tail is B with Y appended.

Rewriting this using pattern-directed invocation, we get the following extremely concise form:

```
append([], Y, Y).
append([A|B], Y, [A|W]) :- append(B, Y, W).
```

This append can also be run backward and can even find all the ways to append two lists to get a specified list:

```
?- append(X, Y, [1, 2]).
X = []
Y = [1, 2] ->;

X = [1]
Y = [2] ->;

X = [1,2].
Y = []
```