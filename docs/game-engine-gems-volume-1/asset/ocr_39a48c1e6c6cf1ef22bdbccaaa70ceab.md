the cone at a height $z$ above the base. We can calculate the total mass of the cone by integrating elliptical disk areas over the entire height of the cone:

(14.28) \( m = \rho \int_0^h a(z)b(z)dz = \rho \frac{a_0 b_0}{h^2} \int_0^h (h-z)^2 dz = \frac{\pi}{3} \rho a_0 b_0 h. \)

The center of mass clearly lies on the z-axis, and we can calculate its z-coordinate by multiplying a factor of z into the integrand for the mass to obtain

(14.29) \( m C_z = \rho \frac{a_0 b_0}{h^2} \int_0^h (h-z)^2 z dz = \frac{\pi}{12} \rho a_0 b_0 h^2. \)

After dividing by $m$, we find the center of mass to be located at the point $(0,0,h/4)$. 

It is no coincidence that the centers of mass for the pyramid and cone are equal. The same point is obtained for any two-dimensional base shape that linearly tapers to a point at a height $h$. To calculate the moments of inertia in a coordinate system having the origin at the center of mass, we again redefine the functions $a(z)$ and $b(z)$ as in Equation (14.25) and integrate from $-h/4$ to $3h/4$. The moments of inertia are then given by the integrals

(14.30) \(\begin{aligned} I_{11} &= \rho \int_{-3h/4}^{3h/4} \int_{-a(z)}^{a(z)} \int_{-b(z)\sqrt{1-(y/a)^2}}^{b(z)\sqrt{1-(y/a)^2}} (y^2+z^2) dx dy dz = \pi \rho a_0 b_0 h \left( \frac{1}{20} \frac{b_0^2}{h^2} + \frac{1}{80} h^2 \right), \\ I_{22} &= \rho \int_{-3h/4}^{3h/4} \int_{-a(z)}^{a(z)} \int_{-b(z)\sqrt{1-(y/a)^2}}^{b(z)\sqrt{1-(y/a)^2}} (x^2+z^2) dx dy dz = \pi \rho a_0 b_0 h \left( \frac{1}{20} \frac{a_0^2}{h^2} + \frac{1}{80} h^2 \right), \\ I_{33} &= \rho \int_{-3h/4}^{3h/4} \int_{-a(z)}^{a(z)} \int_{-b(z)\sqrt{1-(y/a)^2}}^{b(z)\sqrt{1-(y/a)^2}} (x^2+y^2) dx dy dz = \frac{\pi}{20} \rho a_0 b_0 h (a_0^2 + b_0^2). \end{aligned}\)

Substituting the mass $m$, this gives us the inertia tensor