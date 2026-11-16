![](bbox=[0.05, 0.08, 0.95, 0.28])

Figure 1.6: Finding the proposition whose value is computed by a combinational logic circuit. Each wire in the circuit is labeled with the proposition that it represents. The numbering of the labels shows one of the orders in which they can be associated with the wires. The circuit as a whole computes the value of \((\neg(A \land B)) \land (B \lor \neg C)\).

examples of propositions that are in disjunctive normal form:

\(\begin{aligned} &(p \land q \land r) \lor (p \land \neg q \land r \land s) \lor (\neg p \land \neg q) \\ &(p \land \neg q) \\ &(A \land B) \lor (\neg A \land B) \\ &p \lor (\neg p \land q) \lor (\neg p \land \neg q \land r) \lor (\neg p \land \neg q \land \neg r \land w) \end{aligned}\)

Propositions in DNF are just what we need to deal with input/output tables of the type that we have been discussing. Any such table can be computed by a proposition in disjunctive normal form. It follows that it is possible to build a circuit to compute that table using only AND, OR, and NOT gates.

**Theorem 1.3.** Consider a table that lists a logical output value for every combination of values of several propositional variables. Assume that at least one of the output values is true. Then there is a proposition containing those variables such that the value of the proposition for each possible combination of the values of the variables is precisely the value specified in the table. It is possible to choose the proposition to be in disjunctive normal form.

**Proof.** Consider any row in the table for which the output value is T. Form a conjunction of simple terms as follows: For each variable, \(p\), whose value is T in that row, include \(p\) itself in the conjunction; for each variable, \(q\), whose value is F in the row, include \(\neg q\) in the conjunction. The value of the conjunction is T for the combination of variable values given in that