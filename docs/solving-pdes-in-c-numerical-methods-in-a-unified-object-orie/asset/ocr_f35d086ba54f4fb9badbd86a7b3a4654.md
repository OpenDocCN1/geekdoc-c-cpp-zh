discretized implicitly as in Chapter 7, Section 6. (The semi-implicit scheme in Chapter 7, Section 7, is probably more accurate, although not used here.) This completes the definition of the discretization method.

# 10.5 Linearization

The above implicit scheme requires the solution of a nonlinear system of equations at each time step. The nonlinearity is in the coefficients $P_{j+1/2,i}$ and $P_{i,i+1/2}$ defined above, which depend on the unknown discrete solution $u$. A linearization method is thus needed to solve the system of equations iteratively.

Such a linearization is indeed used in Newton’s iteration (Section 9.16). An initial approximation to the discrete solution $u$ at the current time step is obtained from the previous time step. This approximation is used to define $P_{j+1/2,i}$ and $P_{i,j+1/2}$ at the midpoints, as above. These coefficients are used in the discretization to form the discrete linear system of equations. The solution of this system is an improved approximation to the solution at the current time step. This procedure is repeated iteratively, producing better and better approximate solutions at the current time step. When a sufficiently good approximation is reached, it is accepted as the numerical solution at the current time step, and the time marching can proceed to the next time step.

The Newton method requires the solution of a linear system of equations at each iteration to produce the improved approximation. It turns out that these linear systems don’t have to be solved exactly. In fact, it is sufficient to solve them approximately, using one iteration of the multigrid linear-system solver in Chapter 17, Section 8. Indeed, because the multigrid method significantly reduces the residual, it provides the required improved approximation.

It also turns out that, with the implicit time marching described above, it is sufficient to use one time step only. The numerical solution at time $t = \Delta t$ is already denoised properly and can, hence, serve as the output of the denoising algorithm. This completes the definition of the denoising algorithm for grayscale images. In what follows, the algorithm is also extended to color images.

# 10.6 Color Images

So far, we have dealt with grayscale images, in which each pixel contains a single number to indicate the amount of light at the corresponding point in the actual image. Here, we consider color digital images, in which each pixel contains three numbers to indicate the intensities of the three basic colors at the corresponding point in the color image: red, green, and blue. The combination of these three colors with the intensities specified in the pixel uniquely produces the actual color at the corresponding point in the image. This digital representation is called the RGB code: R for red, G for green, and B for blue.

The color digital image can thus be defined mathematically as the set of three $N_1 N_2$-dimensional vectors: $r$, containing the intensities of the red color in the pixels; $g$, containing the intensities of the green color in the pixels; and $b$, containing the intensities of the blue color in the pixels in the entire image. We refer to the vectors $r$, $g$, and $b$ as color vectors.

In the above form, the color image is ready for mathematical manipulations to make it clearer. In particular, when the vectors $r$, $g$, and $b$ are contaminated with random noise, a denoising algorithm is required to remove it. Fortunately, the above denoising algorithm can