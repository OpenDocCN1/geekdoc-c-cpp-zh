```
~~~cpp
// Calculate the box's world mins and maxs:
vec3 t_min = (box_mins - ray.start) / ray.dir;
vec3 t_max = (box_maxs - ray.start) / ray.dir;
vec3 t1 = min(t_min, t_max);
vec3 t2 = max(t_min, t_max);
float t_near = max(max(t1.x, t1.y), t1.z);
float t_far = min(min(t2.x, t2.y), t2.z);
. . .
// The computations for determining the collision, which surface of the box
// is intersected, and the normal at the collision are unchanged from before.
// There is one addition to the normal vector computation, shown next in red.
. . .
// If we hit the box from the negative axis, invert the normal
if(ray.dir[face_index] > 0.0) c.n *= -1.0;

// now convert the normal back into world space
c.n = transpose(inverse(mat3(local_to_world))) * c.n;

// Calculate the world-position of the intersection:
c.p = r.start + c.t * r.dir;

return c;
}
~~~
```

![](bbox=[0.29, 0.547, 0.7, 0.886])

**Figure 16.6** Output of Program 16.5 showing simple ray casting with a non-axis-aligned box