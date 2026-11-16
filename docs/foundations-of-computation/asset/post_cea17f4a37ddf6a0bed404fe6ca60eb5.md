
## 1.2. BOOLEAN ALGEBRA

joker or a diamond.” That is, \( j \lor (t \land d) \equiv (j \lor t) \land (j \lor d) \). The distributive laws are powerful tools and you should keep them in mind whenever you are faced with a mixture of \(\land\) and \(\lor\) operators.

DeMorgan's Laws must also be less than obvious, since people often get them wrong. But they do make sense. When considering \((\neg p \land q)\), you should ask yourself, how can “\(p\) and \(q\)” fail to be true. It will fail to be true if either \(p\) is false or \(q\) is false (or both). That is, \(\neg(p \land q)\) is equivalent to \((\neg p) \lor (\neg q)\). Consider the sentence “A raven is large and black.” If a bird is *not* large and black, then it is not a raven. But what exactly does it mean to be “_not_ (large and black)”? How can you tell whether the assertion “not (large and black)” is true of something? This will be true if it is either not large or not black. (It doesn’t have to be both—it could be large and white, it could be small and black.). Similarly, for “\(p\) or \(q\)” to fail to be true, both \(p\) and \(q\) must be false. That is, \(\neg(p \lor q)\) is equivalent to \((\neg p) \land (\neg q)\). This is DeMorgan's second law.

Recalling that \(p \to q\) is equivalent to \((\neg p) \lor q\), we can apply DeMorgan's law to obtain a formula for the negation of an implication.

\(\neg(p \to q) \equiv \neg((\neg p) \lor q)\)
\(\equiv \neg(\neg p) \land (\neg q)\)
\(\equiv p \land \neg q\)

That is, \(p \to q\) is false exactly when both \(p\) is true and \(q\) is false. For example, the negation of “If you have an ace, you win” is “You have an ace, and you did not win.” Think of it this way: if you had an ace and you didn’t win, then the statement “If you have an ace, you win” was not true.

## Exercises

- 1. Construct truth tables to demonstrate the validity of each of the distributive laws.

- 2. Construct the following truth tables:

  - a) Construct truth tables to demonstrate that \(\neg(p \land q)\) is **not** logically equivalent to \((\neg p) \land (\neg q)\).

  - b) Construct truth tables to demonstrate that \(\neg(p \lor q)\) is **not** logically equivalent to \((\neg p) \lor (\neg q)\).

  - c) Construct truth tables to demonstrate the validity of both DeMorgan's Laws.

- 3. Construct truth tables to demonstrate that \(\neg(p \to q)\) is **not** logically equivalent to any of the following.

  - a) \((\neg p) \to (\neg q)\)
  - b) \((\neg p) \to q\)
  - c) \(p \to (\neg q)\)

Refer back to this section for a formula that is logically equivalent to \(\neg(p \to q)\).

- 4. Is \(\neg(p \to q)\) logically equivalent to \((\neg p) \to (\neg q)\)?

- 5. In the algebra of numbers, there is a distributive law of multiplication over addition: \(x(y+z) = xy + xz\). What would a distributive law of addition over multiplication look like? Is it a valid law in the algebra of numbers?

- 6. The distributive laws given in Figure 1.2 are sometimes called the left distributive laws. The **right distributive laws** say that \((p \lor q) \land r \equiv (p \land r) \lor (q \land r)\) and that \((p \land q) \lor r \equiv (p \lor r) \land (q \lor r)\). Show that the right distributive laws are also valid laws of Boolean algebra. (Note: In practice, both the left and the right distributive laws are referred to simply as the distributive laws, and both can be used freely in proofs.)

- 7. Show that \(p \land (q \lor r \lor s) \equiv (p \land q) \lor (p \land r) \lor (p \land s)\) for any propositions \(p, q, r,\) and \(s\). In words, we can say that conjunction distributes over a disjunction of three terms. (Recall that the \(\land\) operator is called conjunction and \(\lor\) is called disjunction.) Translate into logic and verify the fact that conjunction distributes over a disjunction of four terms. Argue that, in fact, conjunction distributes over a disjunction of any number of terms.

