where the curl operator is interpreted as acting separately on each column in the 3 × 3 matrix ∇v, and the 0 on the right stands for the zero 3 × 3 matrix. In summary, one can write in operator form

∇ × ∇ = 0.

If a vector function v has zero divergence, i.e.,

∇ · v = 0,

at every spatial point (x, y, z), then it can be written as the curl of another vector function w(x, y, z), i.e.,

v = ∇ × w

at every spatial point (x, y, z).

Conversely, if a vector field v can be written as the curl of another vector field w, then it is divergence-free:

∇ · ∇ × w = 0.

In operator form, one can equivalently write

∇ · ∇ × = 0.

Finally, from the above symbolic forms, one can also easily verify the formula

∇ × ∇ × = −Δ + (∇ · )^T .

Here, Δ is interpreted as the vector Laplacian, so the right-hand side is the sum of two 3 × 3 matrices: the negative of the vector Laplacian and the transpose of the gradient of the divergence. Note that although the gradient of the divergence is a symmetric matrix when operating on vector functions that are differentiable to the second order, it may act nonsymmetrically on vector functions with discontinuous second derivatives. This is why we bother to take its transpose in the above formula. This is particularly important in the weak formulation of the linear elasticity equations below, where derivatives are assumed to be square-integrable but not necessarily continuous.

# 21.2 General Linear Elasticity

Here, we use the above notation to write the linear elasticity equations in a more general and compact form. This form uses a three-dimensional setting, with the four unknown functions v1, v2, v3, and p defined in a three-dimensional domain Ω in the (x, y, z) Cartesian coordinate system. (The two-dimensional case can be obtained from this general form as a special case by assuming that v3 ≡ 0 and that the functions are independent of z. The system of PDEs in Section 2, can then be obtained from the present one by eliminating p, as discussed below.)

The unknown functions in the system of PDEs can be referred to as the scalar function p(x, y, z) and the vector function v(x, y, z), which contains the components v1(x, y, z), v2(x, y, z), and v3(x, y, z). Similarly, the right-hand-side functions are given as the scalar function g(x, y, z) and the vector function f(x, y, z).