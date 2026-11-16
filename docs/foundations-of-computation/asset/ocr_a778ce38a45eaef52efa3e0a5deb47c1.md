Substitution Law: The equivalence \( Q \equiv R \) allows us to substitute \( R \) for \( Q \) in the statement \( P \equiv Q \), giving \( P \equiv R \). (Remember that, by Definition 1.4, logical equivalence is defined in terms of a proposition.) This means that we can show that two compound propositions are logically equivalent by finding a chain of logical equivalences that lead from one to the other. For example:

```
p \land (p \to q) \equiv p \land (\neg p \lor q) \quad \text{definition of } p \to q, \text{ Theorem 1.2}
\equiv (p \land \neg p) \lor (p \land q) \quad \text{Distributive Law}
\equiv \mathbb{F} \lor (p \land q) \quad \text{Law of Contradiction, Theorem 1.2}
\equiv (p \land q) \quad \text{Identity Law}
```

Each step in the chain has its own justification. In several cases, a substitution law is used without stating as much. In the first line, for example, the definition of \( p \to q \) is that \( p \to q \equiv \neg p \lor q \). The Second Substitution Law allows us to substitute \( (\neg p \lor q) \) for \( (p \to q) \). In the last line, we implicitly applied the First Substitution Law to the Identity Law, \( \mathbb{F} \lor p \equiv p \), to obtain \( \mathbb{F} \lor (p \land q) \equiv (p \land q) \).

The chain of equivalences in the above example allows us to conclude that \( p \land (p \to q) \) is logically equivalent to \( p \land q \). This means that if you were to make a truth table for these two expressions, the truth values in the column for \( p \land (p \to q) \) would be identical to those in the column for \( p \land q \). We know without actually making the table. In this case, the table would only be four lines long and easy enough to make. But Boolean algebra can be applied in cases where the number of propositional variables is too large for a truth table to be practical.

Let's do another example. Recall that a compound proposition is a tautology if it is true for all possible combinations of truth values of the propositional variables that it contains. But another way of saying the same thing is that \( P \) is a tautology if \( P \equiv T \). So, we can prove that a compound proposition, \( P \), is a tautology by finding a chain of logical equivalences