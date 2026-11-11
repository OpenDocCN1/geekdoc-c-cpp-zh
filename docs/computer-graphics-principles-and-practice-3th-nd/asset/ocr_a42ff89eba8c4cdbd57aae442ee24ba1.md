radial falloff. In the real world, the total power observed at distance r from a uniform spherical emitter whose radius is much smaller than r is proportional to 1/r^2. We can generalize this by computing a value M that involves an inverse quadratic:

$$ M = \frac{\Phi}{(a_0 r^0 m^2 + a_1 r^1 m^1 + a_2 r^2 m^0) 4\pi}. \tag{14.44} $$

If we define a and r by

$$ \vec{a} = (a_0 m^2, a_1 m^1, a_2 m^0), \quad \text{and} \tag{14.45} $$
$$ \vec{r} = (r^0, r^1, r^2), \tag{14.46} $$

then we can rewrite the formula for M as

$$ M = \frac{\Phi}{\vec{a} \cdot \vec{r} 4\pi}. \tag{14.47} $$

This strange expression lets us represent a point emitter that experiences non-physical falloff to approximate a local area source or distant point source, or simply to satisfy an artistic vision. In this context, a directional source can be parameterized by the attenuation constant \vec{a} = (1, 0, 0). This source will produce equal intensity at all points in the scene, and that intensity is comparable to what a local source with power \Phi one meter from a surface would produce.

The resulting interface (Listing 14.15) follows the spirit of the OpenGL fixed-function lighting model, albeit with slightly varying units and border cases. We do not recommend this model for physically based rendering.

# *Listing 14.15: A simple unified model for spot, directional, and omni light sources.*

```
```cpp
class PointLight : public Light {
private:

    /* For local lights, this is the total power of the light source.
       For directional lights, this is the power of an equivalent
       local source 1 m from the surface. */
    Power3      Phi;

    Vector3     axis;

    /* Center of the light in homogeneous coordinates. */
    Vector4     C;

    Vector3     aVec;

    float       spotHalfAngle;

    ...
};
```
```

# *Listing 14.16: PointLight methods for direct illumination.*

```
```cpp
Vector4 PointLight::randomPoint() const {
    return C;
}
```
```