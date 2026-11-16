
no logical choice but to believe q. This applies no matter what p and q represent. For example, if you believe “If Jill is breathing, then Jill pays taxes,” and you believe that “Jill is breathing,” logic forces you to believe that “Jill pays taxes.” Note that we can’t say for sure that the conclusion is true, only that if the premises are true, then the conclusion must be true.

This fact can be rephrased by saying that ((p → q) ∧ p) → q is a tautology. More generally, for any compound propositions P and Q, saying “P → Q is a tautology” is the same as saying that “in all cases where P is true, Q is also true.”11 We will use the notation P ⇒ Q to mean that P ⇒ Q is a tautology. Think of P as being the premise of an argument or the conjunction of several premises. To say P ⇒ Q is to say that Q follows logically from P. We will use the same notation in both propositional logic and predicate logic. (Note that the relation of ⇒ to → is the same as the relation of ≡ to ↔.)

### Definition 1.9. Let P and Q be any formulas in either propositional logic or predicate logic. The notation P ⇒ Q is used to mean that P → Q is a tautology. That is, in all cases where P is true, Q is also true. We then say that Q can be logically deduced from P or that P logically implies Q.

An argument in which the conclusion follows logically from the premises is said to be a valid argument. To test whether an argument is valid, you have to replace the particular propositions or predicates that it contains with variables, and then test whether the conjunction of the premises logically implies the conclusion. We have seen that any argument of the form

```
p → q
p
-----
∴ q
```

is valid, since ((p → q) ∧ p) → q is a tautology. This rule of deduction is called modus ponens. It plays a central role in logic. Another, closely related rule is modus tollens, which applies to arguments of the form

```
p → q
¬q
-----
∴ ¬p
```

To verify that this is a valid argument, just check that \(((p \to q) \wedge \neg q) \implies \neg p\), that is, that \(((p \to q) \wedge \neg q) \to \neg p\) is a tautology. As an example, the following argument has the form of *modus tollens* and is therefore a valid argument:

> If Keanu Reeves is a good actor, then I'm the king of France
> I am not the king of France
> ∴ Keanu Reeves is not a good actor

You should note carefully that the validity of this argument has nothing to do with whether or not Keanu Reeves can act well. The argument forces you to accept the conclusion *only if* you accept the premises. You can logically believe that the conclusion is false, as long as you believe that at least one of the premises is false.

Another named rule of deduction is the **Law of Syllogism**, which has the form

```
p → q
q → r
∴ p → r
```

For example:

> If you study hard, you do well in school
> If you do well in school, you get a good job
> ∴ If you study hard, you get a good job

There are many other rules. Here are a few that might prove useful. Some of them might look trivial, but don't underestimate the power of a simple rule when it is combined with other rules.

| p ∨ q | p | p ∧ q | p |
| --- | --- | --- | --- |
| ¬ p | q | ∴ p | ∴ p ∨ q |
| ∴ q | ∴ p ∧ q | | |

Logical deduction is related to logical equivalence. We defined P and Q to be logically equivalent if P ↔ Q is a tautology. Since P ↔ Q is equivalent to (P → Q) ∧ (Q → P), we see that P ≡ Q if and only if both P ⇒ Q and P ⇐ Q. Thus, we can show that two statements are logically equivalent if we can show that each of them can be logically deduced from the other. Also, we get a lot of rules about logical deduction for free—two rules of deduction for each logical equivalence we know. For example, since ¬(p ∧ q) ≡ (¬p ∨ ¬q), we get that ¬(p ∧ q) ⇒ (¬p ∨ ¬q). For example, if we know “It is not both sunny and warm,” then we can logically deduce “Either it’s not sunny or it’s not warm.” (And vice versa.)

In general, arguments are more complicated than those we’ve considered so far. Here, for example, is an argument that has five premises:

```
(p ∧ r) → s
q → p
t → r
q
t
∴ s
```

Is this argument valid? Of course, you could use a truth table to check whether the conjunction of the premises logically implies the conclusion. But with five propositional variables, the table would have 32 lines, and the size of the table grows quickly when more propositional variables are used. So, in general, truth tables are not practical.

Fortunately, there is another way to proceed, based on the fact that it is possible to chain several logical deductions together. That is, if \(p \Rightarrow Q\) and \(Q \Rightarrow \mathcal{R}\), it follows that \(p \Rightarrow \mathcal{R}\). This means we can demonstrate the validity of an argument by deducing the conclusion from the premises in a sequence of steps. These steps can be presented in the form of a proof:

### Definition 1.10. A formal proof that an argument is valid consists of a sequence of propositions such that the last proposition in the sequence is the conclusion of the argument, and every proposition in the sequence is either a premise of the argument or follows by logical deduction from propositions that precede it in the list.

The existence of such a proof shows that the conclusion follows logically from the premises, and therefore that the argument is valid. Here is a formal proof that the argument given above is valid. The propositions in the proof are numbered, and each proposition has a justification.

- 1. \(q \to p\) premise
- 2. \(q\) premise
- 3. \(p\) from 1 and 2 (modus ponens)
- 4. \(t \to r\) premise
- 5. \(t\) premise
- 6. \(r\) from 4 and 5 (modus ponens)
- 7. \(p \land r\) from 3 and 6
- 8. \((p \land r) \to s\) premise
- 9. \(s\) from 7 and 8 (modus ponens)

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
