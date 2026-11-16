# Table 2.2 Inference Rules

| Inference Rule | Name |
|---|---|
| \( A, B \vDash A \land B \) | Combination rule CR |
| \( A \land B \vDash A \) | Simplification rule SR |
| \( A \vDash A \lor B \) | Addition rule AR |
| \( A, A \Rightarrow B \vDash B \) | Modus ponens MP |
| \( \neg B, A \Rightarrow B \vDash \neg A \) | Modus tollens MT |
| \( A \Rightarrow B, B \Rightarrow C \vDash A \Rightarrow C \) | Hypothetical syllogism HS |
| \( A \lor B, \neg A \vDash B \) | Disjunctive syllogism DS |
| \( A \Rightarrow B, \neg A \Rightarrow B \vDash B \) | Rule of cases RC |
| \( A \Leftrightarrow B \vDash A \Rightarrow B \) | Equivalence elimination EE |
| \( A \Rightarrow B, B \Rightarrow A \vDash A \Leftrightarrow B \) | Equivalence introduction EI |
| \( A, \neg A \vDash B \) | Inconsistency rule IR |
| \( A \land B \vDash B \land A \) | “and” Commutivity rule ACR |
| \( A \lor B \vDash B \lor A \) | “or” Commutivity rule OCR |
| If \( A_1, A_2, \dots, A_n, B \vDash C \)
then \( A_1, A_2, \dots, A_n \vDash B \Rightarrow C \) | Deduction theorem DT |

It is left as an exercise to obtain the soundness of the other rules in Table 2.2. The next example derives a sound argument using these rules.

**Example 2.18** We use the rules to derive the soundness of the argument in Example 2.16. Again let the following propositions stand for these statements about the world:

+   - P: Randi writes books.
+   - Q: Randi helps other people to write books.
+   - R: Randi earns her living as an editor.

The following derivation determines Randi’s occupation:

| Derivation | Rule |
|---|---|
| 1 P∨Q | Premise |
| 2 ¬P | Premise |
| 3 Q⇒R | Premise |
| 4 Q | 1, 2, DS |
| 5 R | 3, 4, MP |

When we write “Premise” in the Rule column, we mean that the proposition is one of our premises. When, for example, we write “1, 2, DS” in row 4, we mean we are using the premises in rows 2 and 3 and the disjunctive syllogism rule to deduce Q.