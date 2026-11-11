
For mathematical convenience, we’re going to consider a scene that is *finite*, in the sense that it’s contained within some sufficiently large sphere around the origin; the interior of this sphere we’ll assume to be coated with a nonreflective material so that all light hitting it is absorbed. In a real scene, once light “leaves” the scene, we ignore it. But for this chapter, it’s very useful to have a ray-casting function that takes a point $P$ and direction $\mathbf{d}$ and returns the first surface point $Q$ along the ray starting at $P$ and going in direction $\mathbf{d}$. If the scene isn’t surrounded by the large sphere, then a ray headed “out of the scene” doesn’t hit anything, and the ray-casting function’s value is not defined. So the large black sphere is completely for mathematical convenience, and it has no impact on the actual transport of light.

To keep the notation simple, we’re going to further assume that we’re studying a steady-state situation, one in which there is no time dependence: The luminaires have all been illuminated for long enough to allow light to scatter throughout the scene and reach a steady state. Furthermore, we’re going to ignore the wavelength dependence, and study just radiance rather than *spectral* radiance.

Thus, our starting point is a collection of surfaces whose union is the set $\mathcal{M}$ of all surface points in the scene (including the large enclosing black sphere). For each point $P \in \mathcal{M}$, we also know $f_r(P, \omega_i, \omega_o)$, the bidirectional reflectance distribution function at $P$, which describes how much light arriving at $P$ traveling in direction $-\omega_i$ becomes light leaving in direction $\omega_o$ (see Chapter 26 for the formal definition). The symbols $\omega_i$ and $\omega_o$ will be reserved, for this section, to be unit vectors that point in the same half-plane as the normal vector $\mathbf{n}_P$ at $P$, that is, $\omega_i \cdot \mathbf{n}_P \ge 0$ and $\omega_o \cdot \mathbf{n}_P \ge 0$.

In addition to the scene geometry and reflectance, we assume that we’re given the **illumination** in the scene, described by the emitted radiance at every point of every luminaire, in every direction; in other words, we’re given a function

$$L^e : \mathcal{M} \times \mathbb{S}^2 \to \mathbb{R} : (P, \omega) \mapsto L^e(P, \omega), \qquad (29.1)$$

where $L^e(P, \omega)$ denotes the *emitted radiance* leaving the point $P$ in direction $\omega$, the radiance you’d measure if every other luminaire and surface in the scene were removed, so that no light at all *arrived* at the point $P$, and hence none was reflected.

> For a typical point $P$ of a typical area luminaire, $L^e(P, \omega)$ is zero if $\omega \cdot \mathbf{n}_P < 0$; in other words, light radiates only toward the “outward” side of the luminaire. For luminaires like typical white incandescent lightbulbs, the radiance in all such outward directions is the same, or $L^e(P, \omega) = C$ for $\omega \cdot \mathbf{n}_P > 0$. Because of the analogy with the light reflected from a Lambertian surface, we’ll refer to such a luminaire as **Lambertian**.

As we said above, we’ll also assume we have a *ray-casting function* (see Figure 29.1),

$$R : \mathcal{M} \times \mathbb{S}^2 \to \mathcal{M}, \qquad (29.2)$$

where $R(P, \omega)$ is the first point hit by a ray starting at $P$ in direction $\omega$. If $\omega \cdot \mathbf{n}_P \le 0$, then $R(P, \omega) = P$, that is, a ray *into* a shape hits the shape immediately. If $\omega \cdot \mathbf{n}_P > 0$, then $R(P, \omega)$ is the point we see by looking in direction $\omega$ from $P$. More precisely, $R(P, \omega)$ is the farthest point $Q$ on the ray from $P$ in direction $\omega$ with the property that all points of the ray strictly between $P$ and $Q$ are in empty space.

![](img/f464cd0043eb5336aa0543fe20a0561b_835_0.png)

*Figure 29.1: $R(P_1, \omega_1) = Q_1$, but $R(P_2, \omega_2) = P_2$.*

The algorithmic representation of the ray-casting function and the associated **visibility function**—see Exercise 29.1—is the subject of Chapters 36 and 37, but you've already seen basic examples in Chapter 15.

With our assumptions clearly characterized, we can now analyze the light transport in our scene.

### 29.2.1 The Rendering Equation, First Version

Consider once again the reflectance equation, Equation 26.80, rewritten without time or wavelength dependence:

$$L^{\text{ref}}(P, \omega_o) = \int_{\omega_i \in \mathbb{S}^2(P)} L(P, -\omega_i) f_r(P, \omega_i, \omega_o) (\omega_i \cdot \mathbf{n}_P) \, d\omega_i, \tag{29.3}$$

This expresses the radiance reflected at point $P$ in *outward* direction $\omega_o$ in terms of the light arriving at $P$ in other directions.

If $P$ happens to be a point of a luminaire, light may also leave $P$ in direction $\omega_o$ because it is *emitted* at $P$ rather than because it is reflected from there; that is,

