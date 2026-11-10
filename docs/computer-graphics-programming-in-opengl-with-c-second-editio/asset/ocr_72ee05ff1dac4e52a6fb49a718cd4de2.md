# **Program 16.10 – Refraction Through a Sphere – Two Secondary Rays**
*Compute Shader*

```
```cpp
...
vec3 raytrace3(Ray r)
{ // this function is identical to raytrace() from Program 16.7

}
...
vec3 raytrace2(Ray r)
{
   ...
   if (c.object_index == 1)  // recall that index==1 indicates collision with the sphere
   {  // generate a second secondary ray for the intersection with the back of the sphere
      Ray refracted_ray;
      refracted_ray.start = c.p - c.n * 0.001;
      refracted_ray.dir = refract(dir, c.n, 1.5);   // index of refraction from glass to air: IOR = 1.5
      vec3 refracted_color = raytrace3(refracted_ray);
      return 2.0*ads_phong_lighting(r, c) * refracted_color;
   }
   ...
}
...
vec3 raytrace(Ray r)
{
   if (c.object_index == 1)
   {  // generate a secondary ray for the intersection with the front of the sphere
      Ray refracted_ray;
      refracted_ray.start = c.p - c.n * 0.001;
      refracted_ray.dir = refract(dir, c.n, 0.6667);   // index of refraction from air to glass: IOR = 1.0/1.5
      vec3 refracted_color = raytrace2(refracted_ray);
      return 2.0*ads_phong_lighting(r, c) * refracted_color;
   }
   ...
}
...
```
```

Figure 16.15 shows the result. Notice that the view of the scene through the transparent sphere has been flipped and appears upside down. A flipped (and severely curved) version of the brick box is also visible in the sphere, as is the checkerboard plane. Also, although not easily seen in Figure 16.15, it is the *back* of the skybox that is visible in the sphere, whereas in Figure 16.11, the sphere reflected the front portion of the skybox.