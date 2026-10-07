# Chapter 8

# Algorithms 23

We conclude that, given any instance $I$ of problem A, we can construct a polynomial time circuit whose known inputs are the bits of $I$, and whose unknown inputs are the bits of $S$, such that the output is $true$ if and only if the unknown inputs spell a solution $S$ of $I$. In other words, the satisfying truth assignments of the circuit are in one-to-one correspondence with the solutions of instance $I$ of A. The reduction is complete.

# Unsolvable problems

At least an NP-complete problem can be solved by some algorithm—the trouble is that this algorithm will be exponential. But it turns out there are difficult computational problems for which no algorithm exists at all!

One famous problem of this sort is an arithmetic version of SAT. Given an equation in many variables, perhaps

```
$x^3y e+2y^3z^2-7xy^5z=6$,
```

are integer values of $x, y, z$ that satisfy it? There is no algorithm that solves this problem. No algorithm at all, polynomial, exponential, doubly exponential, or recursive problems are unsolvable.

The first unsolvable problem was discovered in 1936 by Alan M. Turing, a student of mathematics at Cambridge, England. When Turing came up with it, there were no computers or programming languages (in fact, it can be argued that these things came later because this brilliant thought occurred to Turing). But today we can see it in familiar terms.

Suppose that are given a program in your favorite programming language, along with a particular input. Will the program ever terminate, once started on this input? This is a very reasonable question. Many of us would be ecstatic if we had an algorithm, call it terminates(p,x), that takes as input a file containing program $p$, and a file of data $x$, and after grinding away, finally tells us whether or not $p$ would ever stop if started on x.

But how would you go writing the program terminates? (If you haven't seen this before, it's worth thinking about it for a while, to appreciate the difficulty of writing such a universal infinite-loop detector.)

Well, you can't. Such an algorithm does not exist!

And here is the proof: Suppose we actually had such a program terminates(p,x). Then we could use it as a subroutine of the following evil program:

```
function paradox(z:file)
1: if terminates(z,z) goto 1
```