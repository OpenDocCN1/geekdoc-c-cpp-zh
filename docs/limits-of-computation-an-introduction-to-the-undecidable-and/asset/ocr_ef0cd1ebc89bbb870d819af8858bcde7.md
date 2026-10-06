164 ■ Limits of Computation

If the length of the encoding of X is n, and the length of the certificate C is m, then there is a polynomial p' such that the deterministic Turing machine (DTM) $M_d$ runs in steps bounded by p'(n).

**Note:** The length of the certificate m is not mentioned in the definition, but it must be bounded by a polynomial in n; otherwise, the DTM could not read the entire certificate in p'(n).

**Note:** The initials N and P *do stand* for nonpolynomial! That is a common misconception, but incorrect for several reasons: (1) it has not been proved that there are no polynomial algorithms for the problems in NP, (2) $P \subseteq NP$, some problems in NP (those in P) do have polynomial solvers, and (3) many nonpolynomial problems are not in NP (for example, the undec problems). Instead, NP stands for nondeterministic polynomial.

# Theorem 8.4

The two definitions above (Definitions 8.2 and 8.3) are equivalent.

We need to show that an NDTM solver exists if and only if (iff) a polynomial verifier exists.

**Direction 1:** Assume the first definition is satisfied—the problem has an NDTM, and a yes instance has a path to the accept state bounded by p(n).

The certificate here is the path to the accept state. Remember that a certificate can be anything that proves this is a yes instance—so showing how to accept will do that. To verify the certificate, just follow its path and see that one has reached accept. The path is bounded by a polynomial—this takes the same polynomial number of steps.

**Direction 2:** Assume the second definition is satisfied, that is, a yes instance of the problem has a certificate with a polynomial verifier with bound p'(n). Now show that a polynomial-bounded NDTM exists.

We construct a two-phase machine. The first phase will be to guess the certificate. This can be done by looking at the form of the certificate. At each step of the first phase (1, 2, ..., p'(n)), the choices of the NDTM are: (1) write down one possibility for this step, or (2) stop writing the certificate and proceed to the second phase. Once the bound is reached, the NDTM must stop the certificate.

The second phase of the NDTM is simply to run the deterministic polynomial verifier on the guessed certificate.