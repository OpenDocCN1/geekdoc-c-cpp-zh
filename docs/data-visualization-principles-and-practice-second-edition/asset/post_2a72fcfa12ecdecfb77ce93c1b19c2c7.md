
![](img/1274306e378c42ed8a0ad5669902d2a1_233_0.png)

Figure 6.22. Stream tubes in a 3D vector field (a). Corresponding stream surface (b) and zoomed-in surface detail showing tears in the stream surface (c).

from each point $x$ of the discretization of $\Omega$, a streamline $S$ is traced backwards in the vector field. If $S$ hits $\partial\Omega$ at some point $y$ after a given amount of time, the value $f(y)$ is assigned to all points along it in $\Omega$. After all points of $\Omega$ have been thus visited, we obtain a scalar field $f_\Omega : \Omega \rightarrow \mathbb{R}$. Next, the desired stream surface corresponding to $\Gamma$ can be easily extracted as an isosurface of $f_\Omega$ corresponding to the value that $\Gamma$ takes over $\partial\Omega$, using for example the marching cubes algorithm (Section 5.3.2). Although this method is simple to implement, and delivers at once a family of stream surfaces for different isovalues rather than a single such surface, it cannot extract stream surfaces which do not pass through the boundary of the dataset.

### 6.5.6 Streak Surfaces

For time-dependent vector fields, streak surfaces generalize the notion of streaklines in the same way that stream surfaces generalize the notion of streamlines. Given a seed curve $\Gamma$, a streak surface $S_\Gamma$ is a surface that contains all massless particles that pass through $\Gamma$ at different time moments, or, in other words, the (time-dependent) locus of dye advected in the flow that originates at $\Gamma$.

Conceptually, streak surfaces can be computed using a similar approach to stream surfaces: Streaklines are traced in the flow starting from a densely sampled representation of the seed curve \(\Gamma\). The streak surface is then constructed by connecting streamlines for adjacent seeds to yield a quad mesh. However, apart from the additional challenges posed by highly divergent and/or convergent flow regions already outlined for stream surfaces, streak surfaces add the complexity that each surface sampling point needs to be integrated, or advected, at each time step as the vector field changes. This is computationally much more demanding than tracing stream surfaces for time-independent vector fields. Additionally, due to the high dynamics of streak surfaces, the sampling problems due to vector field convergence or divergence can occur at any point on the surface, rather than around the advancing front represented by the end points of the traced streamlines, as is the case for stream surfaces. This requires additional care in the generation of the mesh representing the streak surface. These challenges make streak surface implementations to be less frequently found in flow visualization software.

![](img/1274306e378c42ed8a0ad5669902d2a1_234_0.png)

Figure 6.23. Streak surface in a 3D vector field describing fluid flow around an obstacle. (Image courtesy of R. Laramee, University of Swansea, UK.)

A relatively simple-to-implement algorithm for constructing streak surfaces as quad meshes from a set of streamlines, including the robust handling of highly divergent and convergent flow regions to generate a good quality mesh, is presented in [McLoughlin et al. 10]. Figure 6.23 shows a streak surface computed with this method, drawn from a seed line \(\Gamma\) in a time-dependent flow. The surface is colored by the velocity field magnitude using a rainbow colormap. As visible, the method can accommodate the computation of the complex emerging surface that exhibits tearing as the flow moves around the obstacle.

## 6.6 Texture-Based Vector Visualization

So far, most of the presented vector visualizations used discrete objects, such as vector glyphs, streamlines, or stream surfaces. By their very nature, discrete visualizations cannot convey information about every point of a given dataset domain, as we have seen on several occasions. The interpolation of attributes between these discrete objects must be done visually by the user. In contrast, dense visualizations such as color plots present the user with a (piecewise) continuous signal that can be easier to interpret. The question arises how we can do this for vector fields.

Texture-based visualizations are an answer. The idea is to create a texture signal that encodes the direction and magnitude of a vector field in the various texture parameters such as luminance, graininess, color, and pattern structure. The main challenge here is how to encode the vector direction in the texture parameters. An intuitive and effective idea is to use the texture graininess for this. Since their appearance at the beginning of the 1990s [van Wijk 91, Cabral and Leedom 93], several methods have used this principle to produce visualizations of vector fields.

