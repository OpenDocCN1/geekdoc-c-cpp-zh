Once a formal proof has been constructed, it is convincing. Unfortunately, it's not necessarily easy to come up with the proof. Usually, the best method is a combination of working forward ("Here's what I know, what can I deduce from that?") and working backwards ("Here's what I need to prove, what other things would imply that?"). For this proof, I might have thought: I want to prove $s$. I know that $p \wedge r$ implies $s$, so if I can prove $p \wedge r$, I'm OK. But to prove $p \wedge r$, it'll be enough to prove $p$ and $r$ separately...

Of course, not every argument is valid, so the question also arises, how can we show that an argument is invalid? Let's assume that the argument has been put into general form, with all the specific propositions replaced by propositional variables. The argument is valid if in all cases where all the premises are true, the conclusion is also true. The argument is invalid if there is even one case where all the premises are true and the conclusion is false. We can prove that an argument is invalid by finding an assignment of truth values to the propositional variables which makes all the premises true but makes the conclusion false. For example, consider an argument of the form:

```
p → q
q → (p ∧ r)
r
-----
∴ p
```

In the case where p is false, q is false, and r is true, the three premises of this argument are all true, but the conclusion is false. This shows that the argument is invalid.

To apply all this to arguments stated in English, we have to introduce propositional variables to represent all the propositions in the argument. For example, consider:

John will be at the party if Mary is there and Bill is not there. Mary will be at the party if it's on Friday or Saturday. If Bill is at the party, Tom will be there. Tom won't be at the party if it's on Friday. The party is on Friday. Therefore, John will be at the party.

Let j stand for "John will be at the party," m for "Mary will be there," b for "Bill will be there," t for "Tom will be there," f for "The party is on Friday," and s for "The party is on Saturday." Then this argument has the form