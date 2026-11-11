
*Listing 32.19: Using final gathering to improve the estimate of indirect radiance arriving at a point.*

```cpp
Radiance3 App::estimateDiffuselyReflectedIndirectLight(..., boolean useGather)
    // estimate arriving radiance at "surfel" with final gather.
    Radiance3 L(0.0f);

    if (!useGather)
        ... use the previous photon-mapping code ...
    else {
        for (int i = 0; i < m_gatherRaysPerSample; ++i) {
            // draw a cosine-weighted sample direction from the surface point
            Vector3 w_i = -n.direction();
            Vector3 w_o = Vector3::cosineHemisphereRandom(surfel.geometric.normal, rnd);
            Ray gatherRay = Ray(surfel.geometric.location, w_o).bumpedRay(...);

            Color3 coeff;
            L += π * surfel.evaluateBSDF(w_i, w_o, f_inf()) *
                estimateTotalScatteredRadiance(gatherRay, depth+1, false);
        }
    }
    return L / m_gatherRaysPerSample;
}
```

The improvement in results is dramatic, at least if we’re willing to use a large number of rays in our final gathering. If we’re typically averaging contributions from 20 nearby photons in the nongather version of the code, we should be using at least 20 gather rays to estimate the radiance in the gather version. Figure 32.15 shows the effect of the final gather.

![](img/f464cd0043eb5336aa0543fe20a0561b_964_0.png)

Figure 32.15: Final gathering with 30 samples in our first three test scenes. The photon maps were generated with 10,000 shot photons, resulting in 1,100 photons (first scene) to 7,900 photons (second scene). The last image is the Cornell box, rendered with the same parameters but no final gather. The improvement is substantial.

### 32.7 Generalizations

Because photon mapping provides a consistent estimate of reflected indirect radiance, we can take any rendering algorithm that needs such an estimate (ray tracing, path tracing) and replace its estimator with a photon-mapping implementation. A similar argument allows one to replace direct evaluation by a final-gather step. Similarly, if it’s possible to break up the rendering integral into various pieces (as we did for impulse-scattered indirect light, diffusely scattered direct light, etc.), and a ray to see some other point is typically the result of some floating-point computation going wrong: A number you expected to be slightly greater than zero was in fact slightly less. The dependence of this error on the point locations is likely to be tied to the floating-point representation, and to generate random results like speckle. But sometimes there’s a strong enough dependence on a single parameter that there’s regularity in the results. Figure 32.19 shows how the floor of the Cornell box is irregularly illuminated (a triangle in the back-right corner is too dark) when we fail to bump just the light-point position.

![](img/f464cd0043eb5336aa0543fe20a0561b_967_0.png)

*Figure 32.19: A diagonal stripe on the floor from failed visibility testing.*

Suppose that your photon mapper shows nice, smooth gradations of reflected light in the Cornell box, but there’s no color bleeding: The left side of the floor isn’t slightly red and the right side isn’t slightly blue. Think for a moment about what might be wrong, and then read on.

One thing to ask is, “Are the photons correct?” You can plot each photon as a point in your scene to verify that they’re well scattered, and you can even plot each one as a small arrow whose base is at the photon location, and which points toward the source of the light. If all the photons point toward the area light, there’s a problem: You’re not getting any scattered photons in your photon map. (You’re also storing first-hit photons, which may be intentional, but if you’re computing direct illumination in a separate step, as we did, it’s a mistake: You’ll end up double-counting the direct illumination!) Interpolating values from the photons you have will tend to give smoothly varying light, however. But you won’t get color bleeding. Let’s assume, though, that the photons are well scattered, only store indirect light, and seem to get their indirect light from many different places.

A photon on the floor near the red wall probably got there by having light hit the red wall and reflect to the floor. The problem has to be in the reflection process, that is, the multiplication by the BRDF and a cosine. Since the magnitude looks right, the absorption/reflection part of the code must be right. But the spectral distribution of the outgoing photon’s power is evidently wrong. What color should that photon be? Fairly red! By drawing your photons as small disks colored by the color of the arriving light, you can rapidly tell whether they’re correct or not. When you discover that all your photons are white, you’ve found the problem: During multiple bounces, the photon power wasn’t being multiplied by the color of the surface from which it was reflecting.