Line integral convolution. To understand the basic principle, consider an input texture N consisting of small-scale black-and-white noise defined over the domain of the 2D vector field we want to visualize (see Figure 6.24). For each pixel p of this domain, we trace a streamline S(p, s) upstream and downstream through p for some maximal distance L. Here, s parameterizes the streamline. Next, we set the value T(p) of the output texture T at the current location p to be the weighted sum of the values of the input texture N measured along the streamline S(p) that passes through p. As a weighting function k(s) : R -> R+, we can use a Gaussian k(s) = e^-s^2, or other functions that are 1 at the origin and decay smoothly and symmetrically from the origin until they reach near-zero values at the maximal distance L.

The obtained value T(p) is

$$T(p) = \frac{\int_{-L}^{L} N(S(p,s))k(s)ds}{\int_{-L}^{L} k(s)ds}.$$ (6.14)

![](img/1274306e378c42ed8a0ad5669902d2a1_236_0.png)

Figure 6.24. Line integral convolution principle. The color T(p) of pixel p is given by integrating the colors of a noise texture N along the streamline S(p,s) passing through p. The red color intensity along s shows the magnitude of the weight function k(s).

The denominator in Equation (6.14) normalizes the weight factors for an arbitrary value of L.

Intuitively, we can think of this process as blurring, or filtering, the noise image along the streamlines with a set of filters k(s) that are aligned with the streamlines. As we shall see in Chapter 9, the filtering operation described by Equation (6.14) can be seen as a convolution of the noise and filter functions N and k. Hence, this process is also known in the visualization field as line integral convolution (LIC) [Cabral and Leedom 93, Rezk-Salama et al. 99].

If we apply Equation (6.14) for all pixels using streamline lengths L of several tens of pixels, we obtain a texture T whose pixel colors exhibit little variation along a streamline, due to the strong blurring, but show strong variation between neighboring streamlines, due to the similar strong variation of the initial noise. Although they can be used for any vector field, texture-based vector visualization methods have been mainly developed in the context of visualizing vector fields describing fluid flows.

Figure 6.25 shows the results of applying the line integral convolution algorithm described above to a simple synthetic vector field.5 The left image shows the noise texture N used. The right image shows the resulting LIC texture T for an integration length L equal to 5 of the domain size. Using smaller values for L creates textures increasingly similar to the input noise. Using larger values for L increases the length of the perceived snake-like texture patterns.

In addition to the LIC algorithm, many other algorithms use textures to visualize vector fields. Many of them generate similar textures to the LIC method,

![](img/1274306e378c42ed8a0ad5669902d2a1_237_0.png)

Figure 6.25. Line integral convolution visualization. (a) Input noise. (b) The resulting LIC texture.

which are coherent along various types of flow lines, such as streamlines or streaklines, and show a high noise-like variation between neighboring flow lines. This basic principle set aside, the specific algorithms differ in many respects, such as the type of vector field they can depict (stationary or time-dependent), the dimension of the depicted domain (planar, curved surface embedded in 3D, or volumetric), whether they generate a still or an animated texture, and the actual implementation used to create the texture. We point the interested reader to a survey article on this topic [Laramee et al. 04].

### 6.6.1 IBFV Method

A particularly attractive algorithm for texture-based vector visualization is the Image Based Flow Visualization method, or IBFV [van Wijk 02a]. IBFV and its variants [van Wijk 03, Telea and van Wijk 03] produce not just static, but animated, flow textures in real time, can handle both stationary and instationary fields defined on domains ranging from planar 2D to volumetric ones, and are quite simple to implement.

We next detail the IBFV method that operates on 2D planar domains, which is also the simplest to implement in its class. The principle of the method is sketched in Figure 6.26. To understand IBFV, consider a time-dependent scalar property \( I : D \times \mathbb{R}_+ \rightarrow \mathbb{R}_+ \) such as the image intensity, defined on a 2D domain
