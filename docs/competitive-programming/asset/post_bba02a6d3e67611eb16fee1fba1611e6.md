
- 9. UVa 10814 - Simplifying Fractions (bignum gcd)
- 10. UVa 10106 - Product (bignum multiplication)
- 11. UVa 10473 - Simple Base Conversion (number base conversion)
- 12. UVa 10523 - Very Easy!!! (bignum addition, multiplication, and power)
- 13. UVa 10925 - Krakovia (bignum addition and division)
- 14. LA 4104 - MODEX (bignum modPow)

## 5.5 Miscellaneous Mathematics Problems

In this section, we list down a few more mathematics problems that have been used a few times in some programming contests. Mastering the solutions for these problems can be an advantage if you are given similar problem or problem that uses these knowledge as part of solution for the problem. The terms mentioned here also act as *keywords* for further study.

### 5.5.1 Combinatorics

**Combinatorics** [31] is a branch of *discrete* mathematics concerning the study of finite or **countable** discrete structures. Programming problems involving combinatorics usually titled 'How Many [Object]', 'Count [Object]', etc, although some problem setters choose to hide this fact from their problem title. The code is usually short, but finding the recurrence formula takes some mathematics brilliance and patience. In ICPC, if such problem exists in the given problem set, ask one team member to derive the formula whereas the other two concentrate on other problems. Quickly code the usually short formula once it is obtained.

For example, try solving UVa 10401 - Triangle Counting. This problem has a short description: “given *n* rods of length 1, 2, ..., *n*, pick any 3 of them & build a triangle. How many distinct triangles can you make? (3 ≤ *n* ≤ 1M)”. Note that, two triangles will be considered different if they have at least one pair of arms with different lengths. If you are lucky, you may spend only a few minutes to spot the pattern. Otherwise, this problem may end up unsolved by the time contest is over. Hint: answers for few small *n* = 3, 4, 5, 6, 7, 8, 9, and 10 are 0, 1, 3, 7, 13, 22, 34, and 50, respectively.

Programming Exercises related to Combinatorics (also see Fibonacci Numbers above):

- 1. UVa 326 - Extrapolation using a Difference Table
- 2. UVa 369 - Combinations (be careful with overflow issue)
- 3. UVa 991 - Safe Salutations (Catalan Numbers)
- 4. UVa 10007 - Count the Trees (Catalan Numbers, see [30] for details)
- 5. UVa 10219 - Find the Ways! (use Java BigInteger class)
- 6. UVa 10303 - How Many Trees (Catalan Numbers)
- 7. UVa 10375 - Choose and Divide
- 8. UVa 10784 - Diagonal
- 9. UVa 10790 - How Many Points of Intersection?
- 10. UVa 10918 - Tri Tiling
- 11. UVa 11069 - A Graph Problem
- 12. UVa 11115 - Uncle Jack ($N^D$, use Java BigInteger class)
- 13. UVa 11204 - Musical Instruments (only 1st choice matters)
- 14. UVa 11310 - Delivery Debacle
- 15. UVa 11401 - Triangle Counting (spot the pattern, coding is easy)
- 16. UVa 11554 - Hapless Hedonism (similar to UVa 11401)

### 5.5.2 Cycle-Finding

**Cycle-finding** [32] is a problem of finding a cycle in a sequence of iterated function values.

For any function $f:S\to S$ and any initial value $x_0\in S$, the sequence of iterated function values: $x_0,x_1=f(x_0),x_2=f(x_1),\ldots,x_i=f(x_{i-1}),\ldots$ must eventually use the same value twice (cycle), i.e. $\exists\ i\ne j$ such that $x_i=x_j$. Once this happens, the sequence must repeat the cycle of values from $x_i$ to $x_{j-1}$. We let $\mu$ be the smallest index $i$ and let $\lambda$ (the loop length) be the smallest positive integer such that $x_\mu=x_{\mu+\lambda}$. The cycle-finding is the problem of finding $\mu$ and $\lambda$, given $f$ and $x_0$.

For example in UVa 350 - Pseudo-Random Numbers, we are given a pseudo-random number generator $f(x)=(Z\times x+I)\%M$ with $x_0=L$ and we want to find out the sequence length before any number is repeated.

A naïve algorithm that works in general for this problem uses a data structure (e.g. C++ STL `<set>`, hash table or direct addressing table) to store information that a number $x_i$ has been visited in the sequence and then for each $x_i$ found later ($i>j$), we test if $x_i$ is stored in the data structure or not. If it is, it implies that $x_j=x_i$, $\mu=j$, $\lambda=i-j$. This algorithm runs in $O(\mu+\lambda)$ but also requires at least $O(\mu+\lambda)$ space to store past values.

There is a better algorithm called Floyd’s Cycle-Finding algorithm [32] that runs in the same $O(\mu+\lambda)$ time complexity but only uses $O(1)$ memory space—much smaller than the naïve version. The working C/C++ implementation of this algorithm is shown below:

