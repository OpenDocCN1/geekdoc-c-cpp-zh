evaluated at the current (or i th) time level rather than the previous (or (i − 1)th) time level:

u_t(t,x) − ε u_xx(t,x) + C(t,x) u_x(t,x)
≐ (Δt)^−1 ( u_j^(i) − u_j^(i−1) ) + ( D^(i) u^(i) )_j = F(i Δt, j h)

where t = i Δt. Using this formula, the implicit scheme can be written compactly in terms of N-dimensional vectors as:

( I + (Δt) D^(i) ) u^(i) = u^(i−1) + (Δt) f^(i),

where I is the identity matrix of order N.

The calculation of u^(i) requires the “inversion” of the tridiagonal matrix I + (Δt) D^(i). Of course, the inverse of this matrix is never calculated explicitly, because this would be too expensive. By “inversion” we mean solving the above linear system for the unknown vector u^(i). The algorithm for doing this is discussed below. This completes the definition of the implicit time marching. The detailed implementation will be discussed later.

Although the computation of each individual u^(i) is more expensive than in the explicit scheme, the entire loop over the entire time-space grid is usually far less expensive, because M can be much smaller. Indeed, since the implicit scheme is unconditionally stable (Chapter 8, Section 8.3), it can use Δt as large as h. This reduces considerably the number of time levels M and the total computational cost.

The implicit scheme can actually be viewed as the analogue of the scheme in Chapter 6, Section 8, with the first-order Taylor approximation

exp(−(Δt) D^(i)) = exp((Δt) D^(i))^(−1) ≐ ( I + (Δt) D^(i) )^(−1).

# 7.7 The Semi-Implicit Scheme

The semi-implicit scheme, also known as the Crank–Nicolson or “midpoint” scheme, can be viewed as a compromise between the explicit and implicit schemes. In this scheme, the discrete convection-diffusion term is the average of the evaluation at the previous time level as in the explicit scheme and the evaluation at the current time level as in the implicit scheme:

u_t(t,x) − ε u_xx(t,x) + C(t,x) u_x(t,x)
≐ (Δt)^−1 ( u_j^(i) − u_j^(i−1) ) + 1/2 ( D^(i) u^(i) + D^(i−1) u^(i−1) )_j
= F((i − 1/2) Δt, j h)

at the “half” time level t = (i − 1/2) Δt. Because the time derivative u_t is discretized symmetrically around this half time level, the scheme is of second-order accuracy in time wherever the solution to the original PDE is indeed smooth in time.

The semi-implicit scheme can be written compactly as the vector equation

( I + Δt/2 D^(i) ) u^(i) = ( I − Δt/2 D^(i−1) ) u^(i−1) + (Δt) f^(i−1/2).