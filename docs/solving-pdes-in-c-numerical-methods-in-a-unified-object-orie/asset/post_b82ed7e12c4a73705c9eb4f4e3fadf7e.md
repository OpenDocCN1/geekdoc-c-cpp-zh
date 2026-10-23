
This system is solved by Newton’s iteration (Section 9.16). The initial guess is obtained from the previous time step and used to calculate \(E\) and linearize the equations. This produces three independent linear systems for the color vectors \(\mathbf r\), \(\mathbf g\), and \(\mathbf b\) at the current time step. Each of these linear systems is solved approximately by one multigrid iteration (Chapter 17, Section 8). Once Newton’s iteration terminates, its result is accepted as the numerical solution at the current time step, and the process is ready to proceed to the next time step.

Actually, it turns out that one time step is sufficient; that is, \(T = \Delta t\) provides the required denoised color vectors, which combine to the required denoised color image.

The parameter \(\eta\) may change from one Newton iteration to the next. Because it estimates the total variation in the image (which decreases as the image gets denoised), it should also decrease. A possible way to define \(\eta\) is
\[
\eta = h_x h_y\left(\|\mathbf r_x\|^2 + \|\mathbf r_y\|^2 + \|\mathbf g_x\|^2 + \|\mathbf g_y\|^2 + \|\mathbf b_x\|^2 + \|\mathbf b_y\|^2\right).
\]
where the vectors \(\mathbf r\), \(\mathbf g\), and \(\mathbf b\) are taken from the previous Newton iteration and their partial derivatives are approximated by divided forward differences, and the \(\|\cdot\|^2\) function stands for the sum of the squares over the entire grid. This completes the definition of the denoising algorithm for RGB color images.

## 10.8 Numerical Examples

In this section, we apply the denoising algorithms to realistic examples. For this purpose, we first use a \(512 \times 512\) original grayscale image of Lena, an image that is commonly used in tests in image processing. We add to each pixel in the original image a uniformly distributed random noise with magnitude of at most 25% of the maximum intensity in the original image. The noisy image is displayed in Figure 10.1. To this image, we apply the denoising algorithm for grayscale images, with \(L_x = L_y = 1\) (unit square), \(N_x = N_y = 512\), \(h_x = h_y = 1/512\), and \(\Delta t = 0.000025\). We use 10 Newton iterations, with \(\eta = 10000\) in the first two iterations (where the variation is particularly large due to the initial noise), \(\eta = 1000\) in the next three iterations, and \(\eta = 100\) in the final five iterations (where the noise has already been reduced, and the variation is rather small). The denoised image is displayed in Figure 10.2.

A similar test is also employed for the RGB color image of Lena. In this case, the random noise is added to every color in every pixel. The noisy image is displayed in Figure 10.3. To this image, we apply the denoising algorithm for color images. Again, 10 Newton iterations are used, with \(\eta\) as at the end of Section 10.7. The denoised image is displayed in Figure 10.4.

The denoising algorithms provide good denoising, with almost no blur. The algorithms may yet improve by using smaller \(\Delta t\) or more Newton iterations with clever choices of \(\eta\) or by switching to the more accurate semi-implicit scheme.

For comparison, we also test the Wiener filter available in the MATLAB library, applied separately to each color vector in the noisy image. This filter is based on the statistical characteristics of the input image. At each pixel, the new value is calculated as a weighted average of values in a subsquare of 10 pixels by 10 pixels around it. (This size of subsquare is the minimal size required to remove some noise in the present example.) The result of this filter is displayed in Figure 10.5. It is easy to see that this result contains much more blur than the result of the present denoising algorithm.

## 10.9 Object Segmentation

Another interesting problem in image processing is object segmentation, namely, detecting objects in the digital image. This problem is closely related to the denoising problem, and has important applications in medicine and other areas as well.

Unlike in the denoising problem, here the original good image is available. Assume for simplicity that this is a noncolor (grayscale) image. Let \(\bar I(x, y)\) be a function that agrees with the original image at the grid of pixels. In fact, the definition of \(\bar I(x, y)\) is similar to that of \(u_0(x, y)\) in Section 10.3, except that it uses a good rather than a noisy image.

