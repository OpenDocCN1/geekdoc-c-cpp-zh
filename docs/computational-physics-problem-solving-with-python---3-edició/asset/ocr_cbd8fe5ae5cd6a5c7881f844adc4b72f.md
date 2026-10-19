![](bbox=[0.141, 0.094, 0.803, 0.223])

Because this choice means that each basis function equals 0 or 1 at the nodes,

$$\phi_i(x_j)=\delta_{ij}, \tag{23.11}$$

the values of the expansion coefficients $\alpha_i$ must equal the values of the (still unknown) solution at the nodes:

$$U(x_i)\simeq\sum_{i=0}^{N-1}\alpha_i\phi_i(x_i)=\alpha_i\phi_i(x_i)=\alpha_i, \tag{23.12}$$

$$\Rightarrow\quad U(x)\simeq\sum_{j=0}^{N-1}U(x_j)\phi_j(x). \tag{23.13}$$

Equation 23.13 makes it clear that the expansion in terms of basis functions is essentially an interpolation between the actual solution at the nodes.

# 23.4.2.1  Solution via Linear Equations

Because the basis functions $\phi_i$ in (23.9) are known, solving for $U(x)$ involves determining the coefficients $\alpha_j$, which, as we just said, are the unknown values of the true solution $U(x)$ on the nodes. We determine those values by substituting the expansions for $U(x)$ and $\Phi(x)$ into the weak form of the PDE (23.8). This converts the integral equation into a set of simultaneous linear equations. As discussed in Chapter 6, there is a standard matrix form for a set of linear equations,

$$A\,y=b. \tag{23.14}$$

Our equations fit that, with $y$ a vector of unknowns, and where we still need to specify the known stiffness matrix $A$ and the known load matrix $b$. To that end, we substitute the expansion $U(x)\simeq\sum_{j=0}^{N-1}\alpha_j\phi_j(x)$ into the weak form (23.8) to obtain:

$$\int_a^b dx\,\frac{d}{dx}\left(\sum_{j=0}^{N-1}\alpha_j\phi_j(x)\right)\frac{d\Phi}{dx}=\int_a^b dx\,4\pi\rho(x)\Phi(x).$$