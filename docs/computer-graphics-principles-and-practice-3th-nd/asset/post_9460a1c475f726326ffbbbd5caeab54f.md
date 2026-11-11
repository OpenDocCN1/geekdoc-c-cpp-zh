
The direct-lighting computation is essentially identical to that in the path tracer, except that we estimate the direct light from each area light with several (`m_diffuseDirectSamples`) samples rather than relying on multiple primary rays to ensure adequate sampling. (The alternative is quite viable, however.) The similarity is so great that we omit the code. This leaves only the impulse-scattered and diffusely reflected indirect light to consider. The first is easy, and it closely resembles the corresponding path-tracing code: We simply compute the total arriving radiance for each impulse recursively, and sum (see Listing 32.17).

This leaves only the computation of diffusely reflected indirect light, which is where the photon map finally comes into play (see Listing 32.18). Central to this code is the photon map's *kernel*, the function that says how much weight to give each nearby photon's contribution.

*Listing 32.18: The photon map used to compute diffusely reflected indirect light.*

```cpp
Radiance3 App::estimateDiffuselyReflectedIndirectLight(const Ray &r,
    const SurfaceElements &surfel) {
    Radiance3 L_o(0.0f);
    Array<Photon> photonArray;
    // find nearby photons
    m_photonMap.getIntersectingMembers(
        Sphere(surfel.geometric.location, m_photonMap.gatherRadius()), photonArray);

    foreach photon p in the array
        const float cos_theta_i =
        L_o += p.power() * m_photonMap.kernel(p.position(), surfel.shading.location) *
            surfel.evaluateBSDF(p.directionToSource(), -r.direction(), finf());
    return L_o;
}
```

We sum up the contributions of all sufficiently nearby photons, weighting them by our kernel and pushing each one through the BSDF to determine the light it contributes traveling toward the source of the ray *r*.

Note that what is being multiplied by the BRDF term is an area-weighted radiance, which is what we called **biradiance** in Chapter 14.

### 32.6.1 Results and Discussion

