This chapter presents a brief introduction to the theory of expensive and impossible problems. Section 17.1 presents the concept of a reduction, which is the central tool used for analyzing the difficulty of a problem (as opposed to analyzing the cost of an algorithm). Reduction allows us to relate the difficulty of various problems from first principles. Section 17.2 discusses “hard” problems, by which we mean problems that, at least appear to require, time exponential on the input size. Finally, 17.3 considers problems that, while simple to define and comprehend, are in fact impossible to solve using a computer program. The classic example of such a problem is deciding whether an arbitrary program will go into an infinite loop when processing a specified input. This is known as the halting problem.

# 17.1 Reductions

We begin with an important concept for understanding the relationships between problems, called reduction. Reduction allows us to solve one problem in terms of another. Equally importantly, when we wish to understand the difficulty of a problem, reduction allows us to make relative statements about upper and lower bounds on the cost of a problem (as opposed to an algorithm or program).

Because the concept of a problem is discussed extensively in this chapter, we want notation in terms of a mapping between inputs and outputs, and the name of the problem will be defined in all capital letters. Thus, a complete definition of the sorting problem could appear as:

+   SORTING:
**Input:** A sequence of integers $x_0, x_1, x_2, \dots, x_{n-1}$.
**Output:** A permutation $y_0, y_1, y_2, \dots, y_{n-1}$ of the sequence such that $y_i \le y_j$ whenever $i < j$.

When you write a program to solve one problem, such as sorting, you might be able to use it to help solve a different problem. This is known in software engineering as software reuse. To illustrate this, let us consider another problem.

+   PAIRING:
**Input:** Two sequences of integers $X = (x_0, x_1, \dots, x_{n-1})$ and $Y = (y_0, y_1, \dots, y_{n-1})$.
**Output:** A pairing of the elements in the two sequences such that the least value in $X$ is paired with the least value in $Y$, the next value in $X$ is paired with the next least value in $Y$, and so on.