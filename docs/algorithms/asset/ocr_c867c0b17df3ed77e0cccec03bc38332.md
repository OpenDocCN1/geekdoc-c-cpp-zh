# 5.3 Horn formulas

In order to display human-level intelligence, a computer must be able to perform at least some modicum of logical reasoning. Horn formulas are a particular framework for doing this, for expressing facts and deriving conclusions.

The most primitive object in a Horn formula is a Boolean variable, taking either true or false. For instances, x, y, and z might denote the possibilities.

```
x ≡ the murder took place in the kitchen
y ≡ the butler is innocent
z ≡ the colonel was asleep at 8 pm
```

A literal is a variable x or its negation ¬ ("NOT x”). In Horn formulas, knowledge about variables is represented by two kinds of clauses:

+   1. Implications, whose left-hand side is an AND of any number of positive literals and whose right-hand side is a single positive literal. These statements of the form "if the conditions on the left hold, then the one on the right might also be true." For instance,

```
(x ∨ u) → u
```

might mean "if the colonel was asleep at 8 pm and the murder took place at 8 pm then the colonel is innocent." A degenerate implication is the singleton → x, meaning that x is true: "the murder definitely occurred in the kitchen."

+   2. Pure negative clauses, consisting of an OR of any number of negative literals, in

```
(u ∨ v ∨ y)
```

“they can't all be innocent”.

Given a set of clauses of these two, the goal is to determine whether there is a consistent explanation: an assignment of true/false values to the variables that satisfies all the clauses. This is also called a satisfying assignment.

The two kinds of clauses pull us in different directions. The implications encourage us to make some of the variables to true, while the negative clauses encourage us to make them false. Our strategy for solving a Horn formula is: We start with all variables false. We then proceed to set some of them to true, one by one, very reluctantly, and only if we absolutely have to because an implication would otherwise be violated. Once we are done with this phase and all implications are satisfied, only then do we turn to the negative clauses and make sure they are all satisfied.

In other words, our algorithm for Horn clauses is the following greedy scheme (stingy is perhaps more descriptive):