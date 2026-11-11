
velocity is the thing that’s easy to work with mathematically, just as it’s possible to measure the distance a car travels over some small time interval, but we work with instantaneous velocity when we’re studying the mathematics of motion. What are the units of \(L\)? Taking as a model “piece of surface” a rectangle in the \(xy\)-plane, and assuming that the light flow is in a set of directions \(\Omega\) all of which are essentially perpendicular to the \(xy\)-plane, we know that

\[\text{energy} \approx \int_{t_0}^{t_1}\int_{x_0}^{x_1}\int_{y_0}^{y_1}\int_{\omega\in\Omega}\int_{\lambda_0}^{\lambda_1} L(t,x,y,0,-\omega,\lambda)\,d\lambda\,d\omega\,dy\,dx\,dt.\qquad (26.39)\]

Note that in the integrand above, \(L\) has four arguments: \(t\), the point \((x,y,0)\), \(-\omega\), and \(\lambda\). The \(\omega\) is negated because \(\omega\) points *out* of the surface, but we want to sum up the light coming *in* to the surface.

Using MKS units for the surface and time, but nanometers for wavelength (which follows long-standing convention), we find that \(L\) must have the units of joules per second per square meter per nanometer per steradian. One joule per second is one watt, so we can also say “watts per square-meter nanometer steradian.”

What happens if the direction \(\omega\) along which light arrives is *not* parallel to the surface normal? Then the amount of light energy arriving at the surface, per unit area, is smaller than if it *were* parallel, by the Tilting principle.

Thus, the more general and exact formula for the energy arriving at that small region of the \(xy\)-plane from directions in the solid angle \(\Omega\), in the given time interval and wavelength interval, is

\[\text{energy} = \int_{t_0}^{t_1}\int_{x_0}^{x_1}\int_{y_0}^{y_1}\int_{\omega\in\Omega}\int_{\lambda_0}^{\lambda_1} L(t,x,y,0,-\omega,\lambda)\,\omega\cdot\mathbf{e}_3\,d\lambda\,d\omega\,dy\,dx\,dt.\qquad (26.40)\]

For a region \(R\) of an arbitrary plane, with normal vector \(\mathbf{n}\), the energy arriving at \(R\) in the interval \(t_0\le t\le t_1\), at wavelengths \(\lambda_0\le\lambda\le\lambda_1\), in directions opposite those in a solid angle \(\Omega\), is

\[\text{energy} = \int_{t_0}^{t_1}\int_{\lambda_0}^{\lambda_1}\int_{P\in R}\int_{\omega\in\Omega} L(t,P,-\omega,\lambda)\,|\omega\cdot\mathbf{n}|\,d\omega\,dP\,d\lambda\,dt,\qquad (26.41)\]

where \(\int_{P\in R}\cdots dP\) is an area integral over the area \(R\).

When we are concerned with overall light energy, rather than caring about how much is transported at each different wavelength, we can integrate \(L\) over all wavelengths \(\lambda\), giving us a new function depending on time, position, and direction, with units of watts per square-meter steradian. This new function is called the **radiance**. This relationship between spectral radiance and radiance is quite general: For any photometric quantity, the spectral version has the wavelength \(\lambda\) as a parameter, while the version without the adjective “spectral” has been integrated over all possible wavelengths.

The function \(L\), defined for all times and points and all directions (and possibly for all wavelengths) describes fully the way light flows around the scene. We’ll call \(L(t,P,\omega)\) or \(L(t,P,\omega,\lambda)\) the “radiance” or “spectral radiance” at time \(t\), location \(P\), etc. But the function \(L\), considered as a whole, is sometimes also called the **plenoptic function**, particularly in computer vision.

### 26.7.1 Radiometric Terms

The spectral radiance \(L\) characterizes the light energy flowing, at each instant, at each point in the world, in each possible direction. Formally its domain is \(\mathbf{R} \times \mathbf{R}^3 \times \mathbf{S}^2 \times \mathbf{R}^+\), where \(\mathbf{S}^2\) denotes the unit sphere in 3-space (the set of all possible directions in which light can flow) and \(\mathbf{R}^+\) is used for the set of all possible wavelengths. In practice, \(\mathbf{R}^+\) may be replaced by the range of wavelengths that are visible. The codomain of \(L\) is \(\mathbf{R}\).

Starting from \(L\), we can describe, via integration, all of the terms conventionally used in **radiometry**, the science of the measurement of radiant energy. An alternative approach is to start from energy or power, and define all the terms by differentiation. We discuss this approach briefly in Section 26.9.

### 26.7.2 Radiance

Spectral radiance is the quantity described by \(L\); radiance is the quantity \(\displaystyle \int_0^{\infty} L(t, P, \omega, \lambda)\,d\lambda,\qquad (26.42)\), which is defined for \((t, P, \omega) \in \mathbf{R} \times \mathbf{R}^3 \times \mathbf{S}^2\). In engineering, the letter \(L\) is usually used for this quantity, with \(L_\lambda\) being reserved for spectral radiance; in graphics, however, the spectral radiance is often denoted by \(L\). Because for us the symbol \(\lambda\) actually is one of the arguments to the function, it’s a bad choice for a subscript. We’ll therefore carry out the remainder of this discussion in the spectral case (keeping \(\lambda\) as an argument), and discuss the nonspectral case at the end. Until then, when we speak of radiance we’ll be speaking of spectral radiance; when we speak of irradiance we’ll mean spectral irradiance, etc.

The most interesting thing about radiance, from a computer graphics point of view, is that in a steady-state situation, that is, one in which \(L\) is independent of \(t\), radiance is constant along rays in empty space (assuming, for the moment, that there are no point light sources; see Exercise 26.3). In mathematical terms, this means that the function \(L\) cannot be just any function. We also know, from physical considerations, that \(L\) can never be negative.

Why is \(L\) constant along rays in empty space? Try an experiment (see Figure 26.25): Look through a narrow cardboard tube at a tiny region of a well-lit latex-painted wall. You’ll see a small disk of light at the end of the tube, outlined in red in the figure. Now move the tube as far away from the wall, and look again at the same region. Again, you’ll see a small disk of light (outlined by the larger blue circle), and it will appear equally bright (assuming that the wall is about equally well lit over the region where you’re looking). There’s an easy explanation for this: When at first you were at distance \(r\) from the wall, light leaving the wall spread out to illuminate a hemisphere of radius \(r\); when you move to distance \(2r\), it’s illuminating a hemisphere of radius \(2r\), whose area is four times as great. But as you look through your tube, you see four times as large a region of the wall. Hence the total energy coming down the tube toward your eye is constant. In each case, the light energy passing through the eye end of the tube is approximately the integral of the radiance over the region of the tube end. Because we’re assuming the wall is uniformly lit, this is just the (approximately constant) radiance times the area of the tube end times the solid angle subtended at the eye by the far end of the tube. The fact that things look the same means that the radiance has not changed as you moved along the ray from the wall to your initial eye point.

![](img/f464cd0043eb5336aa0543fe20a0561b_744_0.png)

*Figure 26.25: A radiance measurement tool.*

To the degree that the pixel area on the sensor in a digital camera can be regarded as infinitesimal (or that the variation of radiance with position on the sensor can be assumed small) and the solid angle of rays that hit that pixel can be considered infinitesimal (or the variation with direction assumed small), the response of the sensor (assuming it responds to total arriving energy) is proportional to radiance. In fact, high-quality cameras used for computer vision experiments produce images whose individual entries are radiance values. To be more precise, the values they produce are often integrals, with respect to wavelength, of spectral radiance multiplied by a response function that characterizes how the sensor responds to radiance of each wavelength.

### 26.7.3 Two Radiance Computations

For a **Lambertian emitter**, the radiance in all outgoing directions is the same. Let’s suppose that we have a Lambertian emitting sphere S of radius r, emitting total power Φ. We’ll now compute the radiance along each ray leaving the sphere. The idea (see Figure 26.26) is to surround the emitter with a concentric sphere S′ of radius R >> r. All power emitted from S must arrive at S′, and the arriving power density (in W m⁻²) on S′ is independent of position. If we call this density D, then

\[4\pi R^2 D = \Phi. \tag{26.43}\]

![](img/f464cd0043eb5336aa0543fe20a0561b_745_0.png)

We’ll compute the power density at the point P in terms of the unknown constant emitted radiance L, which will allow us to solve for L in terms of Φ. The power density at P is

\[\begin{aligned}
D &= \int_{S^2(P)} L\,|\omega \cdot \mathbf{n}(P)|\,d\omega \tag{26.44}\\
&= \int_{\Omega} L\,|\omega \cdot \mathbf{n}(P)|\,d\omega \tag{26.45}\\
&= L\int_{\Omega} |\omega \cdot \mathbf{n}(P)|\,d\omega. \tag{26.46}
\end{aligned}\]

The transition between Equations 26.44 and 26.45 is justified by noting that for ω outside Ω, the radiance at P in direction −ω is zero, so the integral over the whole hemisphere can be reduced to an integral over just Ω.

For sufficiently large values of R, ω · n(P) is very close to 1, so in the limit as R approaches infinity, we get

\[D = L\int_{\Omega} 1\,d\omega = L\,m(\Omega). \tag{26.47}\]

![](img/f464cd0043eb5336aa0543fe20a0561b_745_1.png)

The sphere of radius R around P (drawn in light gray in Figure 26.27) has total area 4πR², and subtends a solid angle of 4π at P; of this 4πR² area, an area of approximately πr² is occupied by the radiating sphere (i.e., as seen from P, the radiating sphere occludes a disk of area πr² in the entire 4πR²). The solid angle
