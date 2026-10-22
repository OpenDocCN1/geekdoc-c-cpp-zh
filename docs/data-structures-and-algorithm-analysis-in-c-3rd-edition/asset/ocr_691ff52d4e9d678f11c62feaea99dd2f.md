problem F can be recast as some language acceptance problem L:

F(I) = YES ⇔ L(I') = ACCEPT.

That is, if a decision problem F yields YES on input I, then there is a language L containing string I' where I' is some suitable transformation of input I. Conversely, if F would give answer NO for input I, then I's transformed version I' is not in the language L.

Turing machines are a simple model of computation for writing programs that are language acceptors. There is a “universal” Turing machine that can take as input a description for a Turing machine, and an input string, and return the execution of that machine on that string. This Turing machine in turn can be cast as a Boolean expression such that the expression is satisfiable if and only if the Turing machine yields ACCEPT for that string. Cook used Turing machines in his proof because they are simple enough that he could develop this transformation of Turing machines to Boolean expressions, but rich enough to be able to compute any function that a regular computer can compute. The significance of this transformation is that any decision problem that is performable by the Turing machine is transformable to SAT. Thus, SAT is NP-hard.

As explained above, to show that a decision problem X is NP-complete, we prove that X is in NP (normally easy, and normally done by giving a suitable polynomial-time, nondeterministic algorithm) and then prove that X is NP-hard. To prove that X is NP-hard, we choose a known NP-complete problem, say A. We describe a polynomial-time transformation that takes an arbitrary instance I of A to an instance I' of X. We then describe a polynomial-time transformation from SLN' to SLN such that SLN is the solution for I. The following example provides a model for how an NP-completeness proof is done.

3-SATISFIABILITY (3 SAT)
Input: A Boolean expression E in CNF such that each clause contains exactly 3 literals.
Output: YES if the expression can be satisfied, NO otherwise.

# Example 17.1 3 SAT is a special case of SAT. Is 3 SAT easier than SAT? Not if we can prove it to be NP-complete.

# Theorem 17.1 3 SAT is NP-complete.

Proof: Prove that 3 SAT is in NP: Guess (nondeterministically) truth values for the variables. The correctness of the guess can be verified in polynomial time.
Prove that 3 SAT is NP-hard: We need a polynomial-time reduction from SAT to 3 SAT. Let E = C1 · C2 · ... · Ck be any instance of SAT. Our