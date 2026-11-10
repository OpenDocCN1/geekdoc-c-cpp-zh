
```cpp
bool inside;       // whether the ray started inside of the object and collided while exiting
int object_index;  // index of the object this collision hit
};

float sphere_radius = 2.5;
vec3 sphere_position = vec3(1.0, 0.0, -3.0);
vec3 sphere_color = vec3(0.0, 0.0, 1.0);        // sphere color is blue

vec3 box_mins = vec3(-2.0, -2.0, 0.0);
vec3 box_maxs = vec3(0.5, 1.0, 2.0);
vec3 box_color = vec3(1.0, 0.0, 0.0);           // box color is red

//---------------------------------------------------------
// Checks if Ray r intersects the box
//---------------------------------------------------------
Collision intersect_box_object(Ray r)
{  // Calculate the box's world mins and maxs:
    vec3 t_min = (box_mins - r.start) / r.dir;
    vec3 t_max = (box_maxs - r.start) / r.dir;
    vec3 t_minDist = min(t_min, t_max);
    vec3 t_maxDist = max(t_min, t_max);
    float t_near = max(max(t_minDist.x, t_minDist.y), t_minDist.z);
    float t_far = min(min(t_maxDist.x, t_maxDist.y), t_maxDist.z);

    Collision c;
    c.t = t_near;
    c.inside = false;

    // If the ray didn't intersect the box, return a negative t value
    if (t_near >= t_far || t_far <= 0.0)
    {   c.t = -1.0;
        return c;
    }

    float intersect_distance = t_near;
    vec3 plane_intersect_distances = t_minDist;

    // if t_near < 0, then the ray started inside the box and left the box
    if (t_near < 0.0)
    {   c.t = t_far;
        intersect_distance = t_far;
        plane_intersect_distances = t_maxDist;
        c.inside = true;
    }

    // Checking which boundary the intersection lies on
    int face_index = 0;
    if (intersect_distance == plane_intersect_distances.y) face_index = 1;
    else if (intersect_distance == plane_intersect_distances.z) face_index = 2;
}

// Create the collision normal
c.n = vec3(0.0);
c.n[face_index] = 1.0;

// If we hit the box from the negative axis, invert the normal
if (r.dir[face_index] > 0.0) c.n *= -1.0;

// Calculate the world-position of the intersection
c.p = r.start + c.t * r.dir;
return c;
}

//-----------------------------------------------------------------------
// Checks if Ray r intersects the sphere
//-----------------------------------------------------------------------
Collision intersect_sphere_object(Ray r)
{
    float qa = dot(r.dir, r.dir);
    float qb = dot(2 * r.dir, r.start - sphere_position);
    float qc = dot(r.start - sphere_position, r.start - sphere_position) - sphere_radius * sphere_radius;

    // Solving for qa * t^2 + qb * t + qc = 0
    float qd = qb * qb - 4 * qa * qc;

    Collision c;
    c.inside = false;

    if (qd < 0.0)    // no solution in this case
    {
        c.t = -1.0;
        return c;
    }

    float t1 = (-qb + sqrt(qd)) / (2.0 * qa);
    float t2 = (-qb - sqrt(qd)) / (2.0 * qa);
    float t_near = min(t1, t2);
    float t_far = max(t1, t2);
    c.t = t_near;

    if (t_far < 0.0)    // sphere is behind the ray, no intersection
    {
        c.t = -1.0;
        return c;
    }
    if (t_near < 0.0)    // the ray started inside the sphere
    {
        c.t = t_far;
        c.inside = true;
    }

    c.p = r.start + c.t * r.dir;    // world position of the collision
    c.n = normalize(c.p - sphere_position);    // use the world position to compute the surface normal

    if (c.inside)   // if collision is leaving the sphere, flip the normal
    {
        c.n *= -1.0;
    }
    return c;
}

//------------------------------------------------------------------------
// Returns the closest collision of a ray
// object_index == -1 if no collision
// object_index == 1 if collision with sphere
// object_index == 2 if collision with box
//------------------------------------------------------------------------

Collision get_closest_collision(Ray r)
{
    Collision closest_collision, cSph, cBox;
    closest_collision.object_index = -1;

    cSph = intersect_sphere_object(r);
    cBox = intersect_box_object(r);

    if ((cSph.t > 0) && ((cSph.t < cBox.t) || (cBox.t < 0)))
    {
        closest_collision = cSph;
        closest_collision.object_index = 1;
    }
    if ((cBox.t > 0) && ((cBox.t < cSph.t) || (cSph.t < 0)))
    {
        closest_collision = cBox;
        closest_collision.object_index = 2;
    }
    return closest_collision;
}

//------------------------------------------------------------------------
// This function casts a ray into the scene and returns the final color for a pixel
//------------------------------------------------------------------------
vec3 raytrace(Ray r)
{
    Collision c = get_closest_collision(r);
    if (c.object_index == -1) return vec3(0.0);       // if no collision, return black
    if (c.object_index == 1) return sphere_color;
    if (c.object_index == 2) return box_color;
}

void main()
{
    int width = int(gl_NumWorkGroups.x);  // one workgroup = one invocation = one pixel
    int height = int(gl_NumWorkGroups.y);
    ivec2 pixel = ivec2(gl_GlobalInvocationID.xy);

    // convert this pixel's screen space location to world space
    float x_pixel = 2.0 * pixel.x / width - 1.0;
    float y_pixel = 2.0 * pixel.y / height - 1.0;

    // Get this pixel's world-space ray
    Ray world_ray;
    world_ray.start = vec3(0.0, 0.0, camera_pos_z);
    vec4 world_ray_end = vec4(x_pixel, y_pixel, camera_pos_z - 1.0, 1.0);
    world_ray.dir = normalize(world_ray_end.xyz - world_ray.start);

    // Cast the ray out into the world and intersect the ray with objects
    vec3 color = raytrace(world_ray);
    imageStore(output_texture, pixel, vec4(color, 1.0));
}
```

