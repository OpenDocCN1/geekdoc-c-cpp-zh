person would not accept that a total stranger was their spouse if they were told that. Because most people recognize that they have imperfect memories, they do not adhere to pure autoepistemic reasoning. Of course, computers do not have this problem until their hard disk crashes.

Autopoietic reasoning is nonmonotonic because the meaning of an autoepistemic statement is context-sensitive. The term context-sensitive means that the meaning changes with the context. As a simple example of context-sensitivity, consider how the word “read” is pronounced in the two sentences:

```
I have read the book
I will read the book
```

The pronunciation of “read” is context sensitive.

Now consider a system consisting of the following two axioms:

```
(∀ x). [Bird(x) ∧ M(Can_fly(x)) → Can_fly (x)]
Bird(Tweety)
```

In this logic system, Can_fly(Tweety) is a theorem derived by unification of Tweety with the variable x and implication.

Now suppose a new axiom is added that states that Tweety cannot fly and thus contradicts the previously derived theorem:

```
~Can_fly(Tweety)
```

The M-operator must change its operation on its argument because now M(Can_fly(Tweety)) is not consistent with the new axiom. In this new context of three axioms, the M-operator would not give a TRUE result for Can_fly(Tweety) because it conflicts with the new axiom. The returned value by the M-operator must be FALSE in this new context, and so the conjunction is FALSE. Thus, there is no implication to produce the theorem Can_fly(Tweety) and no conflict.

One way of implementing this by rules is as follows:

```
IF x is a bird AND x is typical
THEN x can fly
IF x is a bird AND x is nontypical
THEN x cannot fly
```

```
Tweety is a bird
Tweety is nontypical
```

Notice that this system does not invalidate the conclusion Can_fly(Tweety), but rather prevents the incorrect rule from firing at all. This is a much more efficient method of truth maintenance than if we had one rule and the special axiom ~Can_fly(Tweety). Now we have a more general system that can easily handle other nonflying birds such as ostriches without our having to continually add new inferences, which is what the system is supposed to do.