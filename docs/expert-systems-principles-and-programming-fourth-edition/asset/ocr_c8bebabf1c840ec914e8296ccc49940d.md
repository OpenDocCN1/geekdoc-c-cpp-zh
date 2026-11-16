is in conjunctive normal form. The terms within parentheses are clauses:

```
A v B and -B v C
```

As will be shown later, any predicative logic wff, which includes propositional logic as a special case, can be written as clauses. The full clausal form can express any predicative logic formula but may not be as natural or readable for a person. The syntax of PROLOG is the Horn clause subset, which makes mechanical theorem proving by PROLOG much easier and efficient to implement than standard predicate logic notation or full clausal form. As mentioned in Chapter 1, PROLOG allows only one head. A full clausal form expression is generally written in a special form called Kowalski clausal form:

```
A1, A2, ... An -> B1, B2, ... Bm
```

which is interpreted as saying that if all the subgoals A1, A2, ... An are true, then one or more of B1, or B2, ... or Bm are also true. Note that sometimes the direction of the arrow is reversed in this notation. This clause, written in standard predicate notation, is:

```
A1 ^ A2 ... An -> B1 v B2 ... Bm
```

This can be expressed in disjunctive form as the disjunction of literals using the equivalence:

```
P -> Q == -P v Q
```

so:

```
A1 ^ A2 ... An -> B1 v B2 ... Bm
== -(A1 ^ A2 ... An) v (B1 v B2 ... Bm)
== -A1 v ~A2 ... ~An v B1 v B2 ... Bm
```

where de Morgan's law:

```
-(P ^ Q) == -P v ~Q
```

is used to simplify the last expression.

As discussed in Chapter 1, PROLOG uses a restricted type of clausal form, the Horn clause, in which only one head is allowed:

```
A1, A2, ... An -> B
```

which is written in PROLOG syntax as:

```
B :- A1, A2, ... An
```