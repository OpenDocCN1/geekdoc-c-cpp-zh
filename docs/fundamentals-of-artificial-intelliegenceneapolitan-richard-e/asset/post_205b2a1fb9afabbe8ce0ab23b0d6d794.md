
### Table 2.2 Inference Rules

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
| If \( A_1, A_2, \dots, A_n, B \vDash C \)<br>then \( A_1, A_2, \dots, A_n \vDash B \Rightarrow C \) | Deduction theorem DT |

It is left as an exercise to obtain the soundness of the other rules in Table 2.2. The next example derives a sound argument using these rules.

### Example 2.18

We use the rules to derive the soundness of the argument in Example 2.16. Again let the following propositions stand for these statements about the world:

- P: Randi writes books.
- Q: Randi helps other people to write books.
- R: Randi earns her living as an editor.

The following derivation determines Randi’s occupation:

| Derivation | Rule |
|---|---|
| 1 P∨Q | Premise |
| 2 ¬P | Premise |
| 3 Q⇒R | Premise |
| 4 Q | 1, 2, DS |
| 5 R | 3, 4, MP |

When we write “Premise” in the Rule column, we mean that the proposition is one of our premises. When, for example, we write “1, 2, DS” in row 4, we mean we are using the premises in rows 2 and 3 and the disjunctive syllogism rule to deduce Q.

Consider the following quote from Sherlock Holmes concerning a murder case in the novel *A Study in Scarlet*.

> And now we come to the great question as to why. Robbery has not been the object of the murder, for nothing was taken. Was it politics, then, or was it a woman? That is the question which confronted me. I was inclined from the first to the latter supposition. Political assassins are only too glad to do their work and fly. This murder had, on the contrary, been done most deliberately, and the perpetrator had left his tracks all over the room, showing he had been there all the time.

— A. Conan Doyle, *A Study in Scarlet*

### Example 2.19

Let the following propositions stand for these statements about the world:

- P: Robbery was the reason for the murder.
- Q: Something was taken.
- R: Politics was the reason for the murder.
- S: A woman was the reason for the murder.
- T: The murderer left immediately.
- U: The murderer left tracks all over the room.

The following derivation determines the reason for the murder:

| Derivation | Rule |
|---|---|
| 1 ¬Q | Premise |
| 2 P⇒Q | Premise |
| 3 ¬P⇒R∨S | Premise |
| 4 R⇒T | Premise |
| 5 U | Premise |
| 6 U⇒¬T | Premise |
| 7 ¬P | 1, 2, MT |
| 8 R∨S | 3, 7, MP |
| 9 ¬T | 5, 6, MP |
| 10 ¬R | 4, 9, MT |
| 11 S | 8, 10, DS |

So we conclude that a woman was the reason for the murder.

A deduction system is **complete** if it can derive every sound argument. The set of rules in Table 2.2 is complete. However, it would not be complete if we removed the last rule called the *Deduction theorem*. Notice that this rule differs from the others. All the other rules concern arguments in which there are premises. The Deduction theorem is needed to derive arguments in which there are no premises. An argument without premises is simply a tautology.

### Example 2.20

We derive that \(\vdash A \lor \neg A\). Note that no premises appear before the \(\vdash\) symbol. So this is an argument without premises, which is a tautology if it is sound. We use the rules in Table 2.2 to derive its soundness.

| Derivation | Rule | Comment |
|---|---|---|
| 1 \(A\) | Assumption | We assume \(A\). |
| 2 \(A \lor \neg A\) | 1, AR | |
| 3 \(A \Rightarrow A \lor \neg A\) | 1, 2, DT | We now discharge \(A\). |
| 4 \(\neg A\) | Assumption | We assume \(\neg A\). |
| 5 \(\neg A \lor A\) | 4, AR | |
| 6 \(A \lor \neg A\) | 5, CR | |
| 7 \(\neg A \Rightarrow A \lor \neg A\) | 4, 6, DT | We now discharge \(\neg A\). |
| 8 \(A \lor \neg A\) | 3, 7, RC | |

Notice that to use the Deduction theorem, we first temporarily assume a proposition to be true (e.g., step 1), then we conclude that a second proposition is true (e.g., step 2), and finally we conclude that the assumed proposition implies the second proposition (e.g., step 3). At this point we *discharge* the assumed proposition because we do not really know it to be true. We just temporarily assumed this so as to derive an implication.

## 2.2 Resolution

Although a logical human such as Sherlock Holmes might reason similar to our derivation in Example 2.19, it is not straightforward to convert this reasoning strategy to a computer program. Next we develop a different derivation strategy called **resolution theorem proving**. This is the strategy used in many automatic reasoning programs. First, we need to introduce normal forms.

### 2.2.1 Normal Forms

We start with some definitions.

### Definition 2.5

A literal is a proposition of the form P or \(\neg P\), where P is an atomic proposition other than True or False.\(\blacksquare\)

### Definition 2.6

A conjunctive clause is a conjunction of literals.\(\blacksquare\)

### Definition 2.7

A disjunctive clause is a disjunction of literals.\(\blacksquare\)

### Definition 2.8

A proposition is in disjunctive normal form if it is the disjunction of conjunctive clauses.♦

### Definition 2.9

A proposition is in conjunctive normal form if it is the conjunction of disjunctive clauses.♦

### Example 2.21

The following propositions are in disjunctive normal form:

(P ∧ Q) ∨ (R ∧ ¬P)

(P ∧ Q ∧ ¬R) ∨ (S) ∨ (¬Q ∧ T)

The following proposition is not in disjunctive normal form because R∨S∧Q is not a conjunctive clause:

(P ∧ Q) ∨ (R ∨ S ∧ Q)

The following propositions are in conjunctive normal form:

(P ∨ Q) ∧ (R ∨ ¬P)

(P ∨ Q ∨ ¬R) ∧ (S) ∧ (¬Q ∨ T)

The following proposition is not in conjunctive normal form because R∨S∧Q is not a disjunctive clause:

(P ∨ Q) ∧ (R ∨ S ∧ Q)

Any proposition can be converted to a logically equivalent proposition in conjunctive (or disjunctive) normal form. Next we present an algorithm that accomplishes this task in the case of conjunctive normal form (the laws mentioned are the ones in Table 2.1). We use a straightforward pseudocode to show algorithms in this text. The keyword var is used to denote “pass by reference,” which for our purposes means the variable is an output of the algorithm.

### Algorithm 2.1 Conjunctive_Normal_Form

- Input: A proposition.
- Output: A logically equivalent proposition in conjunctive normal form.

```
Procedure Conjunctive_Normal_form(var Proposition);
remove all "↔" symbols using the if and only if elimination law;
remove all "→" symbols using the implication elimination law;
repeat
    if there are any double negations
        remove them using the double negation law;
    if there are any negations of non-atomic propositions
        remove them using DeMorgan's laws;
until the only negations are single negations of atomic propositions;
repeat
    if there are any disjunctions in which one or more terms is a conjunction
        remove them using these laws:
    A ∨ (B ∧ C) ≡ (A ∨ B) ∧ (A ∨ C)   (2.1)
    (A ∧ B) ∨ C ≡ (A ∨ C) ∧ (B ∨ C);   (2.2);
until Proposition is in conjunctive normal form;
```

Equivalence 2.1 is the Distributivity law in Table 2.1 and Equivalence 2.2 can be derived from the Commutivity and Distributivity laws.

### Example 2.22

We use Algorithm 2.1 to convert ¬((P ⇒ Q) ∧ ¬R) to conjunctive normal form:

- ¬((P ⇒ Q) ∧ ¬R) ≡ ¬((¬P ∨ Q) ∧ ¬R) implication elimination
- ≡ ¬(¬P ∨ Q) ∨ ¬¬R DeMorgan's laws
- ≡ ¬(¬P ∨ Q) ∨ R double negation
- ≡ (¬¬P ∧ ¬Q) ∨ R DeMorgan's laws
- ≡ (P ∧ ¬Q) ∨ R double negation
- ≡ (P ∨ R) ∧ (¬Q ∨ R) Equiv. 2.2

### Example 2.23

We use Algorithm 2.1 to convert (P ∧ Q) ∨ (R ∧ S) to conjunctive normal form:

- (P ∧ Q) ∨ (R ∧ S) ≡ ((P ∧ Q) ∨ R) ∧ ((P ∧ Q) ∨ S) Equiv. 2.1
- ≡ (P ∨ R) ∧ (Q ∨ R) ∧ ((P ∧ Q) ∨ S) Equiv. 2.2
- ≡ (P ∨ R) ∧ (Q ∨ R) ∧ (P ∨ S) ∧ (Q ∨ S) Equiv. 2.2
