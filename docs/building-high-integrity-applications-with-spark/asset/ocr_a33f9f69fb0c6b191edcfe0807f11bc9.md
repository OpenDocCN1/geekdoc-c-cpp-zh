# Table 5.4. Truth table for ¬s₁ ∧ (s₂ → (s₃ ∨ (s₁ ↔ s₃)))

| s₁ | s₂ | s₃ | ¬s₁ | s₁ ↔ s₃ | s₃ ∨ (s₁ ↔ s₃) | s₂ → (s₃ ∨ (s₁ ↔ s₃)) | ¬s₁ ∧ (s₂ → (s₃ ∨ (s₁ ↔ s₃))) |
|---|---|---|---|---|---|---|---|
| F | F | F | T | T | T | T | T |
| F | F | T | T | F | T | T | T |
| F | T | F | T | T | T | T | T |
| F | T | T | T | F | T | T | T |
| T | F | F | F | F | F | T | F |
| T | F | T | F | T | T | T | F |
| T | T | F | F | F | F | F | F |
| T | T | T | F | T | T | T | F |

We used Table 5.2 to define the five propositional connectives. Truth tables are also used to show all the possible values of a complex statement. For example, the possible values of the complex statement s₄ defined as

s₄ = ¬s₁ ∧ (s₂ → (s₃ ∨ (s₁ ↔ s₃)))

are given in Table 5.4. This table contains a row for each combination of the three primitive statements (s₁, s₂, s₃) that define s₄. The number of rows in a truth table for a complex statement is 2ⁿ when n is the number of different primitive statements in the definition of the complex statement. The three primitive statements defining s₄ are written as the first three columns of Table 5.4. The eight rows contain all the possible combinations of values of these three inputs. The remaining five columns in the table correspond to the five logical connectives used in the definition of s₄ and are in the order that the connectives would be evaluated from the three inputs.

Certain formulae have the property of being true regardless of the truth values of their constituent statements. These expressions are said to be tautologies. A simple example of a tautology is s₁ ∨ ¬s₁. If s₁ is true, then s₁ ∨ ¬s₁ is true. And if s₁ is false, s₁ ∨ ¬s₁ is still true. Although tautologies might at first glance appear to be uninteresting, they play a very important role in validating arguments, as we will see in Section 5.3.

# 5.2 Logical Equivalence

Look at the fourth column (labeled ¬s₁) and the last column of Table 5.4. The values in these two columns are identical. We say that ¬s₁ and ¬s₁ ∧ (s₂ → (s₃ ∨ (s₁ ↔ s₃))) are logical equivalents. The symbol ↔ is used to indicate the