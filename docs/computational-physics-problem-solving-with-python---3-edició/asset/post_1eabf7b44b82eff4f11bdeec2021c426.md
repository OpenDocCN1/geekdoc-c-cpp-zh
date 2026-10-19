
vertical directions must equal zero (Figure 6.2):

T₁ sin θ₁ − T₂ sin θ₂ − W₁ = 0 ,  (6.6)

T₁ cos θ₁ − T₂ cos θ₂ = 0 ,  (6.7)

T₂ sin θ₂ + T₃ sin θ₃ − W₂ = 0 ,  (6.8)

T₂ cos θ₂ − T₃ cos θ₃ = 0 .  (6.9)

Here Wᵢ is the weight of mass i and Tᵢ is the tension in string i. Note that because we do not have a rigid structure, we cannot assume the equilibrium of torques.

## 6.1.2
### Algorithm: Multidimensional Searching

Equations (6.1)–(6.9) are nine simultaneous nonlinear equations. While linear equations can be solved directly, nonlinear equations cannot (Press et al., 1994). You can use the computer to search for a solution by guessing, but there is no guarantee of finding one.

Unfortunately, not everything in life is logical, as we need to use a search technique now that will not be covered until Chapter 7. While what we do next is self-explanatory, you may want to look at Chapter 7 now if you are not at all familiar with searching.

We apply to our set the same Newton–Raphson algorithm as used to solve a single equation by renaming the nine unknown angles and tensions as the subscripted variable yᵢ and placing the variables together as a vector:

y = [x₁ x₂ x₃ x₄ x₅ x₆ x₇ x₈ x₉]ᵀ = [sin θ₁ sin θ₂ sin θ₃ cos θ₁ cos θ₂ cos θ₃ T₁ T₂ T₃]ᵀ .  (6.10)

The nine equations to be solved are written in a general form with zeros on the right-hand sides and placed in a vector:

fᵢ(x₁, x₂, …, x_N) = 0 ,   i = 1, N ,  (6.11)

f(y) = ( f1(y) f2(y) f3(y) f4(y) f5(y) f6(y) f7(y) f8(y) f9(y) ) = ( 3x4 + 4x5 + 4x6 - 8 3x1 + 4x2 - 4x3 x7x1 - x8x2 - 10 x7x4 - x8x5 x8x2 + x9x3 - 20 x8x5 - x9x6 x1^2 + x4^2 - 1 x2^2 + x5^2 - 1 x3^2 + x6^2 - 1 ) = 0 . (6.12)

The solution to these equations requires a set of nine x_i values that make all nine f_i's vanish simultaneously. Although these equations are not very complicated (the physics after all is elementary), the terms quadratic in x make them nonlinear, and this makes it hard or impossible to find an analytic solution. The search algorithm guesses a solution, expands the nonlinear equations into linear form, solves the resulting linear equations, and continues to improve the guesses based on how close the previous one was to making f = 0. (We discuss search algorithms using this procedure in Chapter 7.)

Explicitly, let the approximate solution at any one stage be the set x_i and let us assume that there is an (unknown) set of corrections Δx_i for which f_i(x1 + Δx1, x2 + Δx2, ..., x9 + Δx9) = 0 , i = 1, 9 . (6.13)

We solve for the approximate Δx_i's by assuming that our previous solution is close enough to the actual one for two terms in the Taylor series to be accurate:

f_i(x1 + Δx1, ..., x9 + Δx9) ≈ f_i(x1, ..., x9) + Σ_{j=1}^9 ∂f_i/∂x_j Δx_j = 0 i = 1, ..., 9 . (6.14)

We now have a solvable set of nine linear equations in the nine unknowns Δx_i, which we express as a single matrix equation f1 + ∂f1/∂x1 Δx1 + ∂f1/∂x2 Δx2 + ... + ∂f1/∂x9 Δx9 = 0 , f2 + ∂f2/∂x1 Δx1 + ∂f2/∂x2 Δx2 + ... + ∂f2/∂x9 Δx9 = 0 , ... f9 + ∂f9/∂x1 Δx1 + ∂f9/∂x2 Δx2 + ... + ∂f9/∂x9 Δx9 = 0 , ( f1 f2 ... f9 ) + ( ∂f1/∂x1 ∂f1/∂x2 ... ∂f1/∂x9 ∂f2/∂x1 ∂f2/∂x2 ... ∂f2/∂x9 ... ∂f9/∂x1 ∂f9/∂x2 ... ∂f9/∂x9 ) ( Δx1 Δx2 ... Δx9 ) = 0 . (6.15)

Note now that the derivatives and the $f$’s are all evaluated at known values of the $x_i$’s, so that only the vector of the $\Delta x_i$ values is unknown. We write this equation in matrix notation as

