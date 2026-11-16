It is left as an exercise to prove the following theorem concerning logical equivalence of quantified expressions.

**Theorem 3.1** The following logical equivalences hold. (_A_ and _B_ are variables denoting arbitrary predicates. Furthermore, they could have other arguments besides _x_.):

+   1. \(\neg \exists x A(x) \equiv \forall x \neg A(x)\)
+   
+   2. \(\neg \forall x A(x) \equiv \exists x \neg A(x)\)
+   
+   3. \(\exists x (A(x) \lor B(x)) \equiv \exists x A(x) \lor \exists x B(x)\)
+   
+   4. \(\forall x (A(x) \land B(x)) \equiv \forall x A(x) \land \forall x B(x)\)
+   
+   5. \(\forall x A(x) \equiv \forall y A(y)\)
+   
+   6. \(\exists x A(x) \equiv \exists y A(y)\)

Equivalences 1 and 2 are **DeMorgan's laws** for quantifiers. Intuitively, Equivalence 1 holds because if _A_(_x_) is false for every _x_ then it cannot be true for any _x_. The other equivalences can readily be made clear with similar intuitive explanations.

# ## 3.1.4 Derivation Systems

Similar to propositional logic, in first-order logic an **argument** consists of a set of formulas, called the **premises**, and a formula called the **conclusion**. We say that the premises **entail** the conclusion if in every model in which all the premises are true, the conclusion is also true. If the premises entail the conclusion, we say the argument is **sound**; otherwise we say it is a **fallacy**. A set of inference rules is called a **deduction system**. A deduction system is **sound** if it only derives sound arguments. A deduction system is **complete** if it can derive every sound argument. Gödel's famous first incompleteness theorem proves that in general there is no complete deduction system in first-order logic. However, its discussion is beyond the scope of this text. Briefly, Gödel showed that there are statements about the natural numbers that cannot be proved.

We write arguments showing the list of premises followed by the conclusion as follows:

+   1. \(A_1\)
+   
+   2. \(A_2\)
+   
+   \(\vdots\)
+   
+   \(n. \underline{A_n}\)
+   
+   \(B\)