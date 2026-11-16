it should not be a surprise that many of the rules of logic have analogs in set theory.

For example, we have already noted that \(\cup\) and \(\cap\) are commutative operations. This fact can be verified using the rules of logic. Let \(A\) and \(B\) be sets. According to the definition of equality of sets, we can show that \(A \cup B = B \cup A\) by showing that \(\forall x((x \in A \cup B) \leftrightarrow (x \in B \cup A))\). But for any \(x\),

```
x \in A \cup B \leftrightarrow x \in A \lor x \in B   (definition of \cup)
\leftrightarrow x \in B \lor x \in A   (commutativity of \lor)
\leftrightarrow x \in B \cup A   (definition of \cup)
```

The commutativity of \(\cap\) follows in the same way from the definition of \(\cap\) in terms of \(\land\), and a similar argument shows that union and intersection are associative operations.

The distributive laws for propositional logic give rise to two similar rules in set theory. Let \(A, B,\) and \(C\) be any sets. Then

```
A \cup (B \cap C) = (A \cup B) \cap (A \cup C)
```

and

```
A \cap (B \cup C) = (A \cap B) \cup (A \cap C)
```

These rules are called the distributive laws for set theory. To verify the first of these laws, we just have to note that for any \(x\),

```
x \in A \cup (B \cap C)
\leftrightarrow (x \in A) \lor ((x \in B) \land (x \in C))   (definition of \cup, \cap)
\leftrightarrow ((x \in A) \lor (x \in B)) \land ((x \in A) \lor (x \in C))   (distributivity of \lor)
\leftrightarrow (x \in A \cup B) \land (x \in A \cup C)   (definition of \cup)
\leftrightarrow x \in ((A \cup B) \cap (A \cup C))   (definition of \cap)
```

The second distributive law for sets follows in exactly the same way.

While \(\cup\) is analogous to \(\lor\) and \(\cap\) is analogous to \(\land\), we have not yet seen any operation in set theory that is analogous to the logical “not” operator, \(\neg\).

Given a set \(A\), it is tempting to try to define \(\{x | \neg(x \in A)\}\), the set that contains everything that does not belong to \(A\). Unfortunately, the rules of set theory do not allow us to define such a set. The notation \(\{x | P(x)\}\) can only be used when the domain of discourse of \(P\) is a set, so there