Naturally, as we discussed in Chapter 31, there's an interaction between the gather radius, the number of photons stored in the photon map, and the quality of the estimated radiance. When we're estimating the reflected indirect radiance at *P*, if we use a **cylinder kernel** (a photon is counted if it's within some distance of *P*, and ignored otherwise) and there are no photons within the gather radius of *P*, the radiance estimate for that ray will be zero. This can happen if the gather radius is too small or if there are too few photons. How many photons are enough? Well, we'd generally like nearby pixel rays hitting the same surface to get similar radiance estimates. But one ray might be within the radius of 20 photons, while the nearby ray might be within the radius of 21 photons. Even if all the photons share the same incoming power, the second ray will get a radiance that's 5% greater. To reduce the noise in areas of constant radiance, it appears that we might need hundreds of photons within the gather radius of *P*.

There are several ways to improve the results without needing that many photons. One is to alter the photon map's **kernel**—the weighting function, centered at *P*, that determines how much each photon’s contribution should matter in the radiance estimate. If we change from the cylinder kernel to a conelike function (photons near the gather radius have their contributions reduced to near zero), then each arrival or departure of a photon within the gather radius (as we vary *P*) has a gradual impact. This is the approach used in our renderer.

A very different approach is described by *Jensen*: Rather than gathering photons within a *fixed* radius, we enlarge the radius enough to get a certain number of photons, and then use the area of the resultant disk in the conversion from power (stored at incoming photons) to outgoing radiance.

The ray-trace-with-photon-mapping renderer we’ve written has several parameters (the number of samples to use to estimate lighting from area lights, the radius of the kernel, the number of photons to shoot into the scene), each of which has an effect on the final result. Figure 32.12 shows that with only 100 photons, the Cornell box scene looks blotchy, because most points in the scene are not within the kernel radius of any photons at all. With one million photons, each point is near thousands of photons, and the estimate of diffusely reflected indirect light is very smooth. (We’ve used a large number of samples for area lights to reduce that source of variation in the image.)

With a larger kernel radius, the low-photon-count image would look smoother, but then distant photons would affect the appearance of the scene at any point. Clearly there’s a tradeoff between photon count *N* and kernel radius *r*. In *Jensen’s* original photon-mapping algorithm, the radiance estimate was provided by using a *fixed number*, *k*, of photons, enlarging the radius as necessary to find that many photons. This has the advantage of **scale invariance**—if you double the scene size, you needn’t change anything—but it still leaves the problem of choosing *N* and *k*.

The number of samples used in estimating direct lighting from area lights also has an impact on the noise in the image. Figure 32.13 shows this, again using the Cornell box. With only one sample per light, the image is very noisy; with 100, the noise is lower than that of the photon-mapped estimate of reflected indirect radiance in Figure 32.12.

> **Inline Exercise 32.8:** In the one-sample-per-source image, how is the noisiness correlated with the brightness, and why? In which areas of the image is the human visual system most sensitive to the noise?

It’s typical in renderers like this one to use many primary rays per pixel. If we use 100 primary rays, then we need not use very many rays (per primary ray) to estimate direct lighting from area sources. We still, however, as *Inline Exercise 32.8* suggests, must address the noise in *some way*, particularly if there are dark areas in the scene. Fortunately in the case of the Cornell box, indirectly reflected light dominates the direct light near the top, and so the noise there ends up less perceptually significant when we include indirect light.

![](img/f464cd0043eb5336aa0543fe20a0561b_961_0.png)

*Figure 32.12: The Cornell box rendered with 100, 10,000, and 1,000,000 photons.*

![](img/f464cd0043eb5336aa0543fe20a0561b_962_0.png)

*Figure 32.13: One-sample-per-pixel rendering of the emitted direct light from area lights only, using 1, 10, and 100 samples to estimate the light from the area source.*

![](img/f464cd0043eb5336aa0543fe20a0561b_962_1.png)

*Figure 32.14: The three other test scenes, rendered with 100 primary rays per pixel, ten thousand (top row) and one million (bottom row) shot photons, and one sample per source for area lights.*

Looking at the other test scenes (see Figure 32.14), we see that photon mapping with one million photons handles the first scene very well. The third scene, with the transparent sphere, exhibits a caustic highlight beneath the sphere. In the fourth scene, the emitting luminaire is (as a reflector) completely Lambertian and black. The mirror is pure specular, and the panel beneath the mirror is dark and Lambertian. Even with one million photons shot, only a few photons end up in the scene, and they're used only in estimating the brightness of the panel beneath the mirror, which is overwhelmingly determined by direct lighting, so the computation of the photon map was almost pointless.

In all versions of photon mapping, we're converting from samples of the arriving power near *P* to an estimate of that power at *P*. This is extremely closely related to the problem of **density estimation** in statistics. The most basic form of density estimate is **nearest neighbor**, in which the value at *P* is taken to be the value at the sample nearest to \(P\). For a continuous density, this converges to the correct value as the number of samples gets large, but the convergence is not exactly the kind we’d like: For any fixed set of samples, the nearest-neighbor estimate of density is piecewise-constant. (On a plane, the regions of constancy are the Voronoi cells associated to the samples.) This leads to a great many discontinuities. On the other hand, as the number of samples increases, the values in adjacent cells get closer and closer, so while the set of discontinuities grows, the magnitude of the discontinuities decreases [WHSG97].

There are many other forms of density estimation aside from nearest-neighbor interpolation. Weighted averaging by some filter kernel is one; Jensen’s method of gathering a fixed number of samples and then dividing by a value that depends on those samples is another. Whole books have been written on density estimation, and the statistics and mathematics quickly become increasingly complex as the sophistication of the methods increases.

### 32.6.2 Further Photon Mapping

The hybrid ray-tracing-photon-mapper approach described above is very basic. Just as we factored out direct lighting, computing it with ray-tracing rather than the photon map, it’s possible to build special photon maps that contain only photons that have passed through particular sequences of scattering, such as caustics and shadows (carefully omitting these photons from the generic photon map so that they’re not double-counted). Such specialized maps can be used to more accurately generate such phenomena, at the cost of ever-growing code complexity.

There is one technique, however, that applies not just to photon mapping, but to many algorithms: a **final gather** step, in which the incoming radiance at the eye-ray/scene-intersection point is estimated by tracing several rays from that intersection and using some estimation technique at the *secondary* intersections to determine the radiance along those rays; these secondary estimates are then combined to form an estimate along the eye ray. For instance, if the eye ray meets the world at \(P\), we trace 20 rays from \(P\) that meet the world at locations \(Q_1,\ldots,Q_{20}\). At each \(Q_i\), we can use our photon map to estimate the radiance leaving \(Q_i\) in the direction toward \(P\), and then combine these 20 samples of arriving radiance at \(P\) to get the radiance exiting from \(P\) toward the eye. By carefully selecting the directions along which to sample, we can produce an estimate of the outgoing radiance at \(P\) that has far fewer artifacts than would arise from the direct photon-map estimate. For instance, if the photon map is using a disk-shaped reconstruction filter, and not very many photons, there will be many sharp discontinuities in the reconstructed radiance estimates used at the points \(Q_i\). But when these are averaged by the reflectance equation at \(P\) to produce the outgoing radiance there, the result is far fewer artifacts in the final rendering.

The alteration in the code is quite minor, as shown in Listing 32.19: The code for estimating the diffusely reflected indirect light at the point \(P\) gets a new argument—`useGather`—that is set to `true` for primary rays but `false` for all subsequent ones. When it’s false, we use the photon map as above. But when it’s true, we essentially perform one-level ray tracing, with a large number of secondary rays, using `photonRender` to estimate the incoming radiance along these.
