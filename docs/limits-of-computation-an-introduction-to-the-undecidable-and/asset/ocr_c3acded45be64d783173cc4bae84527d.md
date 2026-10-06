# Definition 8.1

The class **P** is the set of all decision problems that have polynomial solutions (that is, they are in $O(p(n))$ for some polynomial p in the size of the input).

In contrast, **NP** will consist of problems that are not easy to solve (though no one has been able to prove this!), but have solutions that are easy to check.

There are two standard ways to define the class **NP**. Nothing mathematical should have two definitions, but these two definitions are equivalent. So, we will give both, and immediately show that they are equivalent. Sometimes it will be easier to use one definition than the other, so it will be useful to have both available.

Note that a instance of a decision problem can have a **certificate**. A certificate is showing that how the decision problem is satisfied, that is, what proves that it is a yes instance. For example, it is always possible to think of some kind of certificate for a problem. An actual solution is always a certificate. And, for many problems, there are short certificates—certificates that are shorter than the actual solutions.

COMPOSITE = {n | n is a positive integer and n is not prime}.

Certificate: A pair of numbers 1 $x,y < n$ such that $xy = n$.

Verifier: Multiply x*y, check that the product is n.

PRIME = {n | n is positive integer} has no obvious short certificate.

Certificate: Listing of all primes p from 2 to n/2, with their nonzero remainders (mod $p 
eq 0$).

Verifier: Check these approximately n/4 divisions (or see Pratt, 1975) for a polynomial certificate and verifier.

TAUTOLOGY = {Boolean expressions that are true for all truth assignments).

Certificate: No known short certificate, but certainly the complete truth table would work as a certificate; verify that each row evaluates to.

Verifier: Calculate truth table, check that each row evaluates to.