The linear PDE that provides the solution to the object-segmentation problem is
\[
u_t(t,x,y) - \left(P(x,y)u_x(t,x,y)\right)_x - \left(P(x,y)u_y(t,x,y)\right)_y = g(t,x,y)
\]
in the time-space domain
\[
0 < t < T,\qquad 0 \le x \le L_x,\qquad 0 \le y \le L_y,
\]
where \(g\) is a right-hand-side function to be specified later, and the diffusion coefficient \(P\) is the function defined by
\[
P(x,y) \equiv \frac{1}{1 + \eta^{-1}\left(\bar I_x^2(x,y) + \bar I_y^2(x,y)\right)}.
\]

Because \(P\) is independent of the solution \(u\), this PDE is actually linear. Therefore, one Newton iteration is sufficient for convergence in each time step in the implicit time marching. As a matter of fact, even this single iteration doesn’t have to be exact: it is good enough to reduce the \(\ell_2\)-norm of the residual by one order of magnitude using up to three multigrid iterations (Chapter 17, Section 8).

In our numerical example, we have used \(L_x = L_y = 1\), \(N_x = N_y = 512\), \(\Delta t = 0.000025\), and \(\eta = 100\). The initial-condition function looks like an inverse pyramid:
\[
u(0,x,y) = -\min\bigl(\min(x, 1-x), \min(y, 1-y)\bigr).
\]
Clearly, this is a negative function in the interior of the unit square \((0,1)^2\), which vanishes at its boundary. The set of points at which \(u\) vanishes forms the contour that will eventually segment the required object in the image.

At the initial time \(t=0\), the set of points at which \(u(0,x,y)\) vanishes is the boundary of the unit square. This is a rather poor approximation to the object in the image. Fortunately, as \(t\) grows, the contour formed by the points at which \(u(t,x,y)\) vanishes becomes a better and better approximation to the object in the image.

In order to make the contour approach the object in the image, we must use (at least for small \(t\)) a positive right-hand-side function \(g\) (the so-called “balloon” force [18]). Indeed, a positive external force \(g\) will increase the value of \(u\) as \(t\) grows, making the contour smaller and smaller around the required object in the image.

In our example, we use
\[
g(t,x,y) = \begin{cases} 1000\,P(x,y), & t \le 20\Delta t, \\ 0, & t > 20\Delta t. \end{cases}
\]
In other words, \(g\) is proportional to the diffusion coefficient \(P\) in the first 20 time steps, to get the contour to shrink and approach the object in the image. At further time steps, on the other hand, it is assumed that the contour has already shrunk sufficiently: in order to get it to approximate the object in the image with a yet greater accuracy, \(g\) must vanish. In the present example, we use 30 more time steps with vanishing \(g\).

The linear system obtained in each time step in the implicit time marching is solved approximately by three multigrid iterations (in the first 20 time steps) or by one multigrid iteration (in the next 30 time steps). The solution at the final time step is then interpolated smoothly into a yet finer grid of pixels (see Chapter 27 in [69]), and the final contour is the set of points at which this solution vanishes. For example, the final contour displayed in Figure 10.6 gives a rather good segmentation to the face, hair, and hat of the well-known model Lena.

## 10.10 Denoising in a Curved Surface

Denoising is relevant not only in digital images but also in noisy curved surfaces obtained, e.g., from laser scanning. In this case, the task is to find the accurate surface from noisy data about it. More precisely, one has to find the exact location of the nodes in the discrete mesh that approximates the surface well, using their rough estimates only. More specifically, one has only a noisy datum of the form \(\bar{\mathbf x}_j\) for each node \(j\) that lies on the unknown surface in the three-dimensional Cartesian space. Thus, the accurate location of the node \(j\) is unknown; all one can hope for is to have a better approximation for it by denoising the noisy datum \(\bar{\mathbf x}_j\).

Thus, in this case, \(\mathbf x_j\) can be thought of as the unknown vector function that needs to be discovered from the original noisy data \(\bar{\mathbf x}_j\). To be consistent with the notations in Section 10.7 above, let us denote
\[
\mathbf x_j \equiv (r_j, g_j, b_j),
\]
where \(r_j\) is the \(x\)-coordinate of \(\mathbf x_j\), \(g_j\) is the \(y\)-coordinate of \(\mathbf x_j\), and \(b_j\) is the \(z\)-coordinate of \(\mathbf x_j\). To solve for \(\mathbf x_j\) and have the mesh that approximates the surface well, one must solve a nonlinear diffusion system as in Section 10.7. Here, however, instead of a fixed rectangular grid of pixels, one solves on an unstructured mesh of triangles (or a triangulation) that may move in each iteration until it converges to the required surface.