$$\boldsymbol{f} + F' \Delta \boldsymbol{x} = 0\;,\quad \Rightarrow\quad F' \Delta \boldsymbol{x} = -\boldsymbol{f}\;,\tag{6.16}$$ $$\Delta \boldsymbol{x} = \begin{pmatrix} \Delta x_1 \\ \Delta x_2 \\ \vdots \\ \Delta x_9 \end{pmatrix}\;,\quad \boldsymbol{f} = \begin{pmatrix} f_1 \\ f_2 \\ \vdots \\ f_9 \end{pmatrix}\;,\quad F' = \begin{pmatrix} \partial f_1/\partial x_1 & \cdots & \partial f_1/\partial x_9 \\ \partial f_2/\partial x_1 & \cdots & \partial f_2/\partial x_9 \\ \vdots & & \\ \partial f_9/\partial x_1 & \cdots & \partial f_9/\partial x_9 \end{pmatrix}.$$

Here we use bold italic letters to emphasize the vector nature of the columns of $f_i$ and $\Delta x_i$ values, and denote the matrix of the derivatives $F'$ (it is also sometimes denoted by $J$ because it is the Jacobian matrix).

The equation $F' \Delta \boldsymbol{x} = -\boldsymbol{f}$ is in the standard form for the solution of a linear equation (often written as $A\boldsymbol{x} = \boldsymbol{b}$), where $\Delta \boldsymbol{x}$ is the vector of unknowns and $\boldsymbol{b} = -\boldsymbol{f}$. Matrix equations are solved using the techniques of linear algebra, and in the sections to follow we shall show how to do that. In a formal sense, the solution of (6.16) is obtained by multiplying both sides of the equation by the inverse of the $F'$ matrix:

$$\Delta \boldsymbol{x} = -F'^{-1} \boldsymbol{f}\;,\tag{6.17}$$

where the inverse must exist if there is to be a unique solution. Although we are dealing with matrices now, this solution is identical in form to that of the 1D problem, $\Delta x = -(1/f')f$. In fact, one of the reasons, we use formal or abstract notation for matrices is to reveal the simplicity that lies within.

As we indicate for the single-equation Newton–Raphson method in Section 7.3, even in a case such as this where we can deduce analytic expressions for the derivatives $\partial f_i/\partial x_j$, there are $9 \times 9 = 81$ such derivatives for this (small) problem, and entering them all would be both time-consuming and error-prone. In contrast, especially for more complicated problems, it is straightforward to program a forward-difference approximation for the derivatives,

$$\frac{\partial f_i}{\partial x_j} \simeq \frac{f_i(x_j + \delta x_j) - f_i(x_j)}{\delta x_j}\;,\tag{6.18}$$

where each individual $x_j$ is varied independently because these are partial derivatives and $\delta x_j$ are some arbitrary changes you input. While a central-difference approximation for the derivative would be more accurate, it would also require more evaluations of the $f$’s, and once we find a solution it does not matter how accurate our algorithm for the derivative was.

As also discussed for the 1D Newton–Raphson method (Section 7.3.1), the method can fail if the initial guess is not close enough to the zero of $f$ (here all $N$ of them) for the $f$’s to be approximated as linear. The backtracking technique may be applied here as well, in the present case, progressively decreasing the corrections $\Delta x_i$ until $\|f\|^2 = |f_1|^2 + |f_2|^2 + \cdots + |f_N|^2$ decreases.

## 6.2
### Why Matrix Computing?

Physical systems are often modeled by systems of simultaneous equations written in matrix form. As the models are made more realistic, the matrices correspondingly become larger, and it becomes more important to use a good linear algebra library. Computers are unusually good with matrix manipulations because those manipulations typically involve the continued repetition of a small number of simple instructions, and algorithms exist to do this quite efficiently. Further speedup may be achieved by *tuning* the codes to the computer's architecture, as discussed in Chapter 11.

Industrial-strength subroutines for matrix computing are found in well-established scientific libraries. These subroutines are usually an order of magnitude or more faster than the elementary methods found in linear algebra texts,² are usually designed to minimize the round-off error, and are often “robust,” that is, have a high chance of being successful for a broad class of problems. For these reasons, we recommend that you *do not write your own matrix methods* but instead get them from a library. An additional value of library routines is that you can often run the same program either on a desktop machine or on a parallel supercomputer, with matrix routines automatically adapting to the local architecture. The thoughtful reader may be wondering when a matrix is “large” enough to require the use of a library routine. One rule of thumb is “if you have to wait for the answer,” and another rule is if the matrices you are using take up a good fraction of your computer's random-access memory (RAM).

## 6.3
### Classes of Matrix Problems (Math)

It helps to remember that the rules of mathematics apply even to the world's most powerful computers. For example, you *should* encounter problems solving equations if you have more unknowns than equations, or if your equations are not linearly independent. But do not fret. While you cannot obtain a unique solution when there are not enough equations, you may still be able to map out a space of allowable solutions. At the other extreme, if you have more equations than unknowns, you have an *overdetermined* problem, which may not have a unique solution. An overdetermined problem is sometimes treated using data fitting techniques in which a solution to a sufficient set of equations is found, tested on the unused equations, and then improved if needed. Not surprisingly, this technique

2) Although we prize the book, *Numerical Recipes* by Press et al. (1994), and what it has accomplished, we cannot recommend taking subroutines from it. They are neither optimized nor documented for easy, stand-alone use, whereas the subroutine libraries recommended in this chapter are.
