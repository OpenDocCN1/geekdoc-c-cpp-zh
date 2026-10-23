# 10.7 Denoising Color Images

The denoising algorithm for color images is a natural extension of the above algorithm. Here, however, we have a system of three coupled, nonlinear PDEs, each of which solves for a different color. The solutions of the PDEs at the final time t = T, when confined to the discrete grid, produce the denoised color vectors. When these color vectors are combined, they produce the required denoised color image.

The system of coupled PDEs contains three nonlinear equations, one for each color:

r_t(t,x,y) - (P r_x(t,x,y))_x - (P r_y(t,x,y))_y = 0,
 g_t(t,x,y) - (P g_x(t,x,y))_x - (P g_y(t,x,y))_y = 0,
 b_t(t,x,y) - (P b_x(t,x,y))_x - (P b_y(t,x,y))_y = 0,

where 0 < t < T is the time variable; 0 ≤ x ≤ L_x and 0 ≤ y ≤ L_y are the spatial variables; r(t,x,y), g(t,x,y), and b(t,x,y) are the unknown functions; and the diffusion coefficient P (which depends nonlinearly on r_x(t,x,y), r_y(t,x,y), g_x(t,x,y), g_y(t,x,y), b_x(t,x,y), and b_y(t,x,y)) is defined by

P = det(E)^{-1},

where E is the 2 × 2 matrix

E = ( 1 + (r_x^2 + g_x^2 + b_x^2)/η   (r_x r_y + g_x g_y + b_x b_y)/η ; (r_x r_y + g_x g_y + b_x b_y)/η   1 + (r_y^2 + g_y^2 + b_y^2)/η ).

(Compare this system with the system in [63], [73], where E^{-1} is used instead of det(E)^{-1}.)

In order to complete the system of PDEs into a well-posed problem, one must also impose initial and boundary conditions for the functions r, g, and b. The boundary conditions are of homogeneous Neumann type:

r_n = g_n = b_n = 0,

where n is the outer normal vector at the boundary of the rectangular spatial domain. The initial conditions at t = 0 must agree with the original, noisy image in the grid: r(0,x,y) agrees with the noisy red color vector in the grid, g(0,x,y) agrees with the noisy green color vector in the grid, and b(0,x,y) agrees with the noisy blue color vector in the grid. The solutions of the PDEs at the final time t = T, when confined to the grid, produce the denoised color vectors: r(T,x,y) produces the denoised red color vector, g(T,x,y) produces the denoised green color vector, and b(T,x,y) produces the denoised blue color vector. These color vectors combine to produce the required denoised color image.

The discretization is the same as before. First, E is evaluated at the midpoints (j + 1/2,i) and (j,i + 1/2). Then, P is also evaluated there and used to construct the discrete spatial derivatives. The implicit scheme in Chapter 7, Section 6, is used to discretize the time derivatives. This scheme requires the solution of a large system of nonlinear difference equations at each time step.