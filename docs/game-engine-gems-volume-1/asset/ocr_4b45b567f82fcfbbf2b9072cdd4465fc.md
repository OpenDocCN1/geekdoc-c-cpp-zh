distance R. This allows the consideration of only those occlusions that are nearby, i.e., in the neighborhood sphere of radius R. The particular value of R can be set by the application developer. When we increase this value, shadows due to ambient occlusions get larger and softer.

To define the fuzzy measure that increases from zero to one in [0,R], we can use a simple polynomial

$$\mu\left(D\right)=\left(\frac{D}{R}\right)^\alpha.$$

Using this fuzzy measure, the reflected radiance of the shaded point can be expressed in the following way:

$$L^e(s)=a(s)\left[\frac{R}{\pi}\int_\Omega\mu(D(\mathbf{N},\boldsymbol{\omega}))d\boldsymbol{\omega}+\frac{1}{4}\int_\Omega(1-\mu(D))L^e(\mathbf{N},\boldsymbol{\omega})d\boldsymbol{\omega}\right] = a(s)[L^eO(s)+I(s)].$$

The first term of this expression is the ambient occlusion of the shaded point:

$$O(\mathbf{s})=\frac{1}{\pi}\int_\Omega\mu\left(D(\boldsymbol{\omega})\right)(\mathbf{N}_s\cdot\boldsymbol{\omega})d\boldsymbol{\omega}.$$

The second term is the irradiance due to nearby indirect lighting:

$$I(s)=\frac{1}{\pi}\int_\Omega\left[1-\mu(D(\boldsymbol{\omega}))\right]L^e(\mathbf{N},\boldsymbol{\omega})d\boldsymbol{\omega}.$$

This integral is traced back to the ambient occlusion. Replacing occluder radiance \(L'(\boldsymbol{\omega})\) by the average of surface radiance values in the neighborhood of the shaded point \(\tilde{L}^e(\mathbf{s})\), we can express the irradiance as

$$I(s)\approx\frac{1}{\pi}\int_\Omega\left[1-\mu(D(\boldsymbol{\omega}))\right]\tilde{L}^e(\mathbf{s})(\mathbf{N}\cdot\boldsymbol{\omega})d\boldsymbol{\omega}=\tilde{L}^e(\mathbf{s})(1-O(s)).$$