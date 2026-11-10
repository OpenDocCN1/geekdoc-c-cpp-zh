```
```glsl
glBindTexture(GL_TEXTURE_2D, znTex);
glActiveTexture(GL_TEXTURE0);
glDispatchCompute(workGroupsX, workGroupsY, workGroupsZ);
⋯
}
```
```

# Compute Shader

```
```glsl
⋯
layout (binding=3) uniform sampler2D ynTex;
layout (binding=4) uniform sampler2D xnTex;
layout (binding=5) uniform sampler2D ypTex;
layout (binding=6) uniform sampler2D ynTex;
layout (binding=7) uniform sampler2D zpTex;
layout (binding=8) uniform sampler2D znTex;
⋯
struct Collision
{
    float t;           // value at which this collision occurs for a ray
    vec3 p;             // world position of the collision
    vec3 n;             // normal of the collision
    bool inside;        // whether the collision occurs inside of the object
    int object_index;   // index of the object this collision hit
    vec2 tc;            // texture coordinates for the object at the collision point
    int face_index;     // which box face collides (for textured skybox)
};
⋯
Collision intersect_sky_box_object(Ray r)
{
    ⋯
    // Calculate face index for collision object (assumes that the normal vectors are of length 1)
    if (c.n == vec3(1,0,0)) c.face_index = 0;
    else if (c.n == vec3(-1,0,0)) c.face_index = 1;
    else if (c.n == vec3(0,1,0)) c.face_index = 2;
    else if (c.n == vec3(0,-1,0)) c.face_index = 3;
    else if (c.n == vec3(0,0,1)) c.face_index = 4;
    else if (c.n == vec3(0,0,-1)) c.face_index = 5;

    // Compute texture coordinates
    float totalWidth = skybox_maxs.x - skybox_mins.x;
    float totalHeight = skybox_maxs.y - skybox_mins.y;
    float totalDepth = skybox_maxs.z - skybox_mins.z;
    float maxDimension = max(totalWidth, max(totalHeight, totalDepth));

    // select tex coordinates depending on box face
    float rayStrikeX = (c.p).x + totalWidth/2.0)/maxDimension;
    float rayStrikeY = (c.p).y + totalHeight/2.0)/maxDimension;
    float rayStrikeZ = (c.p).z + totalDepth/2.0)/maxDimension;
```
```