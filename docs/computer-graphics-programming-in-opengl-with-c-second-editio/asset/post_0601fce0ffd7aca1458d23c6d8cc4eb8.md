
## 16.3.2 Refraction

What happens when an object is transparent? Of course, we expect to see what lies behind it (at least partially). As we saw in Chapter 14, OpenGL has support for rendering with transparency, and there are commands for blending colors to simulate transparency. However, ray tracing can give us the tools to generate some of the more complex aspects of transparency and improve realism. For example, ray tracing allows us to simulate refraction.

Refraction happens when light rays are bent when passing through a transparent object, causing an object's position to appear to shift when it is placed behind another transparent object. The amount that the light rays are bent depends on the shape of the transparent object and the material of which it is made. A transparent object is sometimes referred to as the *medium* that the light is passing through, and different transparent media (such as water, glass, or a diamond) bend light to different degrees. Anyone who has peered through a fishbowl knows how complex refraction can be. We will only scratch the surface and see some very simple examples.

The amount that a given medium bends light is called its *index of refraction* or *IOR*. We usually indicate index of refraction with η. IOR is a factor that indicates the degree to which a ray's angle when it hits a medium is altered when the ray continues through the medium (actually, the sines of those angles). The IOR of a vacuum is 1, and the IOR of glass is about 1.5. The IOR of air is so close to 1 that it is usually ignored.

In the case of an object that has thickness (such as our sphere or box, if transparent), refraction may occur both when the ray enters the object, and then again when it exits, and both would need to be considered to properly render an object behind a transparent one. Thus, adding refraction to our scene (e.g., making the sphere or the box transparent) requires a sequence of two successive secondary rays, one that refracts from the initial ray into the object and a second one that refracts as the ray exits the object. An example is shown in Figure 16.14, where the current initial ray being processed is labeled I, the normal at the initial collision point is N₁, the first secondary ray is S₁, the normal at the second collision point is N₂, and the second secondary ray is S₂. In a purely transparent object, the color at the final collision point C is the color that would ultimately be rendered at the collision point of the initial ray I.

![](img/1695de1bc7486362f86c143285f3fb40_449_0.png)

**Figure 16.14**
Refraction with two secondary rays, through a transparent sphere
(The angles have been exaggerated for clarity.)

The derivation for computing a refraction angle is well-documented [F96]:

$$
S = \left( \eta_r (N \cdot I) - \sqrt{1 - \eta_r^2 \left(1 - \operatorname{dot}(N,I)^2\right)} \right) N - \eta_r I
$$

where η_r is the ratio of the IORs of the source and destination media. Rather than code this formula, we simply use the GLSL refract() function that implements it. refract() takes three parameters as input: the incoming vector I, the normal vector N, and the IOR ratio η_r. It then produces the refracted secondary ray S as output.

For a transparent solid glass sphere, the IOR at the point of entry is IOR_air/IOR_glass = 1.0/1.5 ≈ 0.66, and at the point of exit, it is IOR_glass/IOR_air = 1.5/1.0 = 1.5.

Program 16.10 converts the sphere to solid transparent glass, this time using a sequence of two secondary rays so as to generate the refraction of the brick box and skybox behind it. We have also built yet a third copy of the raytrace() function, so that the two secondary rays can be generated and traced in succession, one entering the sphere (with IOR=0.66) and one leaving it (with IOR=1.5). Lighting is included in both the entry and exit points. Since the color and lighting values are all fractions in the range [0..1], and we are multiplying them together, it is common to also need to scale the resulting color values up or the final result will be too dark; here we have scaled the refracted colors up by a factor of 2.0.

Note also that the trick we used to avoid surface acne is modified slightly in both functions; instead of adding a small offset along the normal, we subtract the offset. This is because the secondary rays now continue through the collision point rather than rebounding. So, for refracted rays, we must add a small offset along the negative of the normal.

### Program 16.10 – Refraction Through a Sphere – Two Secondary Rays

*Compute Shader*

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
      refracted_ray.dir = refract(r.dir, c.n, 1.5);   // index of refraction from glass to air: IOR = 1.5
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
      refracted_ray.dir = refract(r.dir, c.n, 0.6667);   // index of refraction from air to glass: IOR = 1.0/1.5
      vec3 refracted_color = raytrace2(refracted_ray);
      return 2.0*ads_phong_lighting(r, c) * refracted_color;
   }
   ...
}
...
```

Figure 16.15 shows the result. Notice that the view of the scene through the transparent sphere has been flipped and appears upside down. A flipped (and severely curved) version of the brick box is also visible in the sphere, as is the checkerboard plane. Also, although not easily seen in Figure 16.15, it is the *back* of the skybox that is visible in the sphere, whereas in Figure 16.11, the sphere reflected the front portion of the skybox.

### Program 16.11 – Combining Reflection and Refraction

*Compute Shader*

```cpp
...
vec3 raytrace(Ray r)
{
    if (c.object_index == 1)
    { // generate a refraction ray
        Ray refracted_ray;
        refracted_ray.start = c.p - c.n * 0.001;
        refracted_ray.dir = refract(r.dir, c.n, 0.66667);
        vec3 refracted_color = raytrace2(refracted_ray); // refraction requires two rays, entry and exit
        // generate a reflection ray
        Ray reflected_ray;
        reflected_ray.start = c.p + c.n * 0.001;
        reflected_ray.dir = reflect(r.dir, c.n);
        vec3 reflected_color = raytrace3(reflected_ray); // reflection only requires a single ray
        return clamp(ambient + light*ref*0.3 *
            (0.3 * refracted_color + 0.2 * reflected_color), 0, 1); // weighted sum of raytrace collisions
    }
...
}
```

![](img/1695de1bc7486362f86c143285f3fb40_452_0.png)

**Figure 16.16**
Output of Program 16.11, showing the combination of the reflection, refraction, and textures: sphere with reflection only (left), sphere with refraction only (center), and sphere with both reflection and refraction (right)

## 16.3.4 Increasing the Number of Rays

What if we have a transparent object and behind it is another transparent object? Ideally, the ray tracer should generate a series of rays for the first and second transparent objects. Then, whichever surface is encountered behind the second object is what we would see. If the transparent objects were boxes (or spheres), how many rays would be required for the final object to appear? An example is shown in Figure 16.17, in which a green star is viewed through two transparent boxes. Since each transparent object would generally require two secondary rays (one entering the object and one leaving the object), we would need a total of five rays.

![](img/1695de1bc7486362f86c143285f3fb40_453_0.png)

However, that is not what the code we have built so far will do. Rather, we have hard-coded functions raytrace1(), raytrace2(), and raytrace3() that result in a maximum sequence of three rays (ignoring the shadow ray). So, in the example shown in Figure 16.17, the sequence of rays would stop at the second transparent object, and we wouldn't see the star at all. As the need for longer and longer sequences of rays increases, we cannot keep making more copies of the raytrace() function, as such a solution would not be scalable.

Another similar situation occurs if we have two highly reflective objects facing each other. Anyone who has done this with two mirrors knows the effect as they reflect back and forth between each other. Figure 16.18 shows such an example generated by one of the authors at his home. Our code could only do two reflections, but no subsequent reflections. A much longer sequence of rays is needed to achieve this effect.

![](img/1695de1bc7486362f86c143285f3fb40_453_1.png)

We actually faced this situation in the previous example from Program 16.11 (Figure 16.16) because both the box and the sphere were reflective. The effects of any additional rays in that particular example would be negligible, and in such cases, a depth of one or two rays is sufficient. However, in those cases where the additional rays are needed to achieve realistic results, we need a way of generating more rays.
