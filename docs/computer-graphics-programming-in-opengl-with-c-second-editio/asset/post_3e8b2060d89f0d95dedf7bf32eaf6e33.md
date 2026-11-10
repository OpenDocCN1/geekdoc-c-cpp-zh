
Program 16.7, with and without ADS lighting applied to the skybox (ADS lighting is applied to the other objects). Comparing figures 16.8 and 16.9 illustrates why lighting effects are generally appropriate for room boxes, but not for skyboxes.

![](img/1695de1bc7486362f86c143285f3fb40_440_0.png)

**Figure 16.9**
Output of Program 16.7 with and without ADS lighting applied to a skybox

### 16.2.10 Plane Intersection and Procedural Textures

In the previous examples, textures were provided in the form of texture image files. In some cases, a surface texture is sufficiently simple that it can be created procedurally, with the advantage that such textures are less likely to exhibit image-related artifacts.

In Program 16.8, we add a plane object (more precisely, a plane segment) to the scene, serving as a sort of table-top surface below the objects. Shadows are cast onto the plane object, but not onto the skybox. The plane has been textured with a checkerboard pattern, generated procedurally.

Computing the intersection point of a ray with a plane is significantly easier than it was for the sphere and the box because a plane has no “inside” that needs to be considered, so there is always at most one intersection point to consider. The derivation is well documented [§16]. Using standard geometry, the distance $t$ along a ray starting at position $r_s$ with direction $r_d$ when it intersects a horizontal plane centered at the origin with normal $n_p=(0,1,0)$ is:

$t = (-r_s \cdot n_p)/(r_d \cdot n_p)$

The intersection point is then, as before,

$collision\ point = r_s + t * r_d$

Given the plane’s width $w$ (i.e., on the $x$-axis) and depth $d$ (i.e., on the $z$-axis), the ray misses the plane segment when

$|collisionPoint_x| > \frac{w}{2}$ or $|collisionPoint_z| > \frac{d}{2}$

These can be generalized to planes at an arbitrary location and rotation using the non-axis-aligned methods described previously in Section 16.2.8. Similarly, the surface normal at the collision point, which so far has been fixed as (0,1,0), may be rotated if the plane is not aligned with the XZ-axes. Texture coordinates are just the $collisionPoint$ x and z coordinates, normalized to the range [0..1].

Computing the procedural checkerboard pattern of white and black colors can be done by scaling the texture coordinates up by the desired number of squares in the checkerboard, and then taking that result modulo 2. The result of 0 or 1 is then returned as either color (0,0,0) or (1,1,1) – i.e., black or white – respectively.

Note that as we increase the number of objects, the test for which collision is the closest (done in the get_closest_collision() function) is becoming increasingly complicated; we improve this design later. The added code for both the plane intersection and the procedural texture are given in Program 16.8, with the resulting output shown in Figure 16.10. All of the changes are in the compute shader.

### Program 16.8 – Plane Intersection and Procedural Texturing

Compute Shader

