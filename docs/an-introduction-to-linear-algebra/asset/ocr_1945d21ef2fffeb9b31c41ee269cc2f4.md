# Chapter 5

# Linear Systems

Systems of linear algebraic equations arise in many diverse disciplines, such as biology, business, engineering, social sciences, and statistics. Therefore, understanding the basic theory and finding efficient methods for the solutions of such systems is of great importance. We shall devote this and the next chapters to study linear systems.

Let $F$ be a given infinite field. Consider the *nonhomogeneous* linear system of $m$ equations in $n$ unknowns

$$\begin{aligned}
a_{11}x_1+a_{12}x_2+\cdots+a_{1n}x_n&=b_1\\
a_{21}x_1+a_{22}x_2+\cdots+a_{2n}x_n&=b_2\\
&\vdots\\
a_{m1}x_1+a_{m2}x_2+\cdots+a_{mn}x_n&=b_m,
\end{aligned}\tag{5.1}$$

where $a_{ij}, b_i\in F$. In matrix form this system can be written as

$$Ax=b,\tag{5.2}$$

where the matrix $A=(a_{ij})_{m\times n}$ and the vectors $x=(x_1,x_2,\cdots,x_n)^t$, and $b=(b_1,b_2,\cdots,b_m)^t$. By a solution $x$ to (5.1) we mean an $n$-tuple that satisfies (5.1). The system (5.1) is said to be consistent if it has a solution, otherwise it is called *inconsistent*. If $b=0$, (5.2) reduces to the *homogeneous system*

$$Ax=0.\tag{5.3}$$

For the homogeneous system (5.3) the zero vector $0=(0,0,\cdots,0)^t$ is always a solution. This solution is called the *trivial solution* of (5.3). Clearly, the system (5.3) besides the trivial solution may also have other solutions. Such solutions we call *nontrivial solutions* of (5.3). Let $F_n$ be the set of all solutions of (5.3), i.e., $F_n=\{x:x\in F^n\text{ such that }Ax=0\}$, then it follows that $(F_n,F)$ with the same addition and scalar multiplication as in Example 1.2 is a vector space. We call $(F_n,F)$ the *solution space* of the homogeneous system (5.3), or the *null space*, or the *kernel* of the matrix $A$, and denote it as $\mathcal{N}(A)$. It is clear that the set of all solutions of the nonhomogeneous system (5.2) is not a vector space.