
that question in the first place. That is, in Chapter 37, we will introduce data structures that quickly and conservatively eliminate whole sets of triangles that the ray could not possibly intersect, without ever performing the ray-triangle intersection. So optimizing this routine now would only complicate it without affecting our long-term performance profile.

Our renderer only processes triangles. We could easily extend it to render scenes containing any kind of primitive for which we can provide a ray intersection solution. Surfaces defined by low-order equations, like the plane, rectangle, sphere, and cylinder, have explicit solutions. For others, such as bicubic patches, we can use root-finding methods.

### 15.4.4 Debugging

We now verify that the intersection code is correct. (The code we've given you is correct, but if you invoked it with the wrong parameters, or introduced an error when porting to a different language or support code base, then you need to learn how to find that error.) This is a good opportunity for learning some additional graphics debugging tricks, all of which demonstrate the Visual Debugging principle.

It would be impractical to manually examine every intersection result in a debugger or printout. That is because the `rayTrace` function invokes `intersect` thousands of times. So instead of examining individual results, we visualize the barycentric coordinates by setting the radiance at a pixel to be proportional to the barycentric coordinates following the Visual Debugging principle. Figure 15.6 shows the correct resultant image. If your program produces a comparable result, then your program is probably nearly correct.

![](img/f464cd0043eb5336aa0543fe20a0561b_461_0.png)

Figure 15.6: The single triangle scene visualized with color equal to barycentric weight for debugging the intersection code.

What should you do if your result looks different? You can't examine every result, and if you place a breakpoint in `intersect`, then you will have to step through hundreds of ray casts that miss the triangle before coming to the interesting intersection tests.

This is why we structured `rayTrace` to trace within a caller-specified rectangle, rather than the whole image. We can invoke the ray tracer on a single pixel from `main()`, or better yet, create a debugging interface where clicking on a pixel with the mouse invokes the single-pixel trace on the selected pixel. By setting breakpoints or printing intermediate results under this setup, we can investigate why an artifact appears at a specific pixel. For one pixel, the math is simple enough that we can also compute the desired results by hand and compare them to those produced by the program.

In general, even simple graphics programs tend to have large amounts of data. This may be many triangles, many pixels, or many frames of animation. The processing for these may also be running on many threads, or on a GPU. Traditional debugging methods can be hard to apply in the face of such numerous data and massive parallelism. Furthermore, the graphics development environment may preclude traditional techniques such as printing output or setting breakpoints. For example, under a hardware rendering API, your program is executing on an embedded processor that frequently has no access to the console and is inaccessible to your debugger.

Fortunately, three strategies tend to work well for graphics debugging.

- 1. Use assertions literally. These cost you nothing in the optimized version of the program, pass silently in the debug version when the program operates correctly, and break the program at the test location when an assertion is violated. Thus, they help to identify failure cases without requiring that you manually step through the correct cases.
- 2. Immediately reduce to the minimal test case. This is often a single-triangle scene with a single light and a single pixel. The trick here is to find the combination of light, triangle, and pixel that produces incorrect results. Assertions and the GUI click-to-debug scheme work well for that.
- 3. Visualize intermediate results. We have just rendered an image of the barycentric coordinates of eye-ray intersections with a triangle for a 400,000-pixel image. Were we to print out these values or step through them in the debugger, we would have little chance of recognizing an incorrect value in that mass of data. If we see, for example, a black pixel, or a white pixel, or notice that the red and green channels are swapped, then we may be able to deduce the nature of the error that caused this, or at least know which inputs cause the routine to fail.

### 15.4.5 Shading

We are now ready to implement `shade`. This routine computes the incident radiance at the intersection point P and how much radiance scatters back along the eye ray to the viewer.

Let’s consider only light transport paths directly from the source to the surface to the camera. Under this restriction, there is no light arriving at the surface from any directions except those to the lights. So we only need to consider a finite number of ωᵢ values. Let’s also assume for the moment that there is always a line of sight to the light. This means that there will (perhaps incorrectly) be no shadows in the rendered image.

Listing 15.17 iterates over the light sources in the scene (note that we have only one in our test scene). For each light, the loop body computes the distance and direction to that light from the point being shaded. Assume that lights emit uniformly in all directions and are at finite locations in the scene. Under these assumptions, the incident radiance Lᵢ at point P is proportional to the total power of the source divided by the square of the distance between the source and P. This is because at a given distance, the light’s power is distributed equally over a sphere of that radius. Because we are ignoring shadowing, let the `visible` function always return `true` for now. In the future it will return `false` if there is no line of sight from the source to P, in which case the light should contribute no incident radiance.

The outgoing radiance to the camera, Lₒ, is the sum of the fraction of incident radiance that scatters in that direction. We abstract the scattering function into a BSDF. We implement this function as a class so that it can maintain state across multiple invocations and support an inheritance hierarchy. Later in this book, we will also find that it is desirable to perform other operations beyond invoking this function; for example, we might want to sample with respect to the probability distribution it defines. Using a class representation will allow us to later introduce additional methods for these operations.

The `evaluateFiniteScatteringDensity` method of that class evaluates the scattering function for the given incoming and outgoing angles. We always then take the product of this and the incoming radiance, modulated by the cosine of the angle between w_i and n to account for the projected area over which incident radiance is distributed (by the Tilling principle).

*Listing 15.17: The single-bounce shading code.*

```cpp
void shade(const Scene& scene, const Triangle& T, const Point3& P,
           const Vector3& n, const Vector3& w_o, Radiance3& L_o) {

    L_o = Color3(0.0f, 0.0f, 0.0f);

    // For each direction (to a light source)
    for (unsigned int i = 0; i < scene.lightArray.size(); ++i) {
        const Light& light = scene.lightArray[i];

        const Vector3 offset = light.position - P;
        const float distanceToLight = offset.length();
        const Vector3 w_i = offset / distanceToLight;

        if (visible(P, w_i, distanceToLight, scene)) {
            const Radiance3 L_i = light.power / (4 * PI * square(distanceToLight));

            // Scatter the light
            L_o +=
                L_i *
                T.bsdf(n).evaluateFiniteScatteringDensity(w_i, w_o) *
                max(0.0, dot(w_i, n));
        }
    }
}
```

### 15.4.6 Lambertian Scattering

The simplest implementation of the BSDF assumes a surface appears to be the same brightness independent of the viewer's orientation. That is, `evaluateFiniteScatteringDensity` returns a constant. This is called Lambertian reflectance, and it is a good model for matte surfaces such as paper and flat wall paint. It is also trivial to implement. Listing 15.18 gives the implementation (see Section 14.9.1 for a little more detail and Chapter 29 for a lot more). It has a single member, `k_L`, that is the “color” of the surface. For energy conservation, this value should have all fields on the range [0, 1].

*Listing 15.18: Lambertian BSDF implementation, following Listing 14.6.*

```cpp
class BSDF {
public:
    Color3 k_L;

    /* Returns f = L_o / (L_i * w_i.dot(n)) assuming
       incident and outgoing directions are both in the
       positive hemisphere above the normal */
    Color3 evaluateFiniteScatteringDensity
        (const Vector3& w_i, const Vector3& w_o) const {
        return k_L / PI;
    }
};
```

Figure 15.7 shows our triangle scene rendered with the Lambertian BSDF using `k_L = Color3(0.0f, 0.0f, 0.8f)`. Because our triangle's vertex

![](img/f464cd0043eb5336aa0543fe20a0561b_463_0.png)

*Figure 15.7: A green Lambertian triangle.*