```glsl
...
vec3 plane_pos = vec3(0, -2.5, -2.0);  // position of the plane
float plane_width = 12.0;
float plane_depth = 8.0;
float plane_xrot = 0.0;                 // rotation of the plane
float plane_yrot = 0.0;
float plane_zrot = 0.0;
...
Collision intersect_plane_object(Ray r)
{
   // Compute the plane's local-space to world-space transform matrices and their inverses
   mat4 local_to_worldT = buildTranslate(plane_pos.x, plane_pos.y, plane_pos.z);
   mat4 local_to_worldR = buildRotateY(plane_yrot) * buildRotateX(plane_xrot) *
                           buildRotateZ(plane_zrot);

   mat4 local_to_worldTR = local_to_worldT * local_to_worldR;
   mat4 world_to_localTR = inverse(local_to_worldTR);
   mat4 world_to_localR = inverse(local_to_worldR);

   // Convert the world-space ray to the plane's local space:
   vec3 ray_start = (world_to_localTR * vec4(r.start,1.0)).xyz;
   vec3 ray_dir = (world_to_localR * vec4(r.dir,1.0)).xyz;

   Collision c;
   c.inside = false;  // there is no "inside" of a plane

   // compute intersection point of ray with plane
   c.t = dot((vec3(0,0,0) - ray_start), vec3(0,1,0)) / dot(ray_dir, vec3(0,1,0));

   // Calculate the world-position and plane-space positions of the intersection:
   c.p = r.start + c.t * r.dir;
   vec3 intersectPoint = ray_start + c.t * ray_dir;

   // if the ray didn't intersect the plane object, return a negative t value
   if (abs(intersectPoint.x) > (plane_width/2.0) || abs(intersectPoint.z) > (plane_depth/2.0))
   {  c.t = -1.0;
      return c;
   }

   // Create the collision normal, invert it if the ray hits the plane from underneath,
   // and convert to world space
   c.n = vec3(0, 1, 0);
   if(ray_dir.y > 0.0) c.n *= -1.0;
   c.n = transpose(inverse(mat3(local_to_worldR))) * c.n;

   // Compute texture coordinates
   float maxDimension = max(plane_width, plane_depth);
   c.tc = (intersectPoint.xz + plane_width/2.0)/maxDimension;
   return c;
}

Collision get_closest_collision(Ray r)
{  Collision cPlane;
   cPlane = intersect_plane_object(r);

   . . .

   if((cPlane.t > 0) &&
      ((cPlane.t < cSph.t) || (cSph.t < 0)&&(cPlane.t < cBox.t) || (cBox.t < 0)&&(cPlane.t <= cRBox.t) || (cRBox.t < 0))
   {
      closest_collision = cPlane;
      closest_collision.object_index = 4;    // object index of 4 designates collision with the plane
   }
   ...
}
vec3 checkerboard(vec2 tc)
{
    float tileScale = 24.0;
    float tile = mod(floor(tc.x * tileScale) + floor(tc.y * tileScale), 2.0);
    return tile * vec3(1,1,1);
}
vec3 raytrace(Ray r)
{
    ...
    if (c.object_index == 4) return ads_phong_lighting(r, c) * checkerboard(c.tc).xyz;
    ...
}
```

![](img/1695de1bc7486362f86c143285f3fb40_443_0.png)

**Figure 16.10**
Output of Program 16.8, showing the addition of a plane with a procedural checkerboard texture

```cpp
// this function is identical to raytrace() from Program 16.7 (see text for explanation)
...
vec3 raytrace(Ray r)
{
    Collision c = get_closest_collision(r);
    if (c.object_index == -1) return vec3(0.0);       // no collision
    if (c.object_index == 1)
    {
        // in the case of the sphere, determine the color by generating a secondary ray
        Ray reflected_ray;
        // compute start point of secondary ray, offset slightly to avoid colliding with the same object
        reflected_ray.start = c.p + c.n * 0.001;
        reflected_ray.dir = reflect(r.dir, c.n);
        vec3 reflected_color = raytrace2(reflected_ray);
        return c.mat.phong_lighting(r) * reflected_color;
    }
    ...
}
```

![](img/1695de1bc7486362f86c143285f3fb40_445_0.png)

**Figure 16.11**
Output of Program 16.9 showing a single reflected ray at the sphere object

Note that the sphere is now acting as a mirror, reflecting the surrounding skybox and the neighboring brick box and checkerboard plane. Recall that back in Chapter 8, we simulated a reflective object using environment mapping. The drawback there was that the environment-mapped objects were able to reflect the skybox, but not neighboring objects. By contrast, here ray tracing enables the reflective object to reflect all neighboring objects, in addition to the skybox. Also note that the front of the skybox (otherwise unseen because it is behind the camera) is now reflected in the sphere.

Figure 16.12 shows the result when we make the box object reflective and use the earth texture for the sphere. We have moved the box object behind the sphere so that its reflections are visible.

![](img/1695de1bc7486362f86c143285f3fb40_446_0.png)

**Figure 16.12**
Single reflected ray at the box object

In the code shown in Program 16.9, it would have been preferable to eliminate the raytrace2() function altogether and replace the call to raytrace2() with a recursive call to raytrace(). Unfortunately, GLSL doesn’t support recursion, so we duplicated the function. Later, as we increase the number of secondary rays, we will build an iterative version of raytrace() that keeps track of recursive ray generation.
