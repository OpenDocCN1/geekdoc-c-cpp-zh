then minimize

```
$\mathscr{F}_1 = \sum_{i=1}^{n} f_i^2;$
```

usually $f_i$ are defined by simple algebraic formulas (without radicals), and the resulting solution is called *algebraic fit*.

In this chapter we describe the most popular geometric fits (type A). The next chapter is devoted to algebraic approximative methods (type B).

**Comparison.** The geometric fit is commonly regarded as being more accurate than algebraic fits (even though this opinion is based mostly on practical experience; our Chapter 7 provides some theoretical analysis of this issue). But every geometric fitting procedure is iterative, subject to occasional divergence, and in any case computationally expensive. On the contrary, algebraic fits are usually simple, reliable, and fast.

Algebraic fits are often used to supply an initial guess to a subsequent iterative geometric fitting routine. Some modern algebraic fits, however, are so accurate that geometric fits would not make much further improvement. In most practical applications a well designed algebraic fit (such as Taubin’s or Pratt’s method, see the next chapter) will do a satisfactory job.

Thus the reader who is just looking for a simple and efficient circle fit should go directly to the next chapter and check the Pratt fit or (even better) the Taubin circle fit. The reader who needs a geometric fit, regardless of its high cost, or who wants to learn this topic in general, should read this chapter.

# 4.1 	 Classical minimization schemes

We begin with a brief description of general numerical schemes used to minimize smooth functions of several variables, especially those adapted to least squares problems. First we recall two classical algorithms that are a part of any standard numerical analysis course.

**Steepest descent.** Suppose we need to find the minimum of a smooth function $\mathscr{G}: \mathbb{R}^k \rightarrow \mathbb{R}$, i.e.,

```
$z = \mathscr{G}(\mathbf{a}), \qquad \mathbf{a} = (a_1, \ldots, a_k) \in \mathbb{R}^k \qquad (4.1)$
```

of $k$ variables. Iterative procedures usually compute a sequence of points $\mathbf{a}^{(0)}$, $\mathbf{a}^{(1)}, \ldots$ that presumably converges to a point where $\mathscr{G}$ takes its minimum value. The starting point $\mathbf{a}^{(0)}$ (the *initial guess*) is assumed to be chosen somehow, and the procedure follows a certain rule to determine $\mathbf{a}^{(i+1)}$ given $\mathbf{a}^{(i)}$.

That is, to define a procedure, it suffices to describe the rule of constructing the next approximation, $\mathbf{a}'$, from the current approximation, $\mathbf{a}$.

We always assume that the derivatives of the function $\mathscr{G}$ can be evaluated; hence one can find the gradient vector $\nabla\mathscr{G}(\mathbf{a})$, and then the most logical move