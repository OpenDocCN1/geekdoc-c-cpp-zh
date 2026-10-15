between the spatial nodes, as averages of the adjacent regular values $D_{i-1}$, $D_i$, and $D_{i+1}$:

$$D_{i\pm1/2}=\frac{1}{2}[D_i+D_{i\pm1}].$$

The desired overall $O(h_t^2+h_x^2)$ precision is ensured by applying the Crank–Nicolson method based on the spatial difference scheme (13.79), and this results in the following discretized form of the diffusion equation:

$$\frac{u_i^{n+1}-u_i^n}{h_t}=\frac{1}{2h_x}\left[D_{i+1/2}\frac{u_{i+1}^{n+1}-u_i^{n+1}}{h_x}-D_{i-1/2}\frac{u_i^{n+1}-u_{i-1}^{n+1}}{h_x}\right]+\frac{1}{2h_x}\left[D_{i+1/2}\frac{u_{i+1}^{n}-u_i^{n}}{h_x}-D_{i-1/2}\frac{u_i^{n}-u_{i-1}^{n}}{h_x}\right].$$

Separating the terms corresponding to $t_n$ and $t_{n+1}$ gives rise to the linear system:

$$-\lambda_{i-1/2}u_{i-1}^{n+1}+(1+2\lambda_i)u_i^{n+1}-\lambda_{i+1/2}u_{i+1}^{n+1}=\\ \lambda_{i-1/2}u_{i-1}^{n}+(1-2\lambda_i)u_i^{n}+\lambda_{i+1/2}u_{i+1}^{n},\qquad i=2,3,\ldots,N_x-1.$$

with

$$\lambda_i=\frac{1}{2}\frac{D_i h_t}{h_x^2},\qquad \lambda_{i\pm1/2}=\frac{1}{4}\frac{(D_i+D_{i\pm1/2})h_t}{h_x^2}.$$

To account for specific physical conditions, the above system must be accompanied by appropriate boundary conditions. In particular, Dirichlet conditions fix the solution values on the boundaries:

$$u_1^{n+1}=u_1^n,\qquad u_{N_x}^{n+1}=u_{N_x}^n.$$

while Neumann conditions define the boundary derivatives (fluxes):

$$-D_1\frac{u_2^{n+1}-u_1^{n+1}}{h_x}=J_{\mathrm{diff}}^{(1)},\qquad -D_{N_x}\frac{u_{N_x}^{n+1}-u_{N_x-1}^{n+1}}{h_x}=J_{\mathrm{diff}}^{(2)}$$

or

$$u_1^{n+1}-u_2^{n+1}=h_xJ_{\mathrm{diff}}^{(1)}/D_1,\qquad -u_{N_x-1}^{n+1}+u_{N_x}^{n+1}=-h_xJ_{\mathrm{diff}}^{(2)}/D_{N_x}.$$

Finally, the relevant coefficients of the first and last rows of the tridiagonal discretized system, coding the boundary conditions, are

$$\begin{array}{llll}
 b_1=1,&c_1=0,&d_1=u_1^n,&\text{Dirichlet},\\
 b_1=1,&c_1=-1,&d_1=h_xJ_{\mathrm{diff}}^{(1)}/D_1,&\text{Neumann},\\
 a_{N_x}=0,&b_{N_x}=1,&d_{N_x}=u_{N_x}^n,&\text{Dirichlet},\\
 a_{N_x}=-1,&b_{N_x}=1,&d_{N_x}=-h_xJ_{\mathrm{diff}}^{(2)}/D_{N_x},&\text{Neumann}.
\end{array}$$

while the elements on the rest of the rows read ($i=2,3,\ldots,N_x-1$):

$$a_i=-\lambda_{i-1/2},\qquad b_i=1+2\lambda_i,\qquad c_i=-\lambda_{i+1/2},$$

$$d_i=\lambda_{i-1/2}u_{i-1}^n+(1-2\lambda_i)u_i^n+\lambda_{i+1/2}u_{i+1}^n.$$