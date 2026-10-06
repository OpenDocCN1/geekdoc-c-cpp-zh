Limits of Computation

# 9.2.1 Restriction (Also Called Generalization)

X is a special case of Y, and so very every yes or no instance of X is already a yes or no instance of Y. No modifications are necessary. Thus, an identity mapping takes a instance of X to a instance of Y, and takes a no instance of X to a no instance of Y.

We have seen examples of generalization earlier: every third degree polynomial is also a fourth degree polynomial (though not versa). So, if we took X to the language p(x): p is a polynomial of degree $\le$ 3 with an integer root for some integer n, and Y is the generalization of X to include fourth degree polynomials, then a yes or no instance of X is, without modification, or a no instance of Y.

$X = \{p(x): p \text{ is polynomial, degree } \le 3, p(n) = 0 \text{ for some n }}\nX = \{x^3 + 8, x - 5, x^2 - x - 6, \dots \} \text{(yes instances)}$

$\overline{X} = \{x^2 + 1, x^4 - 16, \dots \} \text{\ (no instances)}$

$Y = \{p(x): p \text{ is polynomial, degree } \le 4, p(n) = 0 \text{ for some n }}\nY = \{x^3 + 8, x - 5, x^2 - x - 6, x^4 - 16 \ \dots \} \text{\ (yes instances)}$

$Y = \{x^2 + 1, \dots \} \text{\ (no instances)}$

Boolean expressions in conjunctive normal form are certainly Boolean expressions, so CNF Boolean expressions are special cases of general Boolean expressions, and GEN-SAT is a generalization of CNF-SAT.

# Theorem 9.1

GEN-SAT (or general first-order Boolean expression satisfiability) is NP-complete.

# Proof

An instance of GEN-SAT is a Boolean expression in variables $x_i, \dots, x_n$, using all the standard connectors $(\neg, \wedge, \vee, \to, =)$, not in any particular form. Again, the certificate is an assignment of truth values to the $x_i, \dots, x_n$ variables, and therefore it is easy to show (so do it!) that this certificate