**Inline Exercise 15.3:** Two images are shown below. Both have been gamma-encoded with γ = 2.0 for printing and online display. The image on the left is a gradient that has been rendered to give the impression of linear *brightness*. It should appear as a linear color ramp. The image on the right was rendered with linear *radiance* (it is the checkerboard on the right of Figure 15.2 without the blue squares). It should appear as a nonlinear color ramp. The image was rendered at 200 × 200 pixels. What equation do we use to compute the value (in [0, 1]) of the pixel at (x, y) for the gradient image on the left?

![](bbox=[0.19, 0.347, 0.551, 0.474])

# 15.3.3 Scene Representation

Listing 15.7 shows a `Triangle` class. It stores each triangle by explicitly storing each vertex. Each vertex has an associated normal that is used exclusively for shading; the normals do not describe the actual geometry. These are sometimes called **shading normals**. When the vertex normals are identical to the normal to the plane of the triangle, the triangle’s shading will appear consistent with its actual geometry. When the normals diverge from this, the shading will mimic that of a curved surface. Since the silhouette of the triangle will still be polygonal, this effect is most convincing in a scene containing many small triangles.

*Listing 15.7: Interface for a `Triangle` class.*

```
class Triangle {
private:
    Point3      m_vertex[3];
    Vector3     m_normal[3];
    BSDF        m_bsdf;

public:

    const Point3& vertex(int i) const { return m_vertex[i]; }
    const Vector3& normal(int i) const { return m_normal[i]; }
    const BSDF& bsdf() const { return m_bsdf; }
    ...
};
```

We also associate a BSDF class value with each triangle. This describes the material properties of the surface modeled by the triangle. It is described in Section 15.4.5. For now, think of this as the color of the triangle.