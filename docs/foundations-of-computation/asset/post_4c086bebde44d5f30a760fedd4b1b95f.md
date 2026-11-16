
## 1.6. PROOF

And one more example: we will prove that any 4-digit number $d_1d_2d_3d_4$ is divisible by 3 iff the sum of the four digits is divisible by 3.

Proof. This statement is of the form $p \leftrightarrow q$; recall that $p \leftrightarrow q$ is logically equivalent to $(p \to q) \wedge (q \to p)$. So we need to prove for any 4-digit number is $d_1d_2d_3d_4$ that (1) if $d_1d_2d_3d_4$ is divisible by 3 then $d_1+d_2+d_3+d_4$ is divisible by 3, and (2) if $d_1+d_2+d_3+d_4$ is divisible by 3 then $d_1d_2d_3d_4$ is divisible by 3. So let $d_1d_2d_3d_4$ be an arbitrary 4-digit number.

- (1) Assume $d_1d_2d_3d_4$ is divisible by 3, i.e. $d_1d_2d_3d_4 = 3k$ for some integer $k$. The number $d_1d_2d_3d_4$ is actually $d_1 \times 1000 + d_2 \times 100 + d_3 \times 10 + d_4$, so we have the equation

$$
d_1 \times 1000 + d_2 \times 100 + d_3 \times 10 + d_4 = 3k.
$$

Since $1000 = 999 + 1$, $100 = 99 + 1$, and $10 = 9 + 1$, this equation can be rewritten

$$
999d_1 + d_1 + 99d_2 + d_2 + 9d_3 + d_3 + d_4 = 3k.
$$

Rearranging gives

$$
d_1 + d_2 + d_3 + d_4 = 3k - 999d_1 - 99d_2 - 9d_3
= 3k - 3(333d_1) - 3(33d_2) - 3(3d_3).
$$

We can now factor a 3 from the right side to get

$$
d_1 + d_2 + d_3 + d_4 = 3(k - 333d_1 - 33d_2 - d_3).
$$

Since $(k - 333d_1 - 33d_2 - d_3)$ is an integer, we have shown that $d_1+d_2+d_3+d_4$ is divisible by 3.

- (2) Assume $d_1 + d_2 + d_3 + d_4$ is divisible by 3. Consider the number $d_1d_2d_3d_4$. As remarked above,

$$
d_1d_2d_3d_4 = d_1 \times 1000 + d_2 \times 100 + d_3 \times 10 + d_4
$$

so

$$
d_1d_2d_3d_4 = 999d_1 + d_1 + 99d_2 + d_2 + 9d_3 + d_3 + d_4
= 999d_1 + 99d_2 + 9d_3 + (d_1 + d_2 + d_3 + d_4).
$$

We assumed that $d_1 + d_2 + d_3 + d_4 = 3k$ for some integer $k$, so we can substitute into the last equation to get

$$
d_1d_2d_3d_4 = 999d_1 + 99d_2 + 9d_3 + 3k = 3(333d_1 + 33d_2 + 3d_3 + k).
$$

Since the quantity in parentheses is an integer, we have proved that \(d_1 d_2 d_3 d_4\) is divisible by 3.

In (1) and (2) above, the number \(d_1 d_2 d_3 d_4\) was an arbitrary 4-digit integer, so we have proved that for all 4-digit integers, \(d_1 d_2 d_3 d_4\) is divisible by 3 iff the sum of the four digits is divisible by 3. \(\blacksquare\)

Now suppose we wanted to prove the statement “For all integers \(n\), \(n^2\) is even if and only if \(n\) is even.” We have already proved half of this statement (“For all integers \(n\), if \(n\) is even then \(n^2\) is even”), so all we need to do is prove the statement “For all integers \(n\), if \(n^2\) is even then \(n\) is even” and we’ll be done. Unfortunately, this is not as straightforward as it seems: suppose we started in our standard manner and let \(n\) be an arbitrary integer and assumed that $n^2 = 2k$ for some integer $k$. Then we’d be stuck! Taking the square root of both sides would give us $n$ on the left but would leave $n$ a $\sqrt{2k}$ on the right. This quantity is not of the form $2k'$ for any integer $k'$; multiplying it by $\frac{\sqrt{2}}{\sqrt{2}}$ would give $2\sqrt{\frac{k}{2}}$ but there is no way for us to prove that $\frac{\sqrt{k}}{2}$ is an integer. So we’ve hit a dead end. What do we do now?

The answer is that we need a different proof technique. The proofs you have seen so far are what are called **direct proofs**: to prove $p \rightarrow q$ you assume $p$ is true and prove that the truth of $q$ follows. Sometimes, when a direct proof of $p \rightarrow q$ fails, an **indirect proof** will work. Recall that the *contrapositive* of the implication $p \rightarrow q$ is the implication $\neg q \rightarrow \neg p$, and that this proposition is logically equivalent to $p \rightarrow q$. An indirect proof of $p \rightarrow q$, then, is a direct proof of the contrapositive $\neg q \rightarrow \neg p$. In our current example, instead of proving “if $n^2$ is even then $n$ is even” directly, we can prove its contrapositive “if $n$ is not even (i.e. $n$ is odd) then $n^2$ is not even (i.e. $n^2$ is odd).” The proof of this contrapositive is a routine direct argument which we leave to the exercises.

## Exercises

- 1. Find a natural number \(n\) for which \(n^2 + n + 41\) is not prime.

- 2. Show that the propositions \(p \lor q\) and \((\neg p) \rightarrow q\) are logically equivalent.

