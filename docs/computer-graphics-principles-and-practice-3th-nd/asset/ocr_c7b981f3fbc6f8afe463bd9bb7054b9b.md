limiting us to those points that lie on surfaces—we define radiance at \((P,\omega)\) for a nonsurface point \(P\) by letting \(Q=R(P,-\omega)\), and setting

\[L(P,\omega)=L^{\mathrm{out}}(Q,\omega),\tag{29.13}\]

which results in a function that’s constant along rays in empty space. In Equation 29.13, we defined \(L(P,\omega)\) rather than \(L^{\mathrm{in}}\) or \(L^{\mathrm{out}}\) because at points of empty space, these two functions agree; they only differ at points of \(\mathcal{M}\).

The rendering equation now becomes

\[L^{\mathrm{out}}(P,\omega_o)=L^e(P,\omega_o)+\int_{\omega_i\in S^2(P)} L^{\mathrm{in}}(P,-\omega_i)f_s(P,\omega_i,\omega_o)|\omega_i\cdot\mathbf{n}_P|\,d\omega_i.\tag{29.14}\]

The changes we’ve made to incorporate transmission seem fussy and likely to lead to code with multiple cases. In practice, however, they have almost no effect. That’s partly because of the restricted model of scattering we use in representing materials in Chapter 32: Scattering at a surface point consists of a small number of impulses and an otherwise diffuse or glossy reflectance-scattering pattern. (Recall that an impulse is a phenomenon that is similar to mirror reflection or Snell-Fresnel refraction, where radiance arriving along one ray scatters out along just one or two other rays.) In particular, in the general rendering equation, the part of the integral representing transmission degenerates to something far simpler: We look at the radiance arriving along one particular ray, multiply it by a constant representing how much light is transmitted, and add the result to the outgoing radiance.

# 29.4.1 The Measurement Equation

Typically a renderer takes a scene description as input, and produces an image—a rectangular array of values—as output. These values might just be RGB triples in some fixed range, or they might be RGB radiance values representing radiance in W m⁻² sr⁻¹, or something else. In general, a particular pixel value represents the result of a *measurement* process. For a typical digital camera, the red measurement, for one pixel, represents the total charge accumulated in one cell of a CCD device. For a synthetic camera, it might represent the integral of irradiance in the red portion of the spectrum over the rectangular corresponding to one pixel on the image plane. Or it might represent a weighted integral of this irradiance over a disk slightly *larger* than the rectangle usually associated to a pixel so that radiance along a single ray contributes to the value of more than one pixel in the final image. We express this idea by associating to each pixel \(ij\) a **sensor response** \(M_{ij}\), which converts radiance along any ray into a numerical value that can be summed over all rays to get the sensor value. That is to say, we posit that the measurement \(m_{ij}\) associated to pixel \(ij\) is computed as

\[m_{ij}=\int_{U\times S^2} M_{ij}(P,\omega)L^{\mathrm{in}}(P,-\omega)|\omega\cdot\mathbf{n}_P|\,dP\,d\omega,\tag{29.15}\]

where \(U\) is the image plane. This is a purely formal description of the measurement process. The critical thing is that \(M_{ij}\) is zero except for points in a small area and directions in a small solid angle. For a camera with a small pinhole aperture, for instance, \(M_{ij}(P,\omega)\) is nonzero only if both of the following are true.