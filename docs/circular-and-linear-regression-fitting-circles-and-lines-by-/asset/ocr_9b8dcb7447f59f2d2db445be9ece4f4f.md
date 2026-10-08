![](bbox=[0.41, 0.06, 0.65, 0.21])

*Figure 3.5: A data set for which the objective function has four minima.*

**Example of multiple circle fits.** Let four data points (±1,0) and (0,±1) make a square centered at the origin. We place another $k \geq 4$ points identically at the origin (0,0) to have a total of $n = k+4$ points.

This configuration is invariant under the rotation $\mathscr{R} = \mathscr{R}_{\pi/2}$ through the right angle about the origin. Hence, if a circle $\mathbb{S}$ minimizes $\mathscr{F}$, then by rotating that circle through $\pi/2$, $\pi$, and $3\pi/2$ we get three other circles $\mathscr{R}(\mathbb{S})$, $\mathscr{R}^2(\mathbb{S})$, and $\mathscr{R}^3(\mathbb{S})$ that minimize $\mathscr{F}$ as well. We need to check that $\mathscr{R}(\mathbb{S}) \neq \mathbb{S}$, so that we get truly distinct circles; in addition we will make sure that $\mathbb{S}$ is a circle, not a line. This involves some elementary calculations.

Note that $\mathscr{R}(\mathbb{S}) = \mathbb{S}$ if and only if the circle $\mathbb{S}$ is centered on the origin, so we need to show that such circles cannot minimize $\mathscr{F}$. If a circle has radius $r$ and center at (0,0), then $\mathscr{F} = 4(1-r^2) + kr^2$. The minimum of this function is attained at $r = 4/(k+4)$, and it equals $\mathscr{F}_0 = 4k/(k+4)$. Assuming that $k \geq 4$ we can guarantee that the minimum is $\geq 2$.

Also, the best fitting lines here pass through the origin and give $\mathscr{F}_1 = 2$, as it follows from the material of Chapter 2.

To conclude our argument it is enough to find a circle on which $\mathscr{F} < 2$. Consider the circle passing through three points (0,0), (0,1), and (1,0). It only misses two other points, (−1,0) and (0,−1), and it is easy to see that for this circle $\mathscr{F} < 2$. Since $\mathscr{F}$ takes on values that are less than $\mathscr{F}_1$ and $\mathscr{F}_0$ (whenever $k \geq 4$), the best fit will be a circle (not a line), and that circle will not be centered at the origin. We do not find the best fitting circle, but our argument shows that it is not unique.

Fig. 3.5 illustrates the above example, and Fig. 3.6 plots $\mathscr{F}(a, b)$ where four distinct minima are clearly visible.

**Other examples.** If we change the example replacing the square with a rectangle, then we can obtain $\mathscr{F}$ that has exactly two minima. By replacing the square with a regular $m$-gon and increasing the number of identical points at (0,0) we can construct $\mathscr{F}$ with exactly $m$ minima for any $m \geq 3$. In fact, for $m=3$ the corresponding examples are quite simple; they have been described by Nievergelt [138] and Zellner and Clarkson [196]. One can even find the centers and radii of all the best fitting circles explicitly [138].