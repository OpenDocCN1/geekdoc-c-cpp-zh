
124 ■ Limits of Computation

## Theorem 6.1

There are many (uncountably many) languages that are not decided—accepted—by any Turing machine.

## 6.5 CONSTRUCTION OF THE UNDECIDABLE LANGUAGE $ACCEPT_{TM}$

Now we know undecidable languages exist (by counting arguments), but we have not yet produced an example. We have shown that there are uncountably many languages and only countably decidable languages (since countably many Turing machines means uncountable number of undecidable languages, should it be easy to actually display one? Well, not quite. Essentially any description of a language that you are likely to come up with have a deciding Turing machine. We want to produce an undecidable language.

This will be done by constructing a language that is not decided. This is essentially the same proof (by contradiction) as the proofs that writing "Hello World" or detecting infinite loops are not decidable.

Let $ACCEPT_{TM} = \{M, w: M \text{ is the encoding of a Turing machine, w \text{ is the encoding of a string, and } M \text{ accepts } w\}$

## Theorem 6.2

The language $ACCEPT_{TM}$ is not decided by any Turing machine.

## Proof

By contradiction, suppose $ACCEPT_{TM}$ is decided by a Turing machine $M_{ACCEPT}$. That is, $M_{ACCEPT}$ takes an encoded Turing machine $M$ and string $w$ goes to $q_{accept}$ exactly when $M$ accepts $w$; otherwise, it will terminate in $q_{reject}$. Of course, it terminates in one or the other since it is a deciding TM. This is shown in the first part of Figure 6.13.

Now, we modify $M_{ACCEPT}$ so that it takes machines as input—that is, its input is an encoded machine $M$. $M_{ACCEPT}$ will tell if the machine $M$ accepts its own description.

![](img/d80067a1fcf4f931f840f447fc7d1650_146_0.png)

FIGURE 6.13 Deciding Turing machine $M_{ACCEPT}$ for ACCEPT (and two modifications).

One more transformation is in order—accepting and rejecting states. Call this machine $M_{REVISED}$ or $M_R$ for short.

Now, when we use self-reference (that is, sending $M_R$ into $M_R$), we get a contradiction, or impossible situation. $M_R$ should go to $q_{reject}$ (reject $M_R$) exactly when $M_R$ accepts $M_{ACCEPT}$.

And, it goes to $q_{accept}$ exactly when $M_R$ does not accept $M_R$. This cannot happen, but it is a direct result of the one assumption that $M_{ACCEPT}$ exists as a deciding Turing machine. Thus, the contradiction must be in the existence of the de-deciding Turing machine $M_{ACCEPT}$.

The important point here is that $ACCEPT_{TM}$ is not decidable; however, it is Turing *acceptable* (by the universal Turing machine).

The above proof, with its contradiction, only works for deciding Turing machines. If not all strings end up in $q_{accept}$ and $q_{reject}$ there is no contradiction interchanging these states. The strings that did not end up in either one still not. What gives the contradiction is that since we are assuming a deciding TM, $M_R$ on $M_R$ has only the choice of $q_{accept}$ and $q_{reject}$ and both of these are impossible.

## Corollary 6.3

$ACCEPT_{TM}$ is not accepted by any Turing machine.

## Proof

$ACCEPT_{TM}$ has an accepting Turing machine (the universal Turing machine). If its complement were also accepted by some other Turing machine, then $ACCEPT_{TM}$ would be decidable.

## EXERCISES

- 1. Prove that the following sets have the same cardinalities.
   a. The natural numbers (1, 2, 3, ...) and the odd natural numbers (1, 3, 5, ...)
   b. The natural numbers and the rational numbers (n/m), where n, m are natural numbers $m \neq 0$
- 2. a. Consider the sentence “This sentence is false.” Is this sentence true or false?
   b. Consider the number $N$ = the smallest positive integer not named in eleven words—the smallest element of the set of numbers that take many many words to write out in English (such as “eight hundred twenty-two million three hundred forty-six thousand two hundred fifty-one”). Is there a problem here?
   c. Consider the sentences “I always lie” and “I always tell the truth.” Are these sentences self-referential? Are there problems with either one?
   d. What do parts a and b have to do with this course?
- 3. Look up Russell’s paradox. How was it resolved in set theory?
- 4. a. Consider the intermediate value theorem from calculus.
   If a real valued function $f$ is continuous on the closed interval $[a, b]$ and if $N$ is a number strictly between $f(a)$ and $f(b)$, then there exists a number $c$ in $(a, b)$ such that $f(c) = N$.

   Is this a constructive or existential theorem?

   What (if any) would be the advantages of a constructive theorem?

   What (if any) would be the advantages of an existential theorem?
-   b. Consider this quote from an article on routing in networks: "We give a nonconstructive proof of the existence of linear time algorithms that check whether a desired routing scheme exists for a given graph."

   Why would one prefer or not prefer a constructive proof?
- 5. Definition: An algebraic number is any number that satisfies an equation of the form

$$a_nx^n + a_{n-1}x^{n-1} + \dots + a_1x + a_0 = 0$$

where $n>0$, every $a_i$ is an integer, and $a_n$ nonzero

-   a. Show that the number $\sqrt{2}$ and the complex number $i=\sqrt{-1}$ are both algebraic.

-   b. Show that the cardinality of the algebraic numbers is countable.

-   c. What does this say about the existence of non-algebraic numbers? Can you produce a non-algebraic number?

- 6. Let $F = \{f: f \text{ is a function from the reals $(\mathbb{R})$ to the reals\}$. Show that the cardinality of $F$ is greater than $\mathfrak{R}$.

Hans L. Bodlaender, and Jan van Leeuwen. 1997. On Interval Routing Schemes and Treewidth. Information and Computation, 139, 92–109.

## Undecidability and Reducibility

## 7.1 UNDECIDABLE PROBLEMS: OTHER EXAMPLES

Once we have the first undecidable problem (whether Turing machine accepts the string), it is generally not necessary to use the first problem and the idea of reducibility to prove other problems are in the same category. The basic idea of reducibility is simple: if one has two questions, and if one knows the answer to question 1 by the answer to question 2, you do not need both answers. Answering question 2 will answer both of them. In some sense, question 2 must be harder (or at least as hard) as question 1, since an answer to it answers both.

Example

Question 1: Given a quadrilateral, is it a square (all sides and angles equal)?

Question 2: Given a polygon with $n \ge 3$ sides, are all the sides same length—is it equilateral and equiangular?

Clearly, if you had an answer to question 2, it would also answer question 1.

Example

Suppose there is a person, Professor Jones, who carries an umbrella exactly when it is raining (so rain $\rightightarrow$ umbrella; no rain (even if storms forecast) $\rightarrow$ no umbrella).

Question 1: Is it raining?
Question 2: Is Professor Jones carrying an umbrella?

In this (idealized) case, if you are sitting in a room with no windows and Professor Jones walks in, you can tell whether it is raining outside by noting whether Professor Jones came in with an umbrella or not.

Decision problem 1: At time t, is it raining?
Decision problem 2: At time t, is person X carrying an umbrella?

Example

Remote sensors are another example. A warning light for the temperature in a motor behaves so that:

Temperature too high $\rightarrow$ warning light on

Temperature not too high $\rightarrow$ warning light not on