The declarations at the top of the compute shader start by setting the work-group size to 1, as described earlier. A uniform variable for the output texture image is then defined, as well as the camera position (in this example we limit the camera to being positioned along the Z axis, facing in the negative Z direction). Then, structs are declared for defining *rays* (their origins and directions) and *collisions*. Collisions include information about a ray intersecting an object, e.g., the distance along the ray, collision location in world coordinates, which object is hit, and the normal at the surface point of the collision, which will be used later when we add lighting. The declarations conclude by creating variables for the location and color of the objects we intend to draw (in this case, a box and a sphere).

The main() function, shown at the bottom of the code listing, starts by using the work group's invocationID to determine the pixel's X/Y location in the screen-space grid, then converts that from the range [0..width] to the range [-1..+1] corresponding to where the pixel is positioned in the scene's world coordinate system. A ray starting at the camera position and passing through this point is then created, assuming that the render grid is placed a distance of 1.0 (along the Z axis) in front of the camera. main() then calls raytrace(), which accepts a ray and returns the color of the nearest object hit by that ray. main() then stores that color in the image.

The raytrace() function calls get_closest_collision(), which returns a Collision object containing the index of the first object with which the ray collides; raytrace() then returns the color of that object. If the ray doesn't collide with any object in the scene, raytrace() returns the default color (set to black in this example). The get_closest_collision() function works by finding the collision point(s) with the sphere object and the box object (via the functions intersect_sphere_object() and intersect_box_object(), respectively), and returning the collision that has the shortest ray. If there is no colliding object, a special value of -1 is returned.

### 16.2.3 Ray-Sphere Intersection

Computing the intersection(s) of a ray with a sphere is derived using geometry and is well-documented [S16]. Although the derivation is relatively simple, here we describe only the solution. There are either 0, 1, or 2 intersection points, depending on if the ray misses the sphere, skims the surface, or enters on one side and exits out the other. Given the ray's origin r_s and direction r_d, and the sphere's position s_p and radius s_r, then finding the distance t along the ray at which the intersection(s) occur requires solving the following quadratic equation:

$$ (r_d \cdot r_d)t^2 + 2(r_d \cdot [r_s - s_p])t + [r_s - s_p]^2 - s_r^2 = 0 \quad [1] $$

First, we compute its discriminant¹:

$$ \Delta = (2r_d \cdot [r_s - s_p])^2 - 4|r_d|^2(|r_s - s_p|^2 - s_r^2) $$

If Δ < 0, we can stop because the ray misses the sphere (and to avoid attempting to take the square root of a negative number). When Δ is not less than zero, there are then two solutions to equation [1]:

$$ t = \frac{(-2r_d \cdot [r_s - s_p]) \pm \sqrt{\Delta}}{2(r_d \cdot r_d)} $$

The smaller and larger of the two resulting values of t are denoted t_near and t_far, respectively.

- When both t_near and t_far are negative, the entire sphere is behind the ray and there is no intersection.

¹ In the code, we sometimes compute the square of the length of a vector V⃗ by computing V⃗ • V⃗, for performance reasons.
