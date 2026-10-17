The $1/r$ drop-off in the *imaginary part* of $K$ can be explained by the linear Lambertian model of shading, with oblique lighting conditions. Recall that Lambertian shading predicts that pixel intensity is given by

$$i(x,y) \propto \vec{n}(x,y) \cdot \vec{L}$$

where $\vec{n}(x,y)$ is the unit surface normal at point $(x,y)$, and $\vec{L}$ is the unit lighting direction. The linear Lambertian model is obtained by taking only the linear terms of the Taylor series of the Lambertian reflectance equation. Under this model, if constant albedo and illumination conditions are assumed, and lighting is from above, then $i(x,y)=a\,\partial z/\partial y$, where $a$ is some constant. In the Fourier domain, $I(u,v)=a2\pi jvZ(u,v)$, where $j=\sqrt{-1}$. Thus, we have that

$$ZI^*(r,\theta)=-\frac{j}{a2\pi r\sin(\theta)}\,II^*(r,\theta)$$

$$K(r,\theta)=-j\frac{1}{r}\frac{1}{a2\pi\sin(\theta)}$$

Thus, Lambertian shading predicts that $imag[ZI^*]$ should obey a power law, with $\alpha_{imag[ZI^*]}$ being one more than $\alpha_{imag[II^*]}$, which is consistent with the findings in Table 1.1.

Equation (1.4) predicts that only the imaginary part of $ZI^*$ should obey a power law, and the real part of $ZI^*$ should be zero. Yet, in our databases, the real part of $ZI^*$ was typically stronger than the imaginary part. The real part of $ZI^*$ is the Fourier transform of the even-symmetric part of the cross-correlation function, and it includes the direct correlation $\operatorname{cov}[i,z]$, corresponding to the da Vinci correlation between intensity pixel and range pixel discussed earlier. The form of $real[ZI^*]$ is related to the rate at which the da Vinci correlation drops off over space. One explanation for the $1/r^3$ drop-off rate of $real[ZI^*]$ is the observation that deeper crevices and concavities should be more shadowed and therefore darker than shallow concavities. Specifically, the $1/r^2$ drop-off rate of $real[ZI^*]$ predicts that the correlation between nearness and brightness should be inversely proportional to the aperture width it is measured over. This matches our intuition that given two surface concavities with equal depths, the one with the narrower aperture should be darkest.

Figure 1.4 shows examples of $B_K$ in urban and rural scenes. These plots illustrate that the real part of $B_K$ is strongest (most negative) for rural scenes with abundant concavities and shadows. These figures also illustrate how