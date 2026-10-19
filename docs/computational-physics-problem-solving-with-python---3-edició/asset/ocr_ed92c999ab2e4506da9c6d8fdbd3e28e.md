local charge density. As an algorithm, (19.31) does not provide a direct solution to Poisson’s equation, but rather must be repeated many times to converge upon the solution. We start with an initial guess for the potential, improve it by sweeping through all space taking the average over nearest neighbors at each node, and keep repeating the process until the solution no longer changes to some level of precision or until failure is evident. When converged, the initial guess is said to have relaxed into the solution.

A reasonable question with this simple an approach is, “Does it always converge, and if so, does it converge fast enough to be useful?” In some sense, the answer to the first question is not an issue; if the method does not converge, then we will know it; otherwise we have ended up with a solution and the path we followed to get there is no body’s business! The answer to the question of speed is that relaxation methods may converge slowly (although still faster than a Fourier series), yet we will show you two clever tricks to accelerate the convergence.

At this point, it is important to remember that our algorithm arose from expressing the Laplacian ∇² in rectangular coordinates. While this does not restrict us from solving problems with circular symmetry, there may be geometries where it is better to develop an algorithm based on expressing the Laplacian in cylindrical or spherical coordinates in order to have grids that fit the geometry better.

# 19.4.1

# Relaxation and Over-relaxation

There are a number of ways in which algorithm (19.31) can be iterated so as to convert the boundary conditions to a solution. Its most basic form is the Jacobi method and is one in which the potential values are not changed until an entire sweep of applying (19.31) at each point is completed. This maintains the symmetry of the initial guess and boundary conditions. A rather obvious improvement on the Jacobi method utilizes the updated guesses for the potential in (19.31) as soon as they are available. As a case in point, if the sweep starts in the upper left-hand corner of Figure 19.3, then the leftmost U[i −1, j] and topmost U[i,j −1] values of the potential used will be from the present generation of guesses, while the other two values of the potential will be from the previous generation: (Gauss–Seidel method)

U_{i,j}^{(new)} = 1/4 [ U_{i+1,j}^{(old)} + U_{i-1,j}^{(new)} + U_{i,j+1}^{(old)} + U_{i,j-1}^{(new)} ] . (19.32)

This technique, known as the Gauss–Seidel method, usually leads to accelerated convergence, which in turn leads to less round-off error. It also uses less memory as there is no need to store two generations of guesses. However, it does distort the symmetry of the boundary conditions, which one hopes is insignificant when convergence is reached.

A less obvious improvement in the relaxation technique, known as successive over-relaxation (SOR), starts by writing algorithm (19.31) in a form that determines the new values of the potential U^{(new)} as the old values U^{(old)} plus a correc-