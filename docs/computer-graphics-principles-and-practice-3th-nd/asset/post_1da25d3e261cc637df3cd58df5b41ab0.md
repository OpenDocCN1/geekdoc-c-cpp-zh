
$$L^r(P,\omega_o) \approx \frac{\sqrt{2}}{4\pi}\frac{\Phi}{4\pi(r^2)}\int_\Omega d\omega_i + I \tag{29.28}$$

$$= \frac{\sqrt{2}}{4\pi}\frac{\Phi}{4\pi(r^2)}\frac{\pi r^2}{R^2} + I \tag{29.29}$$

$$= \frac{\sqrt{2}}{4\pi}\frac{\Phi}{4\pi R^2} + I. \tag{29.30}$$

Since $R = \sqrt{2}$ and $\Phi = 10$, we get that the reflected radiance is $\frac{5\sqrt{2}}{16\pi^2} + I\ \mathrm{W\ m^{-2}\ sr^{-1}}$. Notice that this approximation of Equation 29.28 is independent of $r$ so that even as the spherical luminaire shrinks to a point, the reflected radiance remains the same.

◈ The constancy of the reflected radiance depends on two things: the assumption that the dot product $\omega_i \cdot n(P)$ can be approximated by $\mathbf{u} \cdot n(P)$, and the fact that the finite portion of the scattering function is constant. The first of these is justified because we’re letting $r$ approach zero. The second is not true for a general BSDF. But if $f_s^0$ is continuous, as it is in all the BSDFs that we consider, then the mean value theorem for integrals tells us that the integral we wish to compute is equal to

$$m(\Omega)\cdot f_s^0(P,\omega_o,\omega_i^*)L(P,-\omega_i^*)(\omega_i^*\cdot n(P)) \tag{29.31}$$

for some $\omega_i^*$ in $\Omega$. As the area of $\Omega$ goes to zero, this vector $\omega_i^*$ must approach $\mathbf{u}$, so the integral approaches

$$\pi(r/R)^2 f_s^0(P,\omega_o,\mathbf{u})L(P,-\mathbf{u})(\mathbf{u}\cdot n(P)). \tag{29.32}$$

To summarize the preceding argument, a point luminaire of power $\Phi$, in direction $\omega_i$ from $P$, at distance $R$, produces reflected radiance (from the nonimpulse portion of scattering) in direction $\omega_o$ in the amount

$$\frac{\Phi}{4\pi R^2} f_s^0(P,\omega_i,\omega_o)\,\omega_i\cdot n_P,\quad \text{for }\omega_i\cdot n_P>0\text{ and }\omega_o\cdot n_P>0. \tag{29.33}$$

Finally, let’s consider the impulse reflection of the very small spherical source. The radiance leaving each point of the luminaire is again $\frac{\Phi}{4\pi(r^2)}$. Because $\omega_i$ points to a point of the luminaire, the radiance arriving in direction $-\omega_i$ is $\frac{\Phi}{4\pi(r^2)}$; to get the outgoing radiance in the mirror-reflected direction $\omega_o$, we multiply by the impulse value 0.3 so that the outgoing radiance due to mirror reflection of the very small spherical source is $0.3\frac{\Phi}{4\pi(r^2)}$. Notice that this depends on the value of $r$! As the size of the luminaire decreases, the radiance emitted must increase to keep the total power the same, with the result that the mirror-reflected radiance also increases without bound. If we try to take a limit, we end up with an answer that includes $\infty$, which is unsatisfactory.

There are several possible ways to address this problem.

- 1. Assert that no eye ray that we trace will ever “just happen” to hit a point luminaire, so this is a probability-zero event, and we can ignore the infinity that would arise if this event happened.
- 2. Say that for the sake of reflecting from diffuse surfaces, point lights are points, but for the sake of specular reflections, they have a nonzero radius $r$, which must be chosen by the user. Note that this makes the world in which we’re trying to simulate light transport internally contradictory.
- 3. Say that point lights are in fact small spheres of a known radius, *r*, but that we’ll restrict our scene to be sure that the distance from a point luminaire to any surface is much greater than *r* so that the diffusely reflected light can be very well approximated by treating the sources as point sources, but mirror-reflected light must be computed using *r*.
- 4. Observe that when we include both point lights and mirror reflections, both of which are approximations of physical phenomena made for convenience, the mathematics becomes intractable, and hence we’ll abandon one or both.

Each of these approaches has its merits, although we prefer approach 3 to approach 2 (even though they both may result in identical programs). In Chapter 32, we choose the first option: We simply ignore mirror-reflected point lights.

## 29.7 Solving the Rendering Equation

