| Expression | Rule |
|---|---|
| ¬(q → q) ∨ (p ∧ q) |  |
| ¬(¬q ∨ p) ∨ (p ∧ q) | Conditional as disjunction |
| (¬(¬q) ∧ ¬p) ∨ (p ∧ q) | De Morgan |
| (q ∧ ¬p) ∨ (p ∧ q) | Double negation |
| (q ∧ ¬p) ∨ (q ∧ p) | Commutative |
| q ∧ (¬p ∨ p) | Distributive |
| q ∧ True | Compliment |
| q | Identity |

# 5.3 Arguments and Inference

An argument is an attempt to convince someone of something. In formal logic, an argument is expressed by a set of statements called premises that together support the truth of another statement called a conclusion. Here is an example of an argument with two premises followed by a conclusion:

If Horace swallowed Sodium Azide, then Horace was poisoned.
Horace swallowed Sodium Azide.
Therefore, Horace was poisoned.

All arguments can be expressed in the following form:

(p₁ ∧ p₂ ∧ p₃ ∧ p₄ ∧ p₅ ∧ p₆ … ∧ pₙ) → c

where the p’s are the premises and c is the conclusion. Informally, this statement says that if all of the premises are true, then the conclusion is true. As premises in a poorly constructed argument can have no relationship to the conclusion, having true premises is not sufficient to show that the conclusion is true. We need to be concerned with the form of the argument. An argument is said to be valid if this implication is a tautology. Only when an argument is valid is the conclusion a logical consequence of its premises.

Consider the poisoning argument given at the beginning of this section. If we use s₁ to represent “Horace swallowed Sodium Azide” and s₂ to represent “Horace was poisoned,” we can write the argument formally as

((s₁ → s₂) ∧ s₁) → s₂

One way to demonstrate that this statement is a tautology, and therefore a valid argument, is to construct a truth table as we have done in Table 5.6. There you can see that no matter what the values of the inputs s₁ and s₂, the value of the argument, ((s₁ → s₂) ∧ s₁) → s₂, is true. Note that there is only one row