As another example, suppose that you’ve decided to improve your photon mapper with a final-gather step. You wisely keep the no-gather part of the program, and include a checkbox in the user interface to determine whether gathering is used or not. When you switch from no-gather to gather, the picture looks almost the same, but a bit dimmer. If you turn off direct light, it’s evidently a lot dimmer. In fact, by inspecting and comparing individual pixels, you find that the pixel values are all dropping by a factor of about three. Once again, think briefly about where the error must be, and then read on.

When you encounter a number near 3 in a renderer, surprisingly often it’s really π. (Similarly, a factor of 10 is often π² ≈ 9.87.) In this case, when this problem arose for one author it was because he used cosine-weighted samples for his gathering, multiplied each by the appropriate fₛ(ωᵢ, ωₒ) factor, but not the cosine (ωᵢ · n), because the cosine was included in the sampling weights, and then averaged the results. The difficulty was the failure to divide by π (the result of doing a cosine-weighted sampling of the constant function 1 on the upper hemisphere).

Suppose that in path-tracing our second model—the one with the glass sphere—we’d seen the reflection of the adjacent solid sphere and of the area light in a simple fashion 100% of the time: Because the mirror has (0, 1, 1) as its normal, an incoming ray in direction $(x, y, z)$ becomes an outgoing ray in direction $(x, -z, -y)$. It’s easy to mentally work through any such interaction. And if we choose a pixel at the center of the scene, then all $x$-coordinates will be very near 0 and can be neglected.

Doubtless you’ll develop your own approaches to debugging, but because rendering code is often closely tied to particular phenomena, an approach in which it’s easy to turn on or off certain parts of computed radiance, and to reason about what remains, makes for much easier debugging.

### 32.9 Discussion and Further Reading

As we promised at the start of this chapter, we’ve described basic implementations of a path tracer and a photon-map/ray-tracing hybrid, showing some design choices and pitfalls along the way. Each render produces an array containing radiance values, the value at pixel $(x, y)$ being an average of the radiance values for eye rays passing through a square centered at $(x, y)$, whose side length is one interpixel spacing. This models a perfect-square radiance sensor, which is a fair approximation of the CCD cells of a typical digital camera. The approximation is only “fair” because at low radiance values, noise in the CCD system may dominate, and for larger radiance values, the response of the sensor is nonlinear: It saturates at some point. And even between these limits, the sensor response isn’t really linear.

What we do with these radiance images depends on our goals. If we want to build an environment map, then a radiance image is a fine thing to work with. If we want to display the image on a conventional monitor using a standard image-display program, we need to convert each radiance value to the sort of value recorded by an ordinary camera in response to this amount of radiance. As we discussed in Chapter 28, these values are typically *not* proportional to radiance. If the radiance values cover a very wide range, an ordinary camera might truncate the lowest and highest values. Because we have the raw values, we may be able to do something more sophisticated, tricking the visual system into perceiving a wider range of brightness than is actually displayed. This is the area of study called **tone mapping** [RPG99, RSSF02, FLW02, MM06], which is an active area of current research.

Rather than simply storing the average radiance for each location, we could instead accumulate the samples themselves for later processing, allowing us to simulate the responses of several different kinds of sensors, for instance, or more generally, using them as data for a density-estimation problem, the “density” in this case being the pixel values. Our simple approach of averaging samples amounts to convolution with a box filter, but other filtering approaches yield better results for different applications [MN88]. Not surprisingly, if we know what filter we’ll be using, we can collect samples in a way that lets us best estimate the convolved value (i.e., we can do importance sampling based on the convolution filter). In general, sampling and reconstruction should be designed hand in hand whenever possible.

The notion of taking multiple samples to estimate the sensor response at a pixel was first extensively developed in Cook’s paper on distribution ray tracing [CPC84]. We’ve applied it here in its minimal form—uniform sampling over a square representing the pixel—but for animation, for instance, we also
