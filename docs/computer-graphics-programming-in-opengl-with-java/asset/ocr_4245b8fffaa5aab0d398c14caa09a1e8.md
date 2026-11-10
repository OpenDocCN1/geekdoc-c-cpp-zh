Note also that the trick we used to avoid surface acne is modified slightly in both functions; instead of adding a small offset along the normal, we subtract the offset. This is because the secondary rays now continue through the collision point rather than rebounding. So, for refracted rays, we must add a small offset along the negative of the normal.

# ***Program 16.10 Refraction Through a Sphere — Two Secondary Rays***

Compute Shader

```
...
vec3 raytrace3(Ray r)
{
    // (this function is identical to raytrace() from Program 16.7
    ...
}

vec3 raytrace2(Ray r)
{
    ...
    if (c.object_index == 1)    // recall that index==1 indicates collision with the sphere
    {
        // generate a second secondary ray for the intersection with the back of the sphere
        Ray refracted_ray;
        refracted_ray.start = c.p - c.n * 0.001;
        refracted_ray.dir = refract(r.dir, c.n, 1.5);    // index of refraction from glass to air: IOR = 1.5
        vec3 refracted_color = raytrace3(refracted_ray);
        return 2.0 * ads_phong_lighting(r, c) * refracted_color;
    }
    ...
}

vec3 raytrace(Ray r)
{
    ...
    if (c.object_index == 1)
    {
        // generate a secondary ray for the intersection with the front of the sphere
        Ray refracted_ray;
        refracted_ray.start = c.p - c.n * 0.001;
        refracted_ray.dir = refract(r.dir, c.n, .66667); // index of refraction from air to glass: IOR=1.0/1.5
        vec3 refracted_color = raytrace2(refracted_ray);
        return 2.0 * ads_phong_lighting(r, c) * refracted_color;
    }
    ...
}
```