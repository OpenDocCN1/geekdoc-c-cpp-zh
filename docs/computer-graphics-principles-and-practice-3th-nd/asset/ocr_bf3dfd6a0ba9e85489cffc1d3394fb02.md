```
```text
SetColor(t);
BlendFunc(ZERO, SRC_COLOR);
DrawSurface();
```
```

We’ve presented this in a form similar to the OpenGL API for real-time rasterization rendering. The mathematics can be applied per-pixel in another rendering framework, such as a ray tracer. Doing so is common practice, although we suggest that if you’ve already written a ray tracer with well-structured ray-scattering code, then it may be trivial to implement much more accurate transmission with a BSDF than with blending. If you choose to employ the blending model, the code might look something like:

```
```text
Radiance3 shade(Vector3 dirToEye, Point3 P, Color3 t, Color4 s, ...) {
    Radiance3 d;
    if (bsdf has transparency)
        // Continue the ray out the back of the surface
        d = rayTrace(Ray(P - dirToEye * epsilon, -dirToEye));
    }

    Radiance3 c = directIllumination(P, dirToEye, s.rgb, ...);

    // Perform the blending of this surface’s color and the background
    return c * s.alpha + d * (t * s.alpha + 1 - s.alpha);
}
```
```

Our blending model for transmission at this point supports frequency-varying (colored) transmission and a distinct color scattered by or emitted at the surface. Yet it still assumes an infinitely thin object so that transmission can be computed once at the surface. For an object with nonzero thickness, light should continue to be absorbed within the material so that thicker objects transmit less light than thinner ones of the same material.

Consider the case of two thin objects held together, assuming \(s_\alpha = 1\) macroscopic coverage and \(1 - t_{rgb}\) microscopic coverage, that is, transmission. We expect the first object to transmit \(t\) of the light from the background; \(d' = td\); and the second to transmit \(t\) of that, for a \(d'' = t^2d\) net contribution from the background, as in our previous double-compositing example of macroscopic partial coverage. Now consider the case of three such thin objects; the net light transmitted will be \(t^3d\). Following this pattern, a thick object composed of \(n\) thin objects will transmit \(t^nd\). The absorption of light is thus exponential in distance, as we suggested in Equation 14.13.

We can still apply the simple compositing model if we precompute an effective net transmission coefficient \(t\) for the thick object based on the distance \(x\) that light will travel in the medium, that is, its cross section along the ray. Three common methods for computing this thickness are tracing a ray (even within the context of a rasterization algorithm), rendering multiple depth buffers so that the front and back surfaces of the object are both known (e.g., [BCL\u207a07]), or simply assuming a constant thickness. It is common to express the rate of absorption by a constant \(k\). The net transmission by the thick object along the ray is thus \(t = e^{-kx}\). The thin-blending model can then be applied with this constant. This exponential falloff is a fairly accurate model and \(k\) can be computed from first principles; however, given the rest of the rendering structure that we’ve assumed in this section, it is more likely to be chosen aesthetically in practice.