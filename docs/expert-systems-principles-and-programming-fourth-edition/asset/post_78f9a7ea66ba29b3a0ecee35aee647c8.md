
true, and inconsistent or unsatisfiable if the wff is false in all interpretations. An example of an inconsistent wff is p ^ ~p.

A wff is valid if it is true in all interpretations; else it is invalid. For example, the wff p v ~p is valid, while p -> q is an invalid wff since it is not true for p = T and q = F. A wff is proved if it can be shown to be valid. All propositional wffs can be proved by the truth table method since there is only a finite number of interpretations for wffs and so the propositional calculus is decidable. However, the predicate calculus is not decidable since there is no general method of proof like truth tables for all predicate calculus wffs.

One example of a valid predicate calculus wff that can be proved is that for any predicate B,

```
(∃ x) B(x) → ~ [ (∀ x) ~ B(x) ]
```

which shows how the existential quantifier can be replaced by the universal quantifier. This predicate calculus wff is therefore a theorem.

There is a big difference between an expression like ⊢ A and ⊬ B. The A is a theorem and so can be proven from the axioms by the rules of inference. The B is a wff and there may be no known proof to show its derivation. While propositional logic is decidable, predicate logic is not. That is, there is no mechanical procedure or algorithm for finding the proof of a predicate logic theorem in a finite number of steps. In fact, there is a theoretical proof that there is no decision procedure for predicate logic. However, there are decision procedures for sub-sets of predicate logic like syllogisms and propositional logic. Sometimes predicate logic is referred to as semidecidable because of this.

Note that PROLOG is based on predicate logic. In the first rush of enthusiasm toward it in the 1970s, the Japanese announced plans for their 5th Generation ultra-advanced computer system. This system would have allowed natural language input and output and really understood what was being said. However there was not enough computerized commonsense knowledge available nor were the microprocessors of the 1980s sufficiently powerful enough to allow voice recognition with a high degree of accuracy. Now with the Open.Cyc project for commonsense ontologies and good voice recognition with no training, such a system has a stronger chance of success (although not with PROLOG).

As a very simple example of a complete formal system, define the following:

- Alphabet : The single symbol "1"
- Axiom : The string "1" (which happens to be the same as the symbol 1)
- Rule of Inference : If any string $ is a theorem, then so is the string $11. This rule can be written as a Post production rule,

```
$ -> $11.
If $ = 1 then this rule gives $11 = 111.
If $ = 111 then the rule gives $11 = 11111 and in general
1, 111, 11111, 1111111, ...
```

The strings above are the theorems of this formal system.

Although strings like 11111 do not look like the types of theorems we are used to seeing, they are perfectly valid logic theorems. These particular theorems also have a semantic meaning because they are the odd numbers expressed in a **unary number system** of the single symbol 1. Just as the binary number system has only the alphabet symbols 0 and 1, the unary number system has only the single symbol 1. Numbers in the unary and decimal system are expressed as:

| Unary | Decimal |
|---|---|
| 1 | 1 |
| 11 | 2 |
| 111 | 3 |
| 1111 | 4 |
| 11111 | 5 |

and so forth.

Notice that because of our rule of inference and axiom, the strings 11, 1111, and so forth cannot be expressed in our formal system. That is, 11 and 1111 are certain strings from our formal alphabet, but they are not theorems or wffs because they cannot be proven using only the rule of inference and the axiom. This formal system allows only the derivation of the odd numbers, not the even numbers. The axiom "1" must be added in order to be able to derive the even numbers.

Another property of a formal system is **completeness**. A set of axioms is **complete** if every wff can either be proved or **refuted**. The term _refute_ means to prove some assertion is false. In a complete system, every logically valid wff is a theorem. However, since predicate logic is not decidable, coming up with a proof depends on our luck and cleverness. Of course, another possibility is writing a computer program that will try to derive proofs and let it grind away.

A further desirable property of a logical system is that it be **sound**. A sound system means that every theorem is a logically valid wff. In other words, a sound system will not allow a conclusion to be inferred that is not a logical consequence of its premises. No invalid arguments will be inferred as valid.

There are different **orders** of logic. A **first-order** language is defined so that the quantifiers operate on objects that are variables such as ∀ x. A **second-order** language would have additional features such as two kinds of variables and quantifiers. In addition to the ordering variables and quantifiers, the second-order logic can have quantifiers that range over function and predicate symbols. An example of second-order logic is the **equality axiom**, which states that two objects are equal if all predicates of them are equal. If P is any predicate of one argument, then:

```
x = y = (∀ P) [P(x) ↔ P(y) ]
```

is a statement of the equality axiom using a second-order quantifier, ∀ P, which ranges over all predicates.

## 3.10 RESOLUTION

The very powerful **resolution** rule of inference introduced by Robinson in 1965 is commonly implemented in theorem-proving AI programs. In fact, resolution is the primary rule of inference in PROLOG. Instead of many different inference rules of limited applicability such as modus ponens, modus tollens, merging, chaining, and so forth, PROLOG uses the one general-purpose inference rule of resolution. This application of resolution makes automatic theorem provers such as PROLOG practical tools for solving problems. Instead of having to try different rules of inference and hoping one succeeds, the single rule of resolution can be applied. This approach can greatly reduce the search space.

As a way of introducing resolution, let's first consider the syllogism about Socrates expressed in PROLOG as follows, where comments are shown with a percent sign:

```
mortal(X) :- man(X).      % All men are mortal
man(socrates).            % Socrates is a man
:- mortal(socrates).      % Query - is Socrates mortal?
yes                       % PROLOG answers yes
```

PROLOG uses a **quantifier-free** notation. Notice that the universal quantifier, ∀, is implied in the statement that all men are mortal.

PROLOG is based on first-order predicate logic. However it also has a number of extensions to make it easier for programming applications. These special programming features violate pure predicate logic and are called **extralogical** features: input/output, cut (which alters the search space), and assert/retract (to alter truth values without any logical justification).

Before resolution can be applied, the wff must be in a **normal** or standard form. The three main types of normal forms are **conjunctive normal form**, clausal form, and its Horn clause subset. The basic idea of normal form is to express wffs in a standard form that uses only the ∧, ∨, and possibly ~. The resolution method is then applied to normal form wffs in which all other connectives and quantifiers have been eliminated. This conversion to normal form is necessary because resolution is an operation on pairs of **disjuncts**, which produces new disjuncts, which simplifies the wff.

The following illustrates a wff in conjunctive normal form, which is defined as the conjunction of disjunctions that are **literals**:

```
(P1 v P2 v ...) ^ (Q1 v Q2 v ...) ^ ... ^ (Z1 v Z2 v ...)
```

Terms such as P1 must be literals, which mean that they contain no logical connectives such as the conditional and **biconditional**, or quantifiers. A literal is an atomic formula or a negated atomic formula. For example, the following wff:

```
(A v B) ^ (~B v C)
```
