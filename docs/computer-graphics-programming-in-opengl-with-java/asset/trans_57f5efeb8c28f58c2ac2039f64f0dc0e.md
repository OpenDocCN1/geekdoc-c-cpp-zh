

```glsl
if (c.object_index == 1) return ads_phong_lighting(r,c) * (texture(sampEarth, c.tc).xyz);
if (c.object_index == 2) return ads_phong_lighting(r,c) * (texture(sampBrick, c.tc).xyz);
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_441_0.png)

图16.7  
示例纹理以及程序16.6的输出，其中添加了纹理坐标。

如果该长方体要作为房间盒或天空盒使用，就需要以略有不同的方式计算纹理坐标，以便与我们第9章中看到的纹理映射方法相匹配。我们可以先在场景中添加第二个长方体，具体来说是一个*轴对齐盒*，如程序16.2中所描述的那样，并采用纯色。图16.8展示了这样一个大小为20x20x20的长方体被添加到场景中。由于摄像机位于长方体内部，因此只有长方体的内侧面可见。另外请注意，在本示例中，场景中的物体会在长方体上投射阴影，就像房间盒的情况一样。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_442_0.png)

计算纹理坐标以应用房间盒或天空盒纹理，取决于我们希望使用单一纹理（如图9.1所示）还是六个单独的纹理（长方体的每个面对应一个）。程序16.7实现了后一种方法，并增加了一个专门用于处理房间盒或天空盒的求交方法。这里展示了Java/JOGL应用程序和计算着色器两方面的改动。在Java程序中，六个纹理被加载并分配到纹理单元；在计算着色器中，它们被采样，并根据射线与哪个面碰撞而被选择。具体是六个面中的哪一个，可以通过法向量轻松确定，因为每个长方体面的法向量不同。随后，纹理坐标的计算方式与程序16.6所示类似。最后请注意，随着场景中物体越来越多，确定最近碰撞所需的测试数量会迅速增加。

² 请注意右下角的接缝。程序16.4中light_ray_start的.01偏移量（用于消除阴影粉刺）在角落处无效，因为法线与相邻的长方体侧面相切。对于不使用阴影的天空盒来说，这不是问题。

## 程序16.7 为天空盒添加纹理

### Java/JOGL 应用程序

```java
...
private int xpTex, xnTex, ypTex, ynTex, zpTex, znTex;        // added to the top-level declarations

public void init(GLAutoDrawable drawable)
{
    ...
    xpTex = Utils.loadTexture("code/cubeMap/xp.jpg");
    xnTex = Utils.loadTexture("code/cubeMap/xn.jpg");
    ypTex = Utils.loadTexture("code/cubeMap/yp.jpg");
    ynTex = Utils.loadTexture("code/cubeMap/yn.jpg");
    zpTex = Utils.loadTexture("code/cubeMap/zp.jpg");
    znTex = Utils.loadTexture("code/cubeMap/zn.jpg");
}

public void display(GLAutoDrawable drawable)
{
    gl.glBindImageTexture(0, screenTextureID[0], 0, false, 0, GL_WRITE_ONLY, GL_RGBA8);
    gl.glActiveTexture(GL_TEXTURE3);
    gl.glBindTexture(GL_TEXTURE_2D, xpTex);
    gl.glActiveTexture(GL_TEXTURE4);
    gl.glBindTexture(GL_TEXTURE_2D, xnTex);
    gl.glActiveTexture(GL_TEXTURE5);
    gl.glBindTexture(GL_TEXTURE_2D, ypTex);
    gl.glActiveTexture(GL_TEXTURE6);
    gl.glBindTexture(GL_TEXTURE_2D, ynTex);
    gl.glActiveTexture(GL_TEXTURE7);
    gl.glBindTexture(GL_TEXTURE_2D, zpTex);
    gl.glActiveTexture(GL_TEXTURE8);
    gl.glBindTexture(GL_TEXTURE_2D, znTex);
    gl.glActiveTexture(GL_TEXTURE0);
    gl.glDispatchCompute(workGroupsX, workGroupsY, workGroupsZ);
    ...
}
```

### 计算着色器

```glsl
...
layout (binding=3) uniform sampler2D xpTex;
layout (binding=4) uniform sampler2D xnTex;
layout (binding=5) uniform sampler2D ypTex;
layout (binding=6) uniform sampler2D ynTex;
layout (binding=7) uniform sampler2D zpTex;
layout (binding=8) uniform sampler2D znTex;
...
struct Collision
{
    float t;                 // value at which this collision occurs for a ray
    vec3 p;                  // world position of the collision
    vec3 n;                  // normal of the collision
    bool inside;             // whether the collision occurs inside of the object
    int object_index;        // index of the object this collision hit
    vec2 tc;                 // texture coordinates for the object at the collision point
    int face_index;          // which box face collides (for textured skybox)
};