- 3. Show that the proposition \((p \lor q) \rightarrow r\) is equivalent to \((p \rightarrow r) \land (q \rightarrow r)\).

- 4. Determine whether each of the following statements is true. If it is true, prove it. If it is false, give a counterexample.

- a) Every prime number is odd.

- b) Every prime number greater than 2 is odd.

- c) If x and y are integers with x < y, then there is an integer z such that x < z < y.

- d) If x and y are real numbers with x < y, then there is a real number z such that x < z < y.

- 5. Suppose that r, s, and t are integers, such that r evenly divides s and s evenly divides t. Prove that r evenly divides t.

- 6. Prove that for all integers n, if n is odd then n^2 is odd.

- 7. Prove that an integer n is divisible by 3 iff n^2 is divisible by 3. (Hint: give an indirect proof of “if n^2 is divisible by 3 then n is divisible by 3.”)

- 8. Prove or disprove each of the following statements.

- a) The product of two even integers is even.
- b) The product of two integers is even only if both integers are even.
- c) The product of two rational numbers is rational.
- d) The product of two irrational numbers is irrational.
- e) For all integers n, if n is divisible by 4 then n^2 is divisible by 4.
- f) For all integers n, if n^2 is divisible by 4 then n is divisible by 4.

## 1.7 Proof by Contradiction

Suppose that we start with some set of assumptions and apply rules of logic to derive a sequence of statements that can be proved from those assumptions, and suppose that we derive a statement that we know to be false. When the laws of logic are applied to true statements, the statements that are derived will also be true. If we derive a false statement by applying rules of logic to a set of assumptions, then at least one of the assumptions must be false. This observation leads to a powerful proof technique, which is known as proof by contradiction.

Suppose that you want to prove some proposition, p. To apply proof by contradiction, assume that ¬p is true, and apply the rules of logic to derive conclusions based on this assumption. If it is possible to derive a statement that is known to be false, it follows that the assumption, ¬p, must be false. (Of course, if the derivation is based on several assumptions, then you only know that at least one of the assumptions must be false.) The fact that ¬p is false proves that p is true. Essentially, you are arguing that p must be true, because if it weren’t, then some statement that is known to be false could be proved to be true. Generally, the false statement that is derived in a proof by contradiction is of the form q ∧ ¬q. This statement is a contradiction in the sense that it is false no matter what the value of q. Note that deriving the contradiction q ∧ ¬q is the same as showing that the two statements, q and ¬q, both follow from the assumption that ¬p.

As a first example of proof by contradiction, consider the following theorem:

### Theorem 1.4. The number \(\sqrt{3}\) is irrational.

Proof. Assume for the sake of contradiction that \(\sqrt{3}\) is rational. Then \(\sqrt{3}\) can be written as the ratio of two integers, \(\sqrt{3} = \frac{m}{n}\) for some integers \(m'\) and \(n'\). Furthermore, the fraction \(\frac{m'}{n'}\) can be reduced to lowest terms by canceling all common factors of \(m'\) and \(n'\). So \(\sqrt{3} = \frac{m}{n}\) for some integers \(m\) and \(n\) which have no common factors. Squaring both sides of this equation gives \(3 = \frac{m^2}{n^2}\) and re-arranging gives \(3n^2 = m^2\). From this equation we see that \(m^2\) is divisible by 3; you proved in the previous section (Exercise 6) that \(m^2\) is divisible by 3 iff \(m\) is divisible by 3. Therefore \(m\) is divisible by 3 and we can write \(m = 3k\) for some integer \(k\). Substituting \(m = 3k\) into the last equation above gives \(3n^2 = (3k)^2\) or \(3n^2 = 9k^2\), which in turn becomes \(n^2 = 3k^2\). From this we see that \(n^2\) is divisible by 3, and again we know that this implies that \(n\) is divisible by 3. But now we have (i) \(m\) and \(n\) have no common factors, and (ii) \(m\) and \(n\) have a common factor, namely 3. It is impossible for both these things to be true, yet our argument has been logically correct. Therefore our original assumption, namely that \(\sqrt{3}\) is rational, must be incorrect. Therefore \(\sqrt{3}\) must be irrational.

One of the oldest mathematical proofs, which goes all the way back to Euclid, is a proof by contradiction. Recall that a prime number is an integer \(n\), greater than 1, such that the only positive integers that evenly divide \(n\) are 1 and \(n\). We will show that there are infinitely many primes. Before we get to the theorem, we need a lemma. (A **lemma** is a theorem that is introduced only because it is needed in the proof of another theorem. Lemmas help to organize the proof of a major theorem into manageable chunks.)

### Lemma 1.5. If \(N\) is an integer and \(N > 1\), then there is a prime number which evenly divides \(N\).

Proof. Let \(D\) be the smallest integer which is greater than 1 and which evenly divides \(N\). (\(D\) exists since there is at least one number, namely \(N\) itself, which is greater than 1 and which evenly divides \(N\). We use the fact that any non-empty subset of \(\mathbb{N}\) has a smallest member.) I claim that \(D\) is prime, so that \(D\) is a prime number that evenly divides \(N\). Suppose that \(D\) is not prime. We show that this assumption leads to a contradiction. Since \(D\) is not prime, then, by definition, there is a number \(k\) between 2 and \(D - 1\), inclusive, such that \(k\) evenly divides \(D\). But since D evenly divides \(N\), we also have that \(k\) evenly divides \(N\) (by exercise 5