$$L(P, \omega_o) = L^e(P, \omega_o) + L^{\text{ref}}(P, \omega_o) \tag{29.4}$$

$$= L^e(P, \omega_o) + \int_{\omega_i \in \mathbb{S}^2(P)} L(P, -\omega_i) f_r(P, \omega_i, \omega_o) (\omega_i \cdot \mathbf{n}_P) \, d\omega_i, \tag{29.5}$$

This is a basic version (e.g., it handles only reflection) of the **rendering equation**, which characterizes the function $L$, given the functions $L^e$ and $f_r$. It was first described in computer graphics by Kajiya [Kaj86] and Immel et al. [ICG86], in slightly differing forms. It is completely analogous to similar equations developed in subjects like radiative transfer. While we'll concentrate on Kajiya's description and derivation in subsequent chapters, the form presented by Immel et al. is particularly well suited to the "sampling" needed in Monte Carlo rendering.

You'll notice that the unknown radiance function $L$ appears on both sides of the equation, once under an integral, just as the unknown function $h$ appears on both sides of the differential equation

$$h'(x) = 2h(x - 1), \tag{29.6}$$

once within a derivative. Equation 29.5 is called an **integral equation**, and solving such an equation is generally more difficult than solving a differential equation. The next chapter discusses various approaches to finding approximate solutions.

Equation 29.4 expresses the radiance function $L$, considering both the radiance *leaving* the point $P$ and the radiance arriving there. Arvo [Arv95] calls the first of these the **surface radiance** and the second the **field radiance**. The rendering equation tells us how to compute *surface* radiance from field radiance, because it's restricted to the case where $\omega_o \cdot \mathbf{n}_P > 0$. But to evaluate the right-hand side, we must know how to compute the *field* radiance as well.

The idea that "closes the loop" in this equation is that any light arriving at a point $P$, traveling in direction $-\omega_i$, must have *departed* from some other point $Q \in \mathcal{M}$ traveling in direction $-\omega_i$. The point $Q$ must be the point visible from $P$ in direction $\omega_i$. These observations allow us to write the **transport equation**:

$$L(P, -\omega_i) = L(R(P, \omega_i), -\omega_i), \tag{29.7}$$

for any $\omega_i$ with $\omega_i \cdot \mathbf{n}_P > 0$.

at $P$; and the third all other light. Thus, the term $L(P, -\omega_i)$ in the rendering equation has been split into a sum of three terms.

The first of these terms is computed (see Listing 29.2) by converting the integral over all possible incoming directions into a sum over the point luminaire sources. This change of domain in the integral means we have to alter the integrand as well, using the change of variable from Section 26.6.5.

*Listing 29.2: Reflecting illumination from point lights.*

```cpp
Radiance3 App::estimateDirectLightFromPointLights(Surfel surfel, Ray ray){
    Radiance3 radiance(0.0f);
    for (int L = 0; L < m_world->lightArray.size(); ++L) {
        const GLight& light = m_world->lightArray[L];
        // Shadow rays
        bool visible = m_world->lineOfSight(surfel.geometric.location +
            surfel.geometric.normal * 0.0001f,
            light.position.xyz());
        if (visible) {
            Vector3 w_i = light.position.xyz() - surfel.shading.location;
            const float distance2 = w_i.squaredLength();
            w_i /= sqrt(distance2);
            // Attenuated radiance
            const Irradiance3& E_i = light.color / (4.0f * pif * distance2);
            radiance += (surfel.evaluateBRDF(w_i, -ray.direction()) *
                E_i * max(0.0f, w_i.dot(surfel.shading.normal)));
        }
    }
    return radiance;
}
```

As you can see, the procedure loops through all the point luminaire sources, and for each one, it checks whether the source is *visible* from $P$, using `m_world->lineOfSight()`, the implementation of the visibility function for the world we're rendering. The reflected radiance is computed as a product of the BRDF, the dot product $\omega_i \cdot \mathbf{n}_r$, and a term $E_i$, which is the incoming radiance adjusted by the change-of-variable factor mentioned above.

The second term is similar, involving estimates of how area luminaires are reflected. The third term is the most interesting, however. Before we look at it, we need one more bit of mathematics (which we'll develop extensively in Chapter 30).

The idea is this: The integral of any function $h$ over any domain $D$ is the product of the average value of $h$ on that domain with the size of the domain. When the domain is the interval $[a, b]$, the size is $b - a$; when the domain is a unit hemisphere, the size is $2\pi$, etc. The “average value” can be estimated by evaluating $h$ at $n$ points of the domain and averaging. As $n$ gets large, the estimate gets better and better. But even $n = 1$ works! That is to say, we can estimate the integral of $h$ over the domain $D$ by evaluating $h(x)$ for a randomly chosen point $x \in D$ and multiplying by the size of $D$. The estimate won't generally be very good, but if we repeat the estimation procedure multiple times, the average will be quite a good estimate.

We’ll apply this to the situation where $h$ is the integrand in the reflectance equation, and $D$ is the upper hemisphere. Let’s look at the code (see Listing 29.3).
