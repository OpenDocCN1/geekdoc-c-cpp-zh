
## Mathematical Induction

Many proofs of theorems or invariants in computer science use a technique called mathematical induction, or simply **induction**. Induction is a principle of mathematics that is like a row of dominoes standing on end. If you push the first domino, all the dominoes will fall one after another. What is it about the dominoes that allows us to draw this conclusion? If you know that when one domino falls the next domino will fall, then you know that pushing the first domino will cause them all to fall in succession. More formally, you can show that all the dominoes will fall if you can show that the following two facts are true:

- The first domino falls.
- For any \( k \ge 1 \), if the \( k \)th domino falls, the \( (k + 1) \)th domino will fall.

The principle of mathematical induction is an axiom that is stated as follows:

**Axiom E-1. The principle of mathematical induction.** A property \( P(n) \) that involves an integer \( n \) is true for all \( n \ge 0 \) if the following are true:

- 1. \( P(0) \) is true.
- 2. If \( P(k) \) is true for any \( k \ge 0 \), then \( P(k + 1) \) is true.

A **proof by induction on** \( n \) is one that uses the principle of mathematical induction. Such a proof consists of the two steps given in Axiom E-1. The first step is called the **basis**, or **base case**. The second step is the **inductive step**. We usually break the induction step into two parts: the **inductive hypothesis** ("if \( P(k) \) is true for any \( k \ge 0 \)") and the **inductive conclusion** ("then \( P(k + 1) \) is true").

## Example 1

The following recursive function, which is given here in pseudocode, computes \( x^n \):

pow2(x: integer, n: integer)
if (n == 0)
return 1
else
return x * pow2(x, n-1)

You can prove that pow2 returns \( x^n \) for all \( n \ge 0 \) by using the following proof by induction on \( n \).

**Basis.** Show that the property is true when n = 0. That is, you must show that pow2(x, 0) returns x^0, which is 1. As you can see from the definition of pow2, pow2(x, 0) is 1, which establishes your basis.

Now you must establish the inductive step. By assuming that the property is true when n = k (the inductive hypothesis), you must show that the property is true when n = k + 1 (the inductive conclusion).

**Inductive Hypothesis.** Assume that the property is true when n = k. That is, assume that pow2(x, k) = x^k

**Inductive Conclusion.** Show that the property is true when n = k + 1. That is, you must show that pow2(x, k + 1) returns the value x^(k+1). By definition of the function pow2, pow2(x, k + 1) = x * pow2(x, k)

By the inductive hypothesis, pow2(x, k) returns the value x^k, so pow2(x, k + 1) = x * x^k = x^(k+1)

which is what you needed to show to establish the inductive step.

The inductive proof is thus complete. We demonstrated that the two steps in Axiom E-1 are true, so the principle of mathematical induction guarantees that pow2 returns x^n for all n >= 0. (**End of proof.**)

## Example 2

Prove that 1 + 2 + ... + n = n(n + 1) / 2 when n >= 1

It will be helpful to let Sn represent the sum 1 + 2 + ... + n.

**Basis.** Sometimes the property to be proven is trivial when n = 0, as is the case here. You can use n = 1 as the basis instead. (Actually, you can use any value of n >= 0 as the basis, but a value of 0 or 1 is typical.) You need to show that the sum S1, which is simply 1, is equal to 1(1 + 1)/2. This fact is obvious.

**Inductive Hypothesis.** Assume that the formula is true when n = k; that is, assume that Sk = k(k + 1)/2.

**Inductive Conclusion.** Show that the formula is true when n = k + 1. To do so, you can proceed as follows:

```
S_{k+1} = (1 + 2 + ... + k) + (k + 1)      (definition of S_{k+1})
        = S_k + (k + 1)                    (definition of S_k)
        = k(k + 1)/2 + (k + 1)             (inductive hypothesis)
        = (k(k + 1) + 2(k + 1))/2          (common denominator)
        = (k + 1)(k + 2)/2                 (factorization)
```

The last expression is n(n + 1)/2 when n is k + 1. Thus, if the formula for Sk is true, the formula for Sk+1 is true. Therefore, by the principle of mathematical induction, the formula is true when n >= 1. (**End of proof.**)

## Example 3

Prove that 2^n > n^2 when n >= 5.

**Basis.** Here is an example in which the base case is not n = 0 or 1, but instead n = 5. It is obvious that the relationship is true when n = 5, because

2^5 = 32 > 5^2 = 25

**Inductive Hypothesis.** Assume that the relationship is true when n = k ≥ 5—that is, assume that 2^k > k^2 when k ≥ 5.

**Inductive Conclusion.** Show that the relationship is true when n = k + 1—that is, show that 2^(k + 1) > (k + 1)^2 when k ≥ 5. To do so, you can proceed as follows:

```
(k + 1)^2 = k^2 + (2k + 1) < k^2 + k^2 when k ≥ 5 < 2^k + 2^k when k ≥ 5 = 2^(k+1)
```

Therefore, by the principle of mathematical induction, 2^n > n^2 when n ≥ 5. (End of proof.)

Sometimes, the inductive hypothesis in Axiom E-1 is not sufficient. That is, you may need to assume more than P(k). The following axiom is a stronger form of the principle of mathematical induction:

Axiom E-2. The principle of mathematical induction (strong form). A property P(n) that involves an integer n is true for all n ≥ 0 if the following are true:

- 1. P(0) is true.
- 2. If P(0), P(1), ..., P(k) are true for any k ≥ 0, then P(k + 1) is true.

Notice that the inductive hypothesis of Axiom E-2 (“If P(0), P(1), ..., P(k) are true for any k ≥ 0”) includes the inductive hypothesis of Axiom E-1 (“If P(k) is true for any k ≥ 0”).

## Example 4

Prove that every integer greater than 1 can be written as a product of prime integers.

Recall that a prime number is one that is divisible only by 1 and itself. The inductive proof is as follows:

Basis. The statement that you must prove involves integers greater than 1. Thus, the base case is n = 2. However, 2 is a prime number, and therefore it trivially is a product of prime numbers.

Inductive Hypothesis. Assume that the property is true for each of the integers 2, 3, ..., k, where k ≥ 2.

Inductive Conclusion. Show that the property is true when n = k + 1; that is, show that k + 1 can be written as a product of prime numbers.

If k + 1 is a prime number, then there is nothing more to show. However, if k + 1 is not a prime number, it must be divisible by an integer x such that 1 < x < k + 1. Thus,

```
k + 1 = x y
```

where 1 < y < k + 1. Notice that x and y are each less than or equal to k, so the inductive hypothesis applies. That is, x and y can each be written as a product of prime numbers. Clearly, the product x × y, which is equal to k + 1, must be a product of prime numbers. Because the formula holds for n = k + 1, it holds for all n ≥ 2 by the principle of mathematical induction. (End of proof.)

## Example 5

Chapter 2 discusses the following recursive definition:

```
rabbit(1) = 1
rabbit(2) = 2
rabbit(n) = rabbit(n - 1) + rabbit(n - 2) when n > 2
```

Prove that

```
rabbit(n) = (a^n - b^n)/\sqrt{5}
```

where \(a = (1 + \sqrt{5})/2\) and \(b = (1 - \sqrt{5})/2 = 1 - a\).

**Basis.** Because \(rabbit(0)\) is undefined, begin at \(n = 1\). Some algebra shows that \(rabbit(1) = (a^1 - b^1)/\sqrt{5} = 1\). However, notice that \(rabbit(2)\) is also a special case. That is, you cannot compute \(rabbit(2)\) from \(rabbit(1)\) by using the recurrence relationship given here. Therefore, the basis in this inductive proof must include \(n = 2\).

When \(n = 2\), some more algebra will show that \(rabbit(2) = (a^2 - b^2)/\sqrt{5} = 1\). Thus, the formula is true when \(n\) is either 1 or 2.

**Inductive Hypothesis.** Assume that the formula is true for all \(n\) such that \(1 \le n \le k\), where \(k\) is at least 2.

**Inductive Conclusion.** Show that the formula is true for \(n = k + 1\). To do so, you can proceed as follows:

```
rabbit(k + 1) = rabbit(k) + rabbit(k - 1) (recurrence relation)
= [(a^k - b^k) + (a^(k-1) - b^(k-1))]/\sqrt{5} (inductive hypothesis)
= [a^(k-1)(a + 1) - b^(k-1)(b + 1)]/\sqrt{5} (factorization)
= [(a^(k-1)(a^2) - b^(k-1)(b^2)]/\sqrt{5} (a + 1 = a^2; b + 1 = b^2)
= (a^(k+1) - b^(k+1))/\sqrt{5}
```

Because the formula holds for \(n = k + 1\), it holds for all \(n > 2\) by the principle of mathematical induction. (**End of proof.**)

**Note.** That the previous proof requires that you show that \(a + 1 = a^2\) and \(b + 1 = b^2\). Although simple algebra will demonstrate the validity of these equalities, exactly how did we discover them after the factorization step? Some experience with inductive proofs will give you the confidence to determine and verify the auxiliary relationships—such as \(a + 1 = a^2\)—that are necessary in a proof. Here, after we introduced the factors \((a + 1)\) and \((b + 1)\), we observed that if these factors were equal to \(a^2\) and \(b^2\), respectively, we could finish the proof. Thus, we tried to show that \(a + 1 = a^2\) and \(b + 1 = b^2\); indeed, we were successful. Inductive proofs often require adventurous algebraic manipulations!
