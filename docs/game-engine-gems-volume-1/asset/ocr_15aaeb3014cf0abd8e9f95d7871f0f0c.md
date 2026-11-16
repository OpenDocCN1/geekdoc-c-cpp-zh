# 18.2 A General Ambient Illumination Model

Let us assume that the surfaces are diffuse. According to the rendering equation, the reflected radiance L^r at a shaded point s can be obtained as an integral of directions ω running over the unit hemisphere Ω above the surface:

L^r(\mathbf{s}) = \int_{\Omega} L^{in}(\mathbf{s}, \boldsymbol{\omega}) \frac{a(\mathbf{s})}{\pi} (\mathbf{N}_s \cdot \boldsymbol{\omega}) d\boldsymbol{\omega} .

where a is the albedo of the diffuse surface, N_s is the unit normal at the shaded point, and L^{in}(\mathbf{s}, \boldsymbol{\omega}) is the incident radiance of the shaded point from direction \boldsymbol{\omega}.

If an occluder point o is visible from s in the direction \boldsymbol{\omega} (see Figure 18.1) and the space is not filled with participating media, then the incident radiance is equal to exiting radiance L^r(o). If no surface is seen, then shaded point s is said to be open in this direction, and the incident radiance is ambient intensity L^a. However, this does not meet our intuition and everyday experience that the effect of distant surfaces is replaced by their average. This experience is due to the fact that the actual space is not empty but is filled with a participating medium. If its extinction coefficient is \sigma and its albedo is 1, then the radiance along a ray of direction \boldsymbol{\omega} changes according to the volumetric rendering equation

L^{in}(\mathbf{s}, \boldsymbol{\omega}) = e^{-\sigma D} L^r(\mathbf{o}) + (1 - e^{-\sigma D}) L^a ,