It’s natural to ask, having derived the rendering equation, how to solve it. That is to say, if we know the scene geometry and materials and illumination, how can we compute *L(P, ω)* for any point *P* and any vector *ω*, or for every *P* and every *ω*? We’ve already given you a taste of the answer in discussing a path tracer. But the general topic is the subject of the next three chapters. Because integration is central to the rendering equation, the first discusses probability and Monte Carlo integration. The second describes the ideas behind several techniques for solving the rendering equation. The third gives an implementation of two renderers. One of the shocking things is how very short the two programs are, given the length of this chapter and the next three. That brevity is partly due to the use of libraries for things like visibility testing, basic linear algebra, and material representation. But as you’ll see, it’s also due to the simplicity of basic Monte Carlo integration.

## 29.8 The Classification of Light-Transport Paths

In the course of the Monte Carlo integration used to estimate solutions to the rendering equation, we’ll break up the integrals of the rendering equation into different parts—sometimes by breaking up the domain of integration into the categories of “directions in which we see luminaires” and “other directions,” and sometimes by breaking up the integrand into a sum of a finite part and an impulse part, usually as a means of distinguishing between things like point luminaires and area luminaires, or between mirror reflections and diffuse reflections.

Because of this distinction in treatment, it’s useful to be able to discuss the path that light took in getting from the luminaire to the receiver (a **light path**), or its reverse, the path we traced from the eye to eventually reach the light source (an **eye path**). Heckbert [Hec90] used a notation that’s now universally accepted:¹ *L* denotes a luminaire, *E* the “eye,” *S* a specular reflection, and *D* a diffuse reflection. Thus, *LDE* represents light that left the source, scattered from a diffuse surface, and reached the eye. Conventional regular-expression notation is useful here, with + used to indicate “one or more,” * for “zero or more,” ? for “zero or one,” parentheses for grouping, and | for “or,” so that L(D|S)E denotes a one-bounce path from a source to the eye that involves either a diffuse or specular reflection, while LD⁺E is a path involving one or more diffuse bounces.

1\. Hanrahan [JAF⁺01] attributes this notation to Shirley, who claims [Shi10] that he’s uncertain who first used it.

**Inline Exercise 29.1.** (a) Write the notation for light that undergoes one or more diffuse bounces, and then a final specular bounce before reaching the eye. (b) A very basic ray tracer might consider rays from the eye that undergo only repeated specular bounces, followed by zero or one diffuse bounce, before reaching the light. Write the notation for the path traveled by the light, from luminaire to eye.

Note that the notation describes a sequence of scattering events, not just the path. In the case of the half-mirror surface we just discussed, light could travel from a luminaire to the surface, be mirror-reflected, and reach the eye; it could also travel from the source, be diffusely scattered, and reach the eye. The light energy in the two cases travels along the same path, but the first is described by LSE while the second is described by LDE.

There are extensions that are fairly common. Veach uses D to mean Lambertian, G for any kind of glossy reflection, S for perfectly specular, and T for transmission, for instance [Vea97].

We can use this notation to characterize certain rendering algorithms in terms of the eye paths that they consider, following Hanrahan [JAP⁺01]:

- Appel’s ray-casting algorithm: E(D|G)L
- Recursive ray tracing (Whitted): E[S*](D|G)L
- Path tracing (Kajiya): E[(D|G|S)⁺(D|G)]L
- Radiosity: ED*L

Recursive ray tracing considers only light that’s diffusely or glossily reflected, and then mirror-reflected to the eye. Radiosity only handles diffuse reflections. And Appel’s ray-casting algorithm considers only direct lighting.

![](img/f464cd0043eb5336aa0543fe20a0561b_847_0.png)

![](img/f464cd0043eb5336aa0543fe20a0561b_847_1.png)

### 29.8.1 Perceptually Significant Phenomena and Light Transport

We conclude this largely mathematical chapter with a discussion of things we notice when we look at the world, for these phenomena—the things we take the trouble to name—are the things we must render effectively if we want to make compelling images. They thus serve as a guide to developing rendering algorithms.

The first phenomenon is the **shadow**. Figure 29.6 shows a hard shadow, created by a luminaire (the sun) that subtends a very small solid angle. The light from the sun is obstructed by the sharp edge of an object. Figure 29.7 shows a soft shadow. Soft shadows can be caused by many things: If the shadowing object is not sharply defined (e.g., a furry animal), the shadow may have no distinct edge, even if it’s cast by a point luminaire. If the shadow is cast by a very small object, diffraction effects may dominate and effectively soften the shadow. But most often, soft shadowing is caused by nonpoint luminaires: A point on the receiving surface may be

![](img/f464cd0043eb5336aa0543fe20a0561b_847_2.png)
