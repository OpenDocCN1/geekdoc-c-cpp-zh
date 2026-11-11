
normals are deflected away from the plane defined by the vertices, the triangle appears curved. Specifically, the bottom of the triangle is darker because the `w_i.dot(n)` term in line 20 of Listing 15.17 falls off toward the bottom of the triangle.

## 15.4.7 Glossy Scattering

The Lambertian surface appears dull because it has no highlight. A common approach for producing a more interesting shiny surface is to model it with something like the Blinn-Phong scattering function. An implementation of this function with the energy conservation factor from Sloan and Hoffmann [AMNH08, 257] is given in Listing 15.19. See Chapter 27 for a discussion of the origin of this function and alternatives to it. This is a variation on the shading function that we saw back in Chapter 6 in WPF, only now we are implementing it instead of just adjusting the parameters on a black box. The basic idea is simple: Extend the Lambertian BSDF with a large radial peak when the normal lies close to halfway between the incoming and outgoing directions. This peak is modeled by a cosine raised to a power since that is easy to compute with dot products. It is scaled so that the outgoing radiance never exceeds the incoming radiance and so that the sharpness and total intensity of the peak are largely independent parameters.

*Listing 15.19: Blinn-Phong BSDF scattering density.*

```cpp
class BSDF {
public:
    Color3 k_L;
    Color3 k_G;
    float s;
    Vector3 n;
    ...

    Color3 evaluateFiniteScatteringDensity(const Vector3& w_i,
        const Vector3& w_o) const {
        const Vector3& w_h = (w_i + w_o).direction();
        return
            (k_L + k_G * ((s + 8.0f) *
                powf(std::max(0.0f, w_h.dot(n)), s) / 8.0f)) /
            PI;
    }
};
```

For this BSDF, choose `Lambertian + glossy < 1` at each color channel to ensure energy conservation, and `glossySharpness` typically in the range [0, 200]. The `glossySharpness` is on a logarithmic scale, so it must be moved in larger increments as it becomes larger to have the same perceptual impact.

Figure 15.8 shows the green triangle rendered with the normalized Blinn-Phong BSDF. Here, `k_L=Color3(0.0f, 0.0f, 0.8f)`, `k_G=Color3(0.2f, 0.2f, 0.2f)`, and `s=100.0f`.

![](img/f464cd0043eb5336aa0543fe20a0561b_464_0.png)

Figure 15.8: Triangle rendered with a normalized Blinn-Phong BSDF.

## 15.4.8 Shadows

The shade function in Listing 15.17 only adds the illumination contribution from a light source if there is an unoccluded line of sight between that source and the point P being shaded. Areas that are occluded are therefore darker. This absence of light is the phenomenon that we recognize as a shadow.

In our implementation, the line-of-sight visibility test is performed by the `visible` function, which is supposed to return `true` if and only if there is an unoccluded line of sight. While working on the shading routine we temporarily implemented `visible` to always return `true`, which means that our images contain no shadows. We now revisit the `visible` function in order to implement shadows.

We already have a powerful tool for evaluating line of sight: the `intersect` function. The light source is not visible from *P* if there is some intersection with another triangle. So we can test visibility simply by iterating over the scene again, this time using the *shadow ray* from *P* to the light instead of from the camera to *P*. Of course, we could also test rays from the light to *P*.

Listing 15.20 shows the implementation of `visible`. The structure is very similar to that of `sampleRayTriangle`. It has three major differences in the details. First, instead of shading the intersection, if we find any intersection we immediately return `false` for the visibility test. Second, instead of casting rays an infinite distance, we terminate when they have passed the light source. That is because we don’t care about triangles past the light—they could not possibly cast shadows on *P*. Third and finally, we don’t really start our shadow ray cast at *P*. Instead, we offset it slightly along the ray direction. This prevents the ray from reintersecting the surface containing *P* as soon as it is cast.

*Listing 15.20: Line-of-sight visibility test, to be applied to shadow determination.*