```cpp
pair<int, int> floyd_cycle_finding(int (*f)(int), int x0) {
  // The main phase of the algorithm, finding a repetition x_i = x_{2i}, hare speed is 2x tortoise’s
  int tortoise = f(x0), hare = f(f(x0)); // f(x0) is the element/node next to x0
  while (tortoise != hare) { tortoise = f(tortoise); hare = f(f(hare)); }
  // Find the position μ of the hare and tortoise move at the same speeds
  int mu = 0; hare = tortoise; tortoise = x0;
  while (tortoise != hare) { tortoise = f(tortoise); hare = f(hare); mu += 1; }
  // Find the length of the shortest cycle starting from x_mu, hare moves, tortoise stays
  int lambda = 1; hare = f(tortoise);
  while (tortoise != hare) { hare = f(hare); lambda += 1; }
  return make_pair(mu, lambda);
}
```

Programming Exercises related to Cycle-Finding:

- 1. UVa 350 - Pseudo-Random Numbers (straightforward application of Floyd’s cycle-finding)
- 2. UVa 408 - Uniform Generator
- 3. UVa 944 - Happy Numbers (similar to UVa 10591)
- 4. UVa 10591 - Happy Number
- 5. UVa 11036 - Eventually periodic sequence
- 6. UVa 11053 - Flavius Josephus Reloaded
- 7. UVa 11549 - Calculator Conundrum

### 5.5.3 Existing (or Fictional) Sequences and Number Systems

Some Ad Hoc mathematical problems involve a definition of existing (or fictional) number Sequence or Number System and our task is to produce either the sequence/number within some range or the n-th one, verify if the given sequence/number is valid according to definition, etc. Usually, following the description carefully is sufficient to solve the problem.

Programming Exercises related to Sequences and Number Systems:

- Sequences
  - 1. UVa 100 - The 3n + 1 problem
  - 2. UVa 413 - Up and Down Sequences
  - 3. UVa 694 - The Collatz Sequence (similar to UVa 100)
  - 4. UVa 10408 - Farey Sequences
  - 5. UVa 10930 - A-Sequence
  - 6. UVa 11063 - B2 Sequences
- Number Systems
  - 1. UVa 136 - Ugly Numbers
  - 2. UVa 138 - Street Numbers
  - 3. UVa 443 - Humble Numbers
  - 4. UVa 640 - Self Numbers (DP)
  - 5. UVa 962 - Taxicab Numbers (Pre-calculate the answer)
  - 6. UVa 974 - Kaprekar Numbers
  - 7. UVa 10001 - Bangla Numbers
  - 8. UVa 10006 - Carmichael Numbers
  - 9. UVa 10042 - Smith Numbers
  - 10. UVa 10044 - Erdos Numbers (solvable with BFS)
  - 11. UVa 10591 - Happy Number (solvable with the Floyd’s Cycle-Finding algorithm)
  - 12. UVa 11461 - Square Numbers
  - 13. UVa 11472 - Beautiful Numbers

### 5.5.4 Probability Theory

**Probability Theory** is a branch of mathematics concerned with analysis of random phenomena. Although an event like an individual coin toss is random, if it is repeated many times the sequence of random events will exhibit certain statistical patterns, which can be studied and predicted.

In programming contests, such problems are either solvable with some closed-form formula, or one has no choice but to enumerate the complete search space.

Programming Exercises related to Probability:

- 1. UVa 474 - Heads Tails Probability
- 2. UVa 542 - France 98
- 3. UVa 10056 - What is the Probability?
- 4. UVa 10491 - Cows and Cars
- 5. UVa 11176 - Winning Streak
- 6. UVa 11181 - Probability|Given
- 7. UVa 11500 - Vampires

### 5.5.5 Linear Algebra

A **linear equation** is defined as an equation where the order of the unknowns (variables) is **linear** (a constant or a product of a constant plus the first power of an unknown), e.g. `X + Y = 2`. **System of linear equations** is defined as a collection of $n$ unknowns (variables) in $n$ linear equations, e.g. `X + Y = 2` and `2X + 5Y = 6`, where the solution is $X = \frac{1}{3}, Y = \frac{2}{3}$. Notice the difference to the **linear Diophantine equation** as the solution for system of linear equations can be non-integers!

There are several ways to find the solution for a system of linear equations. One of them is ‘Gaussian Elimination’. See [5, 37] for details.

Programming Exercises related to Linear Algebra:

- 1. UVa 10089 - Repackaging
- 2. UVa 10109 - Solving Systems of Linear Equations
- 3. UVa 10309 - Turn the Lights Off

## 5.6 Chapter Notes

We admit that there are still a lot of other mathematics problems and algorithms beyond this chapter. This last section provides pointers for a few more topics.

For an even **faster prime testing** function than the one presented here, one can use the non-deterministic **Miller-Rabin’s** algorithm [41] — which can be made deterministic for contest environment with a known maximum input size $N$.
