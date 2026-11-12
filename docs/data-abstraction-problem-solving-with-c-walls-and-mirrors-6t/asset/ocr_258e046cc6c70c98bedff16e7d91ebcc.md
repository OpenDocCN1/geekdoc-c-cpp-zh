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

**Note.** that the previous proof requires that you show that \(a + 1 = a^2\) and \(b + 1 = b^2\). Although simple algebra will demonstrate the validity of these equalities, exactly how did we discover them after the factorization step? Some experience with inductive proofs will give you the confidence to determine and verify the auxiliary relationships—such as \(a + 1 = a^2\)—that are necessary in a proof. Here, after we introduced the factors \((a + 1)\) and \((b + 1)\), we observed that if these factors were equal to \(a^2\) and \(b^2\), respectively, we could finish the proof. Thus, we tried to show that \(a + 1 = a^2\) and \(b + 1 = b^2\); indeed, we were successful. Inductive proofs often require adventurous algebraic manipulations!