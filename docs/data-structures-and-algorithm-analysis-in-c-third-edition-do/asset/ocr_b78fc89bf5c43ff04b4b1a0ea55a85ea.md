# 17.2 Hard Problems

for TRAVELING SALESMAN and all related problems. Because TRAVELING SALESMAN is known to be $NP$-complete, if a polynomial time algorithm were to be found for this problem, then all problems in $NP$ would also be solvable in polynomial time. Conversely, if we were able to prove that TRAVELING SALESMAN has an exponential time lower bound, then we would know that $P 
eq NP$.

# 17.2.2 $NP$-Completeness Proofs

To start the process of being able to prove problems $NP$-complete, we need to prove just one $H$ is $NP$-complete. After that, to show that any problem $X$ is $NP$-hard, we need to reduce $H$ to $X$. When doing, $NP$-completeness proofs, it is very important not to get this reduction backwards! If we reduce candidate $X$ to known hard problem $H$, this means that we use $H$ as a step to solving $X$. When, when we reduce known hard problem $H$ to candidate problem $X$, we are using $X$ as a step to solve $H$. And if we know that $H$ is hard, then $X$ must also be hard (if $X$ were not hard, then there would be $H$ hard).

A crucial first step to getting this whole theory off the ground is finding one problem that is $NP$-hard. The first proof that a problem is $NP$-hard (and because it is in $NP$, therefore $NP$-complete) was done by Stephen Cook. For this, Cook won the first award, which is the closest Computer Science equivalent to the Nobel Prize. The “grand-daddy” $NP$-complete problem that Cook used is SATFIABILITY (or SAT for short).

A Boolean expression combines Boolean variables using the operators AND (-), OR (+), and NOT (to negate Boolean variable $x$). A literal is also a variable or its negation. A clause is one or more literals OR'ed together. Let $E$ be a Boolean expression over variables $x_1, x_2, \dots, x_n$. Then we define Conjunctive Normal Form (CNF) to be a Boolean expression written as series of classes that are AND'ed. For example,

```
$E = (x_5 + \overline{x_7} + x_{10}) \cdot (\overline{x_2} + x_3) \cdot (x_1 + \overline{x_3} + x_6)$
```

is in CNF, and has three clauses. Now we can define the problem.

SATFIABILITY (SAT)
Input: A Boolean expression over variables $x_1, x_2, ...$, in Conjunctive Normal Form.
Output: YES if there is an assignment to the variables that makes $E$ true, NO otherwise.

Cook proved SAT is $NP$-hard. Explaining Cook proof is beyond the scope of this book. But we can briefly summarize it as follows.: