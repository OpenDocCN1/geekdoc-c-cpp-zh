# 3.10 RESOLUTION

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