
这些阶段不需要生成额外光线（碰撞检测、光照/阴影和纹理化）。然而，反射和折射阶段都需要生成一条新光线，并对新光线执行 `process_stack_element()`。由于 GLSL 中无法进行这种递归调用，我们调整当前栈元素的内容，以记录我们执行到的位置，压入一个包含待处理新光线的新栈元素，然后退出 `process_stack_element()`。驱动函数——新版本的 `rayTrace()`——随后继续迭代调用 `process_stack_element()`，直到每个栈元素（每条光线）都有机会完成全部五个阶段。最终结果与可以使用递归时相同。

Program 16.12 中的代码（声明以及 `push()`、`pop()`、`process_stack_element()` 和 `rayTrace()` 函数）替换了 Program 16.11 中之前的 `rayTrace()` 函数（及其“子”函数 `rayTrace2()` 和 `rayTrace3()`）。Program 16.12 的其余部分与 Program 16.11 相同。

Program 16.12 的输出取决于 `max_depth` 设置。该值越大，可生成的光线序列越长。图 16.19 显示了 `max_depth` 值为 0、1、2、3 和 4 时的输出。

![](img/1695de1bc7486362f86c143285f3fb40_458_0.png)

**图 16.19**
Program 16.12 的输出，显示递归深度值 0、1、2、3 和 4（从左到右，从上到下）

