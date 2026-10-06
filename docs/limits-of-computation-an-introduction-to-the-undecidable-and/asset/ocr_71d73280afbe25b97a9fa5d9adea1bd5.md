# 136 Limits of Computation

In a case, M’ now—for the first time—looks at its input x’ and accepts if x’ is of some form. It might just accept x’ no matter what it is—in this case, L(M’) = Σ*.

In case b, M’ usually goes to its reject state; so L(M’) = ∅.

In case c

# Theorem 7.7

Given a Turing machine, it is undecidable whether the Turing accepts the empty string Ε.

# Proof

This follows the classic pattern. Start with a Turing machine M and its input w. We, want to build a new M’ so that

+   - M accepts ⇒ M’ accepts Ε (and maybe other strings too).
- M does not accept w ⇒ M’ does not accept Ε.

To do this, we build an M’ that has M and built into it.
Action of M’ on its input x:

+   - Ignore x while M’ runs M on w.
If M accepts, M’ enters its own accept state q_{M’-accept} (so accepts x).
If M rejects, M’ rejects its input, entering its reject state.

(Should M be looping on w, we do not have to state what to do. M’ will wait for M to finish on w, and that will never occur. So M’ is simply waiting, waiting, waiting…).

Now the language of M’ depends on what M does on w:

+   - M accepts w ⇒ L(M’) = Σ* ⇒ M accepts Ε.
- M does not accept w ⇒ L(M’) = ∅ ⇒ M’ does not accept Ε.