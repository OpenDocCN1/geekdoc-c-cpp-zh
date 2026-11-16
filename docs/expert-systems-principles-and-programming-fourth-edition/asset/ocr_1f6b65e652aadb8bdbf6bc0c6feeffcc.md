# # APPENDIX A
# Some Useful Equivalences

~~p ≡ p
p → q ≡ ¬p ∨ q ≡ ¬q → ¬p
¬(p ∧ q) ≡ ¬p ∨ ¬q
¬(p ∨ q) ≡ ¬p ∧ ¬q
p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)
p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)
(p ∧ q) ∧ r ≡ p ∧ (q ∧ r)
(p ∨ q) ∨ r ≡ p ∨ (q ∨ r)
p ∧ q ≡ q ∧ p
p ∨ q ≡ q ∨ p

¬(∀x) P(x) ≡ (∃x) ¬P(x)
¬(∃x) P(x) ≡ (∀x) ¬P(x)
(∀x) P(x) ∧ (∀x) Q(x) ≡ (∀x) (P(x) ∧ Q(x))
(∃x) P(x) ∨ (∃x) Q(x) ≡ (∃x) (P(x) ∨ Q(x))

Note: The ∀ does not distribute over an ∨, and ∃ does not distribute over ∧, so a new dummy variable, z, is needed in the following two equivalences.

(∀x) P(x) ∨ (∀x) Q(x) ≡ (∀x) P(x) ∨ (∀z) Q(z)
≡ (∀x) (∀z) (P(x) ∨ Q(z))
(∃x) P(x) ∧ (∃x) Q(x) ≡ (∃x) P(x) ∧ (∃z) Q(z)
≡ (∃x) (∃z) (P(x) ∧ Q(z))