...
Collision intersect_sky_box_object(Ray r)
{
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
    float rayStrikeX = ((c.p).x + totalWidth/2.0)/maxDimension;
    float rayStrikeY = ((c.p).y + totalHeight/2.0)/maxDimension;
    float rayStrikeZ = ((c.p).z + totalDepth/2.0)/maxDimension;

    if (c.face_index == 0) c.tc = vec2(rayStrikeZ, rayStrikeY);
    else if (c.face_index == 1) c.tc = vec2(1.0-rayStrikeZ, rayStrikeY);
    else if (c.face_index == 2) c.tc = vec2(rayStrikeX, rayStrikeZ);
    else if (c.face_index == 3) c.tc = vec2(1.0-rayStrikeX, rayStrikeZ);
    else if (c.face_index == 4) c.tc = vec2(1.0-rayStrikeX, rayStrikeY);
    else if (c.face_index == 5) c.tc = vec2(rayStrikeX, rayStrikeY);
    return c;
}

...
Collision get_closest_collision(Ray r)
{ ...
    Collision closest_collision, cSph, cBox, cSBox;
...
    cSBox = intersect_sky_box_object(r);
...
    // determine which collision is the closest
    if ((cBox.t > 0) && ((cSph.t < cBox.t) || (cSph.t < 0)) && ((cSBox.t < cBox.t) || (cBox.t < 0)))
    {
        closest_collision = cSBox;
        closest_collision.object_index = 3;
    }
    return closest_collision;
}

vec3 raytrace(Ray r)
{  Collision c = get_closest_collision(r);
   if (c.object_index == -1) return vec3(0.0); // no collision
   if (c.object_index == 1) return ads_phong_lighting(r,c) * (texture(sampEarth, c.tc).xyz);
   if (c.object_index == 2) return ads_phong_lighting(r,c) * (texture(sampBrick, c.tc).xyz);
   if (c.object_index == 3)      // this example is a skybox, so we return only the texture, without lighting
   {  if (c.face_index == 0) return texture(xnTex, c.tc).xyz; // sample -X face texture image
      else if (c.face_index == 1) return texture(xpTex, c.tc).xyz; // sample +X face texture image
      else if (c.face_index == 2) return texture(ynTex, c.tc).xyz; // sample -Y face texture image
      else if (c.face_index == 3) return texture(ypTex, c.tc).xyz; // sample +Y face texture image
      else if (c.face_index == 4) return texture(znTex, c.tc).xyz; // sample -Z face texture image
      else if (c.face_index == 5) return texture(zpTex, c.tc).xyz; // sample +Z face texture image
   }
}
```

请注意，在程序16.7中，当射线最近的碰撞对象是天空盒时，我们没有包含ADS光照（这可以在计算着色器的raytrace()函数中看到），因为天空盒不应响应光照。对于房间盒，我们会包含ADS光照，但前提是立方体各面的图像严格对应房间的墙壁。图16.9展示了程序16.7的输出，其中天空盒分别应用了ADS光照和未应用ADS光照（ADS光照应用于其他物体）。对比图16.8和图16.9，可以说明为什么光照效果通常适用于房间盒，而不适用于天空盒。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_446_0.png)

**图16.9**  
程序16.7的输出，对天空盒应用和不应用ADS光照。

## 16.7.10 平面求交与程序化纹理

在之前的示例中，纹理以纹理图像文件的形式提供。在某些情况下，表面纹理非常简单，可以通过程序化方式生成，其优点是此类纹理不太可能出现与图像相关的伪影。

在程序16.8中，我们向场景中添加了一个平面对象（更准确地说，是一个平面段），用作物体下方的一种桌面表面。阴影投射到平面对象上，但不投射到天空盒上。该平面使用程序化生成的棋盘格图案进行了纹理映射。

计算射线与平面的交点比计算射线与球体和长方体的交点要简单得多，因为平面没有需要考虑的“内部”，因此最多只有一个交点需要考虑。推导过程有充分的文献记载[S16]。使用标准几何，从位置r_s出发、方向为r_d的射线，在原点为中心、法线为n_p = (0,1,0)的水平平面上相交时，沿射线的距离t为

$$ t = \frac{(-r_s \cdot n_p)}{(r_d \cdot n_p)} $$