```cpp
bool visible(const Vector3& p, const Vector3& direction, float
            distance, const Scene& scene) {
    static const float rayBumpEpsilon = 1e-4;
    const Ray shadowRay(p + direction * rayBumpEpsilon, direction);

    distance -= rayBumpEpsilon;

    // Test each potential shadow caster to see if it lies between P and the light
    float ignore[3];
    for (unsigned int s = 0; s < scene.triangleArray.size(); ++s) {
        if (intersect(shadowRay, scene.triangleArray[s], ignore) < distance) {
            // This triangle is closer than the light
            return false;
        }
    }

    return true;
}
```

Our single-triangle scene is insufficient for testing shadows. We require one object to cast shadows and another to receive them. A simple extension is to add a quadrilateral “ground plane” onto which the green triangle will cast its shadow. Listing 15.21 gives code to create this scene. Note that this code also adds another triangle with the same vertices as the green one but the opposite winding order. Because our triangles are single-sided, the green triangle would not cast a shadow. We need to add the back of that surface, which will occlude the rays cast upward toward the light from the ground.

![](img/f464cd0043eb5336aa0543fe20a0561b_465_0.png)

Figure 15.9: The green triangle scene extended with a two-triangle gray ground “plane.” A back surface has also been added to the green triangle.

**Inline Exercise 15.7:** Walk through the intersection code to verify the claim that without the second “side,” the green triangle would cast no shadow.

Figure 15.9 shows how the new scene should render *before* you implement shadows. If you do not see the ground plane under your own implementation, the most likely error is that you failed to loop over all triangles in one of the ray-casting routines.

*Listing 15.21: Scene-creation code for a two-sided triangle and a ground plane.*

```cpp
void makeOneTriangleScene(Scene& s) { s.triangleArray.resize(1);

    s.triangleArray[0] =
        Triangle(Vector3(0,1,-2), Vector3(-1.9,-1,-2), Vector3(1.6,-0.5,-2),
            Vector3(0,0.6,1).direction(),
            Vector3(-0.4f,-0.4f,1.0f).direction(),
            Vector3(0.4f,-0.4f,1.0f).direction(),
            BSDF(Color3::green() * 0.8f,Color3::white() * 0.2f, 100));

    s.lightArray.resize(1);
    s.lightArray[0].position = Point3(1, 3, 1);
    s.lightArray[0].power = Color3::white() * 10.0f;
}

void makeTrianglePlusGroundScene(Scene& s) {
    makeOneTriangleScene(s);

    // Invert the winding of the triangle
    s.triangleArray.push_back
        (Triangle(Vector3(-1.9,-1,-2), Vector3(0,1,-2),
            Vector3(1.6,-0.5,-2), Vector3(0,-0.4f,1.0f).direction(),
            Vector3(0,0.6f,1).direction(), Vector3(-0.4f,-0.4f,1.0f).direction(),
            BSDF(Color3::green() * 0.8f,Color3::white() * 0.2f, 100)));

    // Ground plane
    const float groundY = -1.0f;
    const Color3 groundColor = Color3::white() * 0.8f;
    s.triangleArray.push_back
        (Triangle(Vector3(-10, groundY, -10), Vector3(-10, groundY, -0.01f),
            Vector3(10, groundY, -0.01f),
            Vector3::unitY(), Vector3::unitY(), Vector3::unitY(), groundColor));

    s.triangleArray.push_back
        (Triangle(Vector3(-10, groundY, -10), Vector3(10, groundY, -0.01f),
            Vector3(10, groundY, -10),
            Vector3::unitY(), Vector3::unitY(), Vector3::unitY(), groundColor));
}
```

Figure 15.10 shows the scene rendered with `visible` implemented correctly. If the `rayBumpEpsilon` is too small, then **shadow acne** will appear on the green triangle. This artifact is shown in Figure 15.11. An alternative to starting the ray artificially far from *P* is to explicitly exclude the previous triangle from the shadow ray intersection computation. We chose not to do that because, while appropriate for unstructured triangles, it would be limiting to maintain that custom ray intersection code as our scene becomes more complicated. For example, we would like to later abstract the scene data structure from a simple array of triangles. The abstract data structure might internally employ a hash table or tree and have complex methods. Pushing the notion of excluding a surface into such a data structure could complicate that data structure and compromise its general-purpose use. Furthermore, although we are rendering only triangles now,

![](img/f464cd0043eb5336aa0543fe20a0561b_466_0.png)