```cpp
struct Object {
float radius;        // sphere radius (only relevant if type=sphere)
vec3  mins;          // box corner (if type=box). If type=plane, X and Z values are width and depth
vec3  maxs;          // opposite box corner (if type=box)
float xrot;          // X component of object rotation (only relevant if type=box or plane)
float yrot;          // Y component of object rotation (only relevant if type=box or plane)
float zrot;          // Z component of object rotation (only relevant if type=box or plane)
vec3  position;      // location of center of object
bool  hasColor;      // whether or not the object has a particular color specified
bool  hasTexture;    // whether or not the object includes a texture image in computing its color
bool  isReflective;  // whether or not the object is reflective (generates a secondary ray)
                     // (if the object is a room box, this field is used to enable or disable lighting)
bool  isTransparent; // whether or not the object is refractive (generates a secondary ray)
vec3  color;         // the RGB color specified for the object (only relevant if hasColor is true)
float reflectivity;  // percentage of reflective color to include (only relevant if isReflective is true)
float refractivity;  // percentage of refractive color to include (only relevant if isTransparent)
float IOR;           // Index of Refraction (only relevant if isTransparent is true)
vec4  ambient;       // ADS ambient material characteristic
vec4  diffuse;       // ADS diffuse material characteristic
vec4  specular;      // ADS specular material characteristic
float shininess;     // ADS shininess material characteristic
};

Object[] objects =
{  // object #0 is the room box
   { 0, 0.0, vec3(-20, -20, -20), vec3( 20, 20, 20), 0, 0, 0, vec3(0), true, false, true, false, vec3(0.25,
     1.0, 1.0), 0, 0, vec4(0.2, 0.2, 0.2, 1.0), vec4(0.9, 0.9, 0.9, 1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
   },
   // object #1 is the checkerboard ground plane
   { 3, 0.0, vec3(12, 0, 16), vec3(0), 0, 0, 0, vec3(0.0, -1.0, -2.0), false, true, false, false, vec3(0),
     0.0, 0.0, 0.0, vec4(0.2, 0.2, 0.2, 1.0), vec4(0.9, 0.9, 0.9, 1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
   },
   // object #2 is the transparent sphere with slight reflection and no texture
   { 1, 1.2, vec3(0), vec3(0), 0, 0, 0, vec3(0.7, 0.2, 2.0), false, true, true, true, vec3(0),
     0.8, 0.8, 1.5, vec4(0.5, 0.5, 0.5, 1.0), vec4(1.0,1.0,1.0,1.0), vec4(1.0, 1.0, 1.0, 1.0), 50.0
   },
   // object #3 is the slightly reflective box with texture
   { 2, 0.0, vec3(-0.25, -0.8, -0.25), vec3(0.25, 0.8, 0.25), 0, 0, 70.0, 0.0, vec3(-0.75, -0.2, 3.4),
     false, true, true, false, vec3(0), 0.5, 0.0, 0.0, vec4(0.5, 0.5, 0.5, 1.0), vec4(1.0, 1.0, 1.0, 1.0),
     vec4(1.0, 1.0, 1.0, 1.0), 50.0
   }
};
int numObjects = 4;
...
vec3 getTextureColor(int index, vec2 tc)
{ // customized for this scene
    if (index==1) return checkerboard(tc).xyz;
    else if (index==3) return texture(sampMarble, tc).xyz;
    else return vec3(1.0, 0.7, 0.7); // return pink if index is for an object other than the plane or box
}

Collision intersect_plane_object(Ray r, Object o)
{
    ...
    mat4 local_to_worldT = buildTranslate(vec3(o.position.x, o.position.y, o.position.z));
    mat4 local_to_worldR =
        buildRotateY(DEG_TO_RAD * o.yrot) * buildRotateX(DEG_TO_RAD * o.xrot) *
        buildRotateZ(DEG_TO_RAD * o.zrot);
    ...
} // similar object references in other intersection functions also changed to 'o.position', 'o.mins', etc.

//------------------------------------------------------------------
// Returns the closest collision of a ray
// object_index == -1 if no collision
// object_index == 0 if collision with room box
// object_index > 0 if collision with another object
//------------------------------------------------------------------
Collision get_closest_collision(Ray r)
{ float closest = 3.402823466e+38; // initialize to a very large number (max value of a float)
    Collision closest_collision;
    closest_collision.object_index = -1;

    for (int i=0; i<numObjects; i++)
    { Collision c;
        if (objects[i].type == 0)
        { c = intersect_room_box_object(r);
            if (c.t <= 0) continue; // ray didn't collide with this skybox object
        }
        else if (objects[i].type == 1)
        { c = intersect_sphere_object(r, objects[i]);
            if (c.t <= 0) continue; // ray didn't collide with this sphere object
        }
        else if (objects[i].type == 2)
        { c = intersect_box_object(r, objects[i]);
            if (c.t <= 0) continue; // ray didn't collide with this box object
        }
        else if (objects[i].type == 3)
        { c = intersect_plane_object(r, objects[i]);
            if (c.t <= 0) continue; // ray didn't collide with this plane object
        }
        else continue;             // in case we have any non-collidable object types
        if (c.t < closest)		// we found a collision, now check if it is closer than the current closest
        {
            closest = c.t;
            closest_collision = c;
            closest_collision.object_index = i;
        }
    }
    return closest_collision;
}
...
void process_stack_element(int index)
{
    ... // phases 1-4 remain unchanged
    // PHASE 5 - Mixing to produce the final color – generalized for any combination of these objects
    if(stack[index].phase == 5)
    {
        if (c.object_index > 0) // we collided with something, and it is not a room box
        {
            // first get texture color if applicable
            vec3 texColor = vec3(0.0);
            if (objects[c.object_index].hasTexture)
                texColor = getTextureColor(c.object_index, c.tc);

            // next, get object color if applicable
            vec3 objColor = vec3(0.0);
            if (objects[c.object_index].hasColor)
                objColor = objects[c.object_index].color;

            // then get reflected and refractive colors, if they are needed later
            vec3 reflected_color = stack[index].reflected_color;
            vec3 refracted_color = stack[index].refracted_color;

            // Now build the mix of colors – if it is the last color, just return it without blending
            vec3 mixed_color = objColor + texColor;
            if ((objects[c.object_index].isReflective) && (stack[index].depth < max_depth))
                mixed_color = mix(mixed_color, reflected_color, objects[c.object_index].reflectivity);
            if ((objects[c.object_index].isTransparent) && (stack[index].depth < max_depth))
                mixed_color = mix(mixed_color, refracted_color, objects[c.object_index].refractivity);
            stack[index].final_color = mixed_color * stack[index].phong_color;
        }

        if (c.object_index == 0)        // room box object is unique because it might have six textures
        {
            vec3 lightFactor = vec3(1.0);        // holds the lighting value if isReflective is true
            if (objects[c.object_index].isReflective) lightFactor = stack[index].phong_color;

            if (objects[c.object_index].hasColor) // here, roomboxes have color or texture (not both)
                stack[index].final_color = lightFactor * objects[c.object_index].color;
            else
            {
                if (c.face_index == 0) stack[index].final_color = lightFactor * getTextureColor(5, c.tc);
```