- 8. There are two additional basic laws of logic, involving the two expression \(p \mathbb{F}\) and \(p \mathbb{V}\). What are the missing laws? Show that your answers are, in fact, laws.

- 9. For each of the following pairs of propositions, show that the two propositions are logically equivalent by finding a chain of equivalences from one to the other. State which definition or law of logic justifies each equivalence in the chain.

  - a) \(p \land (q \land p)\). \(p \land q\)
  - b) \((p \to q) \to (p \lor q)\)
  - c) \((p \lor q) \land \neg q\). \(p \land \neg q\)
  - d) \(\neg p \to q\). \(p \lor q\)
  - e) \((p \to r) \land (q \to r)\). \((p \lor q) \to r\)
  - f) \(p \to (p \land q)\). \(p \to q\)

- 10. For each of the following compound propositions, find a simpler proposition that is logically equivalent. Try to find a proposition that is as simple as possible.

  - a) \((p \land q) \lor \neg q\)
  - b) \(\neg(p \lor q) \land p\)
  - c) \(p \lor \neg(p \land q)\)
  - d) \(\neg(p \land \neg q)\)
  - e) \((p \land q) \to q\)
  - f) \((p \to q) \land (\neg p \to q)\)

- 11. Express the negation of each of the following sentences in natural English:

  - a) It is sunny and cold.
  - b) I will have cake or I will have pie.
  - c) If today is Tuesday, this is Belgium.
  - d) If you pass the final exam, you pass the course.

- 12. Apply one of the laws of logic to each of the following sentences, and rewrite it as an equivalent sentence. State which law you are applying.

  - a) I will have coffee and cake or pie.
  - b) He has neither talent nor ambition.
  - c) You can have spam, or you can have spam.

## 1.3 Application: Logic Circuits

Computers have a reputation—not always deserved—for being “logical.” But fundamentally, deep down, they are made of logic in a very real sense. The building blocks of computers are *logic gates*, which are electronic components that compute the values of simple propositions such as \(p \lor q\) and \(\neg p\). (Each gate is in turn built of even smaller electronic components called transistors, but this needn’t concern us here.)

A wire in a computer can be in one of two states, which we can think of as being *on* and *off*. These two states can be naturally associated with the Boolean values \(\mathbb{T}\) and \(\mathbb{F}\). When a computer computes, the multitude of wires inside it are turned on and off in patterns that are determined by certain rules. The rules involved can be most naturally expressed in terms of logic. A simple rule might be, “turn wire C on whenever wire A is on and wire B is on.” This rule can be implemented in hardware as an **AND** gate. An AND gate is an electronic component with two input wires and one output wire, whose job is to turn its output on when both of its inputs are on and to turn its output off in any other case. If we associate “on” with \(\mathbb{T}\) and “off” with \(\mathbb{F}\), and if we give the names \(A\) and \(B\) to the inputs of the gate, then the gate computes the value of the logical expression \(A \land B\). In effect, \(A\) is a proposition with the meaning “the first input is on,” and \(B\) is a proposition with the meaning “the second input is on.” The AND gate functions to ensure that the output is described by the proposition \(A \land B\). That is, the output is on if and only if the first input is on and the second input is on.

An **OR gate** is an electronic component with two inputs and one output which turns its output on if either (or both) of its inputs is on. If the inputs are given names \(A\) and \(B\), then the OR gate computes the logical value of \(A \lor B\). A **NOT gate** has one input and one output, and it turns its output off when the input is on and on when the input is off. If the input is named \(A\), then the NOT gate computes the value of \(\neg A\).

Other types of logic gates are, of course, possible. Gates could be made to compute \(A \rightarrow B\) or \(A \oplus B\), for example. However, any computation that can be performed by logic gates can be done using only AND, OR, and NOT gates, as we will see below. (In practice, however, NAND gates and NOR gates, which compute the values of \(\neg(A \land B)\) and \(\neg(A \lor B)\) respectively,
