
![](img/e1667d904eba93816cbfc3a4b0128062_27_0.png)

Figure 1.6: Finding the proposition whose value is computed by a combinational logic circuit. Each wire in the circuit is labeled with the proposition that it represents. The numbering of the labels shows one of the orders in which they can be associated with the wires. The circuit as a whole computes the value of \((\neg(A \land B)) \land (B \lor \neg C)\).

examples of propositions that are in disjunctive normal form:

\(\begin{aligned} &(p \land q \land r) \lor (p \land \neg q \land r \land s) \lor (\neg p \land \neg q) \\ &(p \land \neg q) \\ &(A \land B) \lor (\neg A \land B) \\ &p \lor (\neg p \land q) \lor (\neg p \land \neg q \land r) \lor (\neg p \land \neg q \land \neg r \land w) \end{aligned}\)

Propositions in DNF are just what we need to deal with input/output tables of the type that we have been discussing. Any such table can be computed by a proposition in disjunctive normal form. It follows that it is possible to build a circuit to compute that table using only AND, OR, and NOT gates.

**Theorem 1.3.** Consider a table that lists a logical output value for every combination of values of several propositional variables. Assume that at least one of the output values is true. Then there is a proposition containing those variables such that the value of the proposition for each possible combination of the values of the variables is precisely the value specified in the table. It is possible to choose the proposition to be in disjunctive normal form.

**Proof.** Consider any row in the table for which the output value is T. Form a conjunction of simple terms as follows: For each variable, \(p\), whose value is T in that row, include \(p\) itself in the conjunction; for each variable, \(q\), whose value is F in the row, include \(\neg q\) in the conjunction. The value of the conjunction is T for the combination of variable values given in that row of the table, since each of the terms in the conjunction is true for that combination of variables. Furthermore, for any *other* possible combination of variable values, the value of the conjunction will be F, since at least one of the simple terms in the conjunction will be false.

Take the disjunction of all such conjunctions constructed in this way, for each row in the table where the output value is true. This disjunction has the value T if and only if one of the conjunctions that make it up has the value T—and that is precisely when the output value specified by the table is T. So, this disjunction of conjunctions satisfies the requirements of the theorem.

As an example, consider the table in Figure 1.7. This table specifies a desired output value for each possible combination of values for the propositional variables p, q, and r. Look at the second row of the table, where the output value is true. According to the proof of the theorem, this row corresponds to the conjunction ((p ∧ ¬q) ∧ r). This conjunction is true when p is false, q is false, and r is true; in all other cases it is false. The other two rows where the output is true give two more conjunctions. The three conjunctions produce the DNF proposition ((p ∧ ¬q ∧ r) ∨ (p ∧ q ∧ r) ∨ (p ∧ q ∧ r)). This proposition computes all the output values specified in the table. Using this proposition as a blueprint, we get a logic circuit whose outputs match those given in the table.

Now, given any combinatorial logic circuit, there are many other circuits that have the same input/output behavior. When two circuits have the same input/output table, the compound propositions associated with the two circuits are logically equivalent. To put this another way, propositions that are logically equivalent produce circuits that have the same input/output behavior. As a practical matter, we will usually prefer the circuit that is simpler. The correspondence between circuits and propositions allows us to apply Boolean algebra to the simplification of circuits.

For example, consider the DNF proposition corresponding to the table in Figure 1.7. In ((p ∧ ¬q ∧ r) ∨ (p ∧ q ∧ r) ∨ (p ∧ q ∧ r)), we can factor (q ∧ r) from the last two terms, giving ((p ∧ ¬q ∧ r) ∨ ((p ∨ p) ∧ (q ∧ r))). Since ¬p ∨ p ≡ T, and T ∧ Q ≡ Q for any proposition Q, this can be simplified to ((p ∧ ¬q ∧ r) ∨ (q ∧ r)). Again, we can apply the distributive law to this to factor out an r, giving ((p ∧ ¬q) ∨ q) ∧ r). This compound proposition is logically equivalent to the one we started with, but implementing it in a circuit requires only five logic gates, instead of the ten required by the original proposition.

| p | q | r | output |
|---|---|---|---|
| F | F | F | F |
| F | F | T | T |
| F | T | F | F |
| F | T | T | F |
| T | F | F | T |
| T | F | T | F |
| T | T | F | F |
| T | T | T | T |

Figure 1.7: An input/output table specifying a desired output for each combination of values of the propositional variables p, q, and r. Each row where the output is T corresponds to a conjunction, shown next to that row in the table. The disjunction of these conjunctions is a proposition whose output values are precisely those specified by the table.

If you start with a circuit instead of a proposition, it is often possible to find the associated proposition, simplify it using Boolean algebra, and use the simplified proposition to build an equivalent circuit that is simpler than the original.

All this explains nicely the relationship between logic and circuits, but it doesn't explain why logic circuits should be used in computers in the first place. Part of the explanation is found in the fact that computers use binary numbers. A binary number is a string of zeros and ones. Binary numbers are easy to represent in an electronic device like a computer: Each position in the number corresponds to a wire. When the wire is on, it represents one; when the wire is off, it represents zero. When we are thinking in terms of logic, the same states of the wire represent true and false, but either representation is just an interpretation of the reality, which is a wire that is on or off. The question is whether the interpretation is fruitful.

Once wires are thought of as representing zeros and ones, we can build circuits to do computations with binary numbers. Which computations?

sion, but you can get by with ten gates in the circuit: Use a single NOT gate to compute \(\neg p\), and connect the output of that gate to two different AND gates. Reusing the output of a logic gate is an obvious way to simplify circuits that does not correspond to any operation on propositions.

| A | B | C | output |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

| A | B | C | output |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

Figure 1.8: Input/output tables for the addition of three binary digits, A, B, and C.

Any that we want! If we know what the answer should be for each combination of inputs, then by Theorem 1.3 we can build a circuit to compute that answer. Of course, the procedure described in that theorem is only practical for small circuits, but small circuits can be used as building blocks to make all the calculating circuits in a computer.

For example, let's look at binary addition. To add two ordinary, decimal numbers, you line them up one on top of the other, and add the digits in each column. In each column, there might also be a carry from the previous column. To add up a column, you only need to remember a small number of rules, such as 7 + 6 + 1 = 14 and 3 + 5 + 0 = 8. For binary addition, it's even easier, since the only digits are 0 and 1. There are only eight rules:

- 0 + 0 + 0 = 00
- 0 + 0 + 1 = 01
- 0 + 1 + 0 = 01
- 0 + 1 + 1 = 10
- 1 + 0 + 0 = 01
- 1 + 0 + 1 = 10
- 1 + 1 + 0 = 10
- 1 + 1 + 1 = 11

Here, I've written each sum using two digits. In a multi-column addition, one of these digits is carried over to the next column. Here, we have a calculation that has three inputs and two outputs. We can make an input/output table for each of the two outputs. The tables are shown in Figure 1.8. We know that these tables can be implemented as combinatorial circuits, so we know that circuits can add binary numbers. To add multi-digit binary numbers, we just need one copy of the basic addition circuit for each column in the sum.
