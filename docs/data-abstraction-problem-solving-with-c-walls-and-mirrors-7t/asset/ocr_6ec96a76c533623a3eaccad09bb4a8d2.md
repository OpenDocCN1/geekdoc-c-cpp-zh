**Inductive Hypothesis.** Assume that the relationship is true when \( n = k \ge 5 \)—that is, assume that \( 2^k > k^2 \) when \( k \ge 5 \).

**Inductive Conclusion.** Show that the relationship is true when \( n = k + 1 \)—that is, show that \( 2^{k+1} > (k + 1)^2 \) when \( k \ge 5 \). To do so, you can proceed as follows:

```
\( (k + 1)^2 = k^2 + (2k + 1) \) (square \( k + 1 \))
\( < k^2 + k^2 \) when \( k \ge 5 \) (\( 2k + 1 < k^2 \))
\( < 2^k + 2^k \) when \( k \ge 5 \) (inductive hypothesis)
\( = 2^{k+1} \)
```

Therefore, by the principle of mathematical induction, \( 2^n > n^2 \) when \( n \ge 5 \). (**End of proof.**)

Sometimes, the inductive hypothesis in Axiom E-1 is not sufficient. That is, you may need to assume more than \( P(k) \). The following axiom is a stronger form of the principle of mathematical induction:

# **Axiom E-2. The principle of mathematical induction (strong form).** A property \( P(n) \) that involves an integer \( n \) is true for all \( n \ge 0 \) if the following are true:

+   1. \( P(0) \) is true.
+   2. If \( P(0), P(1), \dots, P(k) \) are true for any \( k \ge 0 \), then \( P(k + 1) \) is true.

Notice that the inductive hypothesis of Axiom E-2 ("If \( P(0), P(1), \dots, P(k) \) are true for any \( k \ge 0 \)") includes the inductive hypothesis of Axiom E-1 ("If \( P(k) \) is true for any \( k \ge 0 \)").

# Example 4

Prove that every integer greater than 1 can be written as a product of prime integers.

Recall that a prime number is one that is divisible only by 1 and itself. The inductive proof is as follows:

**Basis.** The statement that you must prove involves integers greater than 1. Thus, the base case is \( n = 2 \). However, 2 is a prime number, and therefore it trivially is a product of prime numbers.

**Inductive Hypothesis.** Assume that the property is true for each of the integers \( 2, 3, \dots, k \), where \( k \ge 2 \).

**Inductive Conclusion.** Show that the property is true when \( n = k + 1 \); that is, show that \( k + 1 \) can be written as a product of prime numbers.

If \( k + 1 \) is a prime number, then there is nothing more to show. However, if \( k + 1 \) is not a prime number, it must be divisible by an integer \( x \) such that \( 1 < x < k + 1 \). Thus,

```
\( k + 1 = x \times y \)
```

where \( 1 < y < k + 1 \). Notice that \( x \) and \( y \) are each less than or equal to \( k \), so the inductive hypothesis applies. That is, \( x \) and \( y \) can each be written as a product of prime numbers. Clearly, the product \( x \times y \), which is equal to \( k + 1 \), must be a product of prime numbers. Because the formula holds for \( n = k + 1 \), it holds for all \( n \ge 2 \) by the principle of mathematical induction. (**End of proof.**)

# Example 5

Chapter 2 discusses the following recursive definition:

```
rabbit(1) = 1
rabbit(2) = 2
rabbit(n) = rabbit(n - 1) + rabbit(n - 2) when n